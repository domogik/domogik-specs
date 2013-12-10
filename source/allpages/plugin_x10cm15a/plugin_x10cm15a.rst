.. toctree::



********
Purpose
********

X10 is an automation technology which allows to switch and dim lights, control appliances, etc. This plugin allows to control X10 devices if you got a __CM15A__ / __CM15PRO__ adaptator. If you want to use another adaptator, check if there are available plugins for these adaptators.

************
How to plug
************

/!\change cm15 pic
{img fileId="185" thumb="y" alt="" rel="box[g]"} {img fileId="184" thumb="y" alt="" rel="box[g]"}

On the left the CM15A module which is used to send commands to all x10 plugged in modules.
On the right a LM12 module used to control a lamp.
******
cm15a
******

This plugin uses the linux driver to use CM15 adaptator. So, you will first need to install the driver.

Installation
=============

More information can be find `here <http://www.linuxha.com/USB/cm15a.html>`_
If already plugged, deplug cm15 module, and get `iplc-driver.tgz <http://www.linuxha.com/common/iplcd/iplc-driver.tgz>`_
.. code-block:: json


    
    tar zxvf iplc-driver.tgz
    
    ln -s /usr/src/linux-headers-$(uname -r)/include/generated/autoconf.h /usr/src/linux-headers-$(uname -r)/include/linux/autoconf.h
    
    cd iplc/driver/linux-2.6/cm15a.d # or Linux 2.4 if you need support for 2.4
    make
    sudo insmod cm15a.ko # You need to be root
    ls -l /dev/cm15a*
    


If you want to give the rights to the domogik user, you can create /etc/udev/rules.d/98-cm15a.rules, and add : 
.. code-block:: json


    
    KERNEL=="cm15a0", BUS=="usb", SYSFS{idVendor}=="0bc7", SYSFS{idProduct}=="0001", NAME="cm15a0", OWNER="domogik"
    


Then, deplug/plug in your CM15 device. You should have a /dev/cm15 link created :
.. code-block:: json


    
    # ls -l /dev/cm15a0
    lrw------- 1 domogik domogik 7 2010-07-19 09:50 /dev/cm15a0
    


Note that "cm15a0" may change on your installation.



Try using an appliance
***********************

Plug in an appliance device (using A1 code for example) and run :
.. code-block:: json


    
    echo sur /dev/cm15a0 ?
    

The appliance should switch on. Now run :
.. code-block:: json


    
    echo sur /dev/cm15a0 ?
    

The appliance should switch off.

Try using a lamp 
******************

Plug in a lamp device (using A2 code for example) and run :
.. code-block:: json


    
    echo sur /dev/cm15a0 ?
    

The lamp should switch on. Now, run (one or more times) :
.. code-block:: json


    
    echo sur /dev/cm15a0 ?
    

This command lowers brightness of 10 units each time you call it. So, your lamp intensity should decrease. Now, run : 
.. code-block:: json


    
    echo sur /dev/cm15a0 ?
    

This command increases brightness of 10 units each time you call it. So, your lamp intensity should increase.

*********************
Plugin configuration
*********************

Enabling plugin
================

You can enable plugin by using (from your domogik directory) :
.. code-block:: json


    
    dmgenplug x10cm15a
    


You just have to reload administration page to see the plugin in the list.

Configuration
==============

In Domogik administration, go to x10_cm15a configuration page.

cm15a-cfg-path
***************

Path to cm15a config file
Default : /dev/cm15a0
The default value (/dev/cm15a0) should be fine. When set don't forget to save it!

Start plugin
=============

You can now start the plugin (start button).

*********************
Creating x10 devices
*********************

Creating a lamp device
=======================

In administration, go to __Organization > Devices__ page. Create a new device like this :
* Name : Short name, like "Hall"
* Description : Device details, like "Hall light"
* Address : X10 address, like "A4"
* Reference : X10 module's model, only for information, like "LM12"
* Type : 
** X10.switch (provides only on/off)
** X10.dimmer (provides on/off and dim/bright)
* Usage : Light

Example : 

.. image:: ../../_static/images/194

((Setup_your_devices|Attribute the features to a place and you can now control your lamp)).

Creating an appliance device
=============================

In administration, go to __Organization > Devices__ page. Create a new device like this :
* Name : Short name, like "Coffee machine"
* Description : Describe your coffee machine if you want!
* Address : X10 address, like "A3"
* Reference : X10 module's model, only for information, like "AM12"
* Type : X10.switch
* Usage : Appliance

((Setup_your_devices|Attribute the features to a place and you can now control your appliance)).

*****************
Developper Notes
*****************


xPL schema
===========

The `x10.basic <http://xplproject.org.uk/wiki/index.php?title=Schema\_-\_X10.BASIC>`_ schema is used.

/command
=========

.. code-block:: json


    
    /command/x10/<address>/on # switch on the lamp / appliance
    /command/x10/<address>/off # switch off the lamp / appliance
    

''Only for lamps'' 
.. code-block:: json


    
    /command/x10/<address>/dim/<value> # dim units by <level> (1-22) (decrease brightness)
    /command/x10/<address>/bright/<value> # brighten units by <level> (1-22) (increase brightness)
    

Note that these values are relative.