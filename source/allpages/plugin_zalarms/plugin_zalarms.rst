A quick and dirty plugin to test the cron plugin.
You can create alarms and dawnalarms.

Prerequisites
==============

Install the `cron <http://wiki.domogik.org/plugin\_zalarms>`_ plugin and start it.

Install the plugin
===================

This plugin is available in the development sources. Follow this `documentation|nocache <http://wiki.domogik.org/Developers\_installation>`_ to install them.
Enable the plugin :
__sudo dmgenplug -f zalarms__

Configure and start the zalarms plugin
=======================================

Add all the alarms you want using the configuration page of the plugin. And start it.
All events are sent when the plugin starts. So you can stop it now.
The jobs you have created are now stored (permanently) in the cron plugin store. If you want to delete them, look at the `cron <http://wiki.domogik.org/plugin\_zalarms>`_ plugin.

No words, just some examples :
First case of use
******************

I want to start my "christmas" tree at 7:00 every morning and stop it at 8:00. In the evening, I want to start it at 17:00 and stop it at 21:00. In the weekend, start it at 10:00 and stop it at 21:00.
I want to send an on (off) command using the xpl-cmnd type, according to the telldus.basic schema to device TS14.
.. image:: ../../_static/images/326

Second case of use
*******************

Want to be waked up by the dawn the morning. So use the dawnalarm with a dimmer.
I want to be waked up a 8:00 every saturday and sunday morning. The dawn process must start a 7:00 and use the following levels : 10,20,40,60,80,100. 
The light will start at 7:00 with a level of 10%, and 12 minutes later (60 minutes / (6-1)) the ligth will goes to level 20%. And so on.
At 8:00, the ligth will be 100%.
Here is the value to put in the alarm1 configuration zone : SaSu,07:00-08:00,10,20,40,60,80,100
Actually, your device must use the dim command and the level parameter.
.. image:: ../../_static/images/327

Third case of use with plcbus
******************************

Want to shut off all the lights of the home at 0h00 from sunday to thursday and at 1h00 friday and saturday.
.. image:: ../../_static/images/336
Now add a device in Domogik (technology cron / job) and give homeOff as address.
The last thing to do is to add widgets. Look at the `cron <http://wiki.domogik.org/plugin\_zalarms>`_ documentation.