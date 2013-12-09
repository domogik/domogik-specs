\_\_Important update : the new documentation of this plugin is [http://docs.domogik.org/plugin/cron/dev/en/index.html]\_\_

The following documentation below is (or surely will be) outdated. Some parts of it will be added in ReST one when needed.

The purpose of this plugin is to offer cron jobs over XPL.
It can act as a timer, a date, an interval or a cron like server. It will send an xpl message at the specified date.
It can be called in pure XPL or via the client library.
See documentation `here <http://xplproject.org.uk/wiki/index.php?title=Schema\_-\_TIMER>`_ for more details.

Prerequisites
==============

Normally you don't need to do this, but ...
* install the apscheduler extension for python:
__sudo easy_install apscheduler__

Install the plugin
===================

This plugin is available in the development sources. Follow this `documentation|nocache <http://wiki.domogik.org/Developers\_installation>`_ to install them.
Enable the plugin :
__dmgenplug cron__

There is no options to configure the plugin so just start it.

Adding cron jobs
=================

This plugin is in alpha developpment, so there is actually no user interface. 
If you want to add alarms, you could use the `zalarms plugin <http://wiki.domogik.org/plugin\_zalarms>`_.

Adding a device to interact with a cron job
============================================

Add a cron.job device from the cron technology. Choose the usage christmas tree.
You must use the name ( device / cron job) created previously as address (christmas).

Next add the widgets :
One for the status and another for the switch (stateless basic widget).
Now, you can resume or stop the cron job using the On/Off buttons of the widget. When a cron job is stopped, it don't send message anymore. But it stays in memory. You can restart it using the resume (on) button.

Jobs are permanently stored in the plugin So if you want to remove it permanently, you must halt it.
You can add a halt widget (stateless basic widget) to do it and click the off button. If you have a status widget, you will see it taking the "halted" status.
You can also send an xpl message to halt a job. Loook at the documentation below to do it.

 Plugin developpers
====================

The following documentation is for plugin developpers, specially the query_cron library. It can be usefull if you want to planned some events in your plugin.
How it works
*************

First, you need to create a device (a cron job in the timer.basic schema) with the client library, by sending an xpl message or using the plugin zalarms. Keep in mind that devices always stay in memory, until you halt (remove)  them.
Here is the step to manage a device.
#First, you need to start it. That will create the device and activate it.
#Now, you cant stop it : stop sending messages
#you can resume it : will send messages again 
#and halt it : this will stop the device and destroy it. You can't resume it anymore.

Using the client library
*************************

After starting the cron plugin (server) you could use the library to create your cron job inside your plugin.
I use this library in the dawndusk one. Look at the code with me :

Import the library
.. code-block:: json


    from domogik.xpl.lib.cron_query import cronQuery{CODE}
    
    Initialize the class
.. code-block:: json


    self._cronQuery = cronQuery(self.myxpl,self.log){CODE}

Create the message you want to receive
.. code-block:: json


    nstMess = XplMessage()
    nstMess.set_type("xpl-trig")
    nstMess.set_schema("dawndusk.basic")
    nstMess.add_data({"type" : "dawndusk"})
    nstMess.add_data({"status" :  "dawn"})


And create the cron job
.. code-block:: json


    self._cronQuery.startDateJob("mydevice",nstMess,"YYYYMMDDHHMMSS"){CODE}
    You will receive the message at date YYYYMMDDHHMMSS :)
    
    Using xpl messages :
    *********************
    
    First case of use : I want to start my christmas tree at 7:00 every morning and stop it at 9:00. In the evening, I want to start it at 17:00 and stop it at 21:00. In the weekend, start it at 10:00 and stop it at 23:00.
    I want to send an on (off) command, using the telldus.basic schema to device TS34
    Here is the message to send
.. code-block:: json


    xpl-cmnd
    timer.basic
         {
          action=start
          device=christmas
          devicetype=alarm
          alarm=MoTuWeThFr,07:00-09:00,17:00-21:00
          alarm=SaSu,10:00-23:00
          nst-xpltype=xpl-cmnd 
          nst-schema=telldus.basic
          parameter0=command
          valueon0=on
          valueoff0=off
          nst-device=TS34
          }

Second case of use : I want to emulate the dawn in my bedroom using a dimmer
Start the dawn process at 6:00 in the week. At 7:00, the dimmer will be at 100%.
Wake up lately in the weekend
I want to use the device TS35 using the telldus.basic schema.
Here is the message to send
xpl-cmnd
.. code-block:: json


    timer.basic
         {
          action=start
          device=wakeup
          devicetype=dawnalarm
          alarm=MoTuWeThFr,06:00-07:00
          alarm=SaSu,09:00-10:00
          nst-xpltype=xpl-cmnd 
          nst-schema=telldus.basic
          nst-device=TS35
          }


The different types of jobs
****************************

This plugin use TIMER.BASIC `schema <http://xplproject.org.uk/wiki/index.php?title=Schema\_-\_TIMER>`_, and update it ;)

!!!!The timer
It works as a heartbeat sending message every ''frequence'' seconds.
.. code-block:: json


        def startTimerJob(self, device, nstMess, frequence, duration=0):
            '''
            Start a job of type timer
            @param device : the name of the job (=device in xpl)
            timer.basic
               {
                action=start
                device=<name of the timer>
                [devicetype=timer]
                [duration=0 or empty|integer]
                [frequence=integer. 45 by default]
               }
    


!!!!The date
Send a message at the specified date.
.. code-block:: json


        def startDateJob(self, device, nstMess, sdate):
            '''
            Start a job of type date
            @param device : the name of the job (=device in xpl)
            timer.basic
               {
                action=start
                device=<name of the timer>
                devicetype=date
                date= the datetime of the job (YYYYMMDDHHMMSS)
               }
             '''
    


!!!!The interval
A more elaborated heartbeat.
.. code-block:: json


        def startIntervalJob( self, device, nstMess, weeks=0,days=0,hours=0,
                              minutes=0,seconds=0,startdate=None):
            '''
            Start a job of type interval
            @param device : the name of the job (=device in xpl)
            timer.basic
               {
                action=start
                device=<name of the timer>
                devicetype=interval
                [weeks=0]
                [days=0]
                [hours=0]
                [minutes=0]
                [seconds=0]
                [startdate=YYYYMMDDHHMMSS]
               }
            '''
     
    

For a complete description of syntax, look at this `page <http://packages.python.org/APScheduler/intervalschedule.html>`_.


!!!!The cron like
The more sophisticated one.
.. code-block:: json


        def startCronJob( self, device, nstMess, year=None,month=None,day=None,
                          week=None,dayofweek=None,hour=None,
                          minute=None,second=None,startdate=None):
            '''
            Start a job of type cron
            @param device : the name of the job (=device in xpl)
            timer.basic
               {
                action=start
                device=<name of the timer>
                devicetype=cron
                [year= ... ]
                [month= ... ]
                [day= ... ]
                [week= ... ]
                [dayofweek= ... ]
                [hour= ... ]
                [minute= ... ]
                [second= ... ]
                [startdate=YYYYMMDDHHMMSS]
               }
            '''
    

For a complete description of syntax, look at this `page <http://packages.python.org/APScheduler/cronschedule.html>`_.

!!!!The alarm
Turn on and off a device.

.. code-block:: json


        def startDawnAlarmJob( self, device, nstMess, params={}, alarms=list()):
            """
            Start a job of type alarm
    
            The format of the timer value consists of a list of
            two-character codes for the days of the week (each code is
            simply the first two letters of the day) on which the timer
            will be active (with no delimiters)
            The second parameter is a simple time or an interval time.
            If the period is an interval, a valueOn message is sent first and
            a valueOff is send at the end of te period
            The time in the form hh:mm using the 24 hour clock.
    
            For example, for defining one alarm during the week at 6:30 and another
            for the weekend at 8:00 :
            You can also create an alarm to turn on your christmas tree twice a day.
            timer.basic
               {
                action=start
                device=<name of the timer>
                devicetype=alarm
                alarm=MoTuWeThFr,09:30
                alarm=SaSu,08:00
                alarm=SaSu,08:00,18:00
                alarm=MoTuWeThFrSaSu,07:00-08:00,17:00-21:00
             }
            '''
    


!!!!The dawnalarm
Turn on a light, simulating the dawn
.. code-block:: json


        def startJobDawnAlarm(self, device):
            """
            Start a job of type dawnalarm
            A dawnalarm emulates the dawn using a dimmer device.
    
            The format of the timer value consists of a list of
            two-character codes for the days of the week (each code is
            simply the first two letters of the day) on which the timer
            will be active (with no delimiters)
            The second parameter is an interval time : the begin and the end
            of the dawn process.
            The times are in the form hh:mm using the 24 hour clock.
            The next parameters are the dim level of the device
            (from 00 to 99). If none are specified, we use 10,20,...,90
    
            For example, for defining one alarm starting at 6:00 and
            finishing at 6:30 with 4 status (10,40,70,90)
            and another for the weekend starting at 7:00 ans finishing at 8:00
            with the standard dim levels :
            timer.basic
               {
                action=start
                device=<name of the timer>
                devicetype=dawnalarm
                alarm=MoTuWeThFr,06:00-06:30,10,40,70,90
                alarm=SaSu,07:00-08:00
             }
    
            """
    


!!!!The HVAC timer
Program a timer with the HVAC syntaxe. The full documentation is `here <http://xplproject.org.uk/wiki/index.php?title=Schema\_-\_HVAC>`_.
.. code-block:: json


        startHvacJob( self, device, nstMess, params={}, timers={}):
            """
            Start a job of type hvac
            This schema reports the current timer settings. It is sent as
            an xPL status message if requested by an hvac.request
            with request=timer, or as a trigger message when a timer
            value is changed.
    
            The timer elements define the days and times on which the
            hvac system will be active. There can be more than one
            timer= element in the message. This allows different time
            periods to be set for different days of the week (for example,
            additional heating at weekends, when the house may be occupied
            for a greater portion of the day).The timer values provided in
            this message replace any previous timer settings, so the message
            contains all the timer information for the zone.
    
            The format of the timer value consists of a list of
            two-character codes for the days of the week (each code is
            simply the first two letters of the day) on which the timer
            will be active (with no delimiters), followed by a comma
            separated list of time periods. Each time period is formed
            from a start time and end time separated by a hyphen,
            with each time in the form hh:mm using the 24 hour clock.
    
            For example, for timers defining a morning and evening period
            during the week, and a daytime period at weekends,
            the message could look something like this:
    
            hvac.timer
             {
                zone=lounge
                timer=MoTuWeThFr,06:30-09:00,17:00-22:30
                timer=SaSu,08:00-23:00
             }
    
            If no timers have been set, then the message will contain
            the zone and a single timer= entry with nothing to the right
            of the equals sign.
            @param device : the name of the job (=device in xpl)
            timer.basic
               {
                action=start
                device=<name of the timer>, normally the zone id
                devicetype=hvac
                timer=MoTuWeThFr,06:30-09:00,17:00-22:30
                [timer=SaSu,08:00-23:00]
                [timer=...]
                [valueon1=comfort]
                [valueoff1=economy]
               }
            hvac.timer
               {
                zone=id
                timer=[SuMoTuWeThFrSa,hh:mm-hh:mm,hh:mm-hh:mm,...etc]
                [timer=]
               }
        
            """
    


The different actions
**********************

.. code-block:: json


    def stopJob(self, device):
            """
            Stop a device. It could be restarted via a
            resume command.
            @param device : the name of the timer
            
            timer.basic
            {
             action=stop
             device=<name of the timer>
            }
            """
    

.. code-block:: json


    def resumeJob(self, device):
            """
            Resume a previous stopped device
            @param device : the name of the timer
            
            timer.basic
            {
             action=resume
             device=<name of the timer>
            }
            """
    

.. code-block:: json


    def haltJob(self, device):
            """
            Stop a job and delete the device.
            @param device : the name of the timer
            """
            
            timer.basic
            {
             action=halt
             device=<name of the timer>
            }
    

.. code-block:: json


    def statusJob(self, device):
            """
            Retrieve the status of a device. If it does not
            exist, report it as halted
            @param device : the name of the timer
            """
            
            timer.basic
            {
             action=status
             device=<name of the timer>
            }
    


The nested message :
*********************

You must add the message that will be send in the start message of the device.
This is done by preceding the param name by nst-.
.. code-block:: json


    
               {
                nst-schema=The schema to use
                nst-type=The type of message to send
                parameter0=the name of the first parameter
                valueon0=value on for the first parameter
                valueoff0=value off for the first parameter
                ...
                nst_another=another fiel to include
               }

Parameters are transmitted using parameterx (0<=x<=3). The values that it can take are transmitted using valueonx and valueoff (0<=x<=3)

Storage engine
***************

Cron jobs are stored as ConfigParser files in the domogik data directory. If you want to edit them, you must stop the cron plugin before. Keep in mind that when you create a cron job, it will exist until you halt it.


Interface develoment
*********************

Specifications are `here|nocache <http://wiki.domogik.org/plugin\_cron\_interface>`_.