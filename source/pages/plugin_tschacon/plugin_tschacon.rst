****************
Tschacon Plugin
****************

Purpose
========


The aim of this plugin is to manage Chacon / DiO devices with a tellstick usb stick

Installation
=============

First of all you need to install the `telldus core software <http://developer.telldus.se/wiki/TellStick\_installation\_Linux>`_ on your server.

Once installed you should have the ''/dev/tellstick'' device on your system. You can see it typing :
.. code-block:: json


    ls -alh /dev/tellstick{CODE}Your device interface file's primary group is plugdev, so to be able to use it with domogik, add your domogik user to this group :
.. code-block:: json


    gpasswd -a domogik plugdev{CODE}(use sudo if needed)

You should now be ok to use your device 

Configuration / Pairing devices
================================

Configuration of the plugin is straight forward. Enable your plugin in your domogik installation with :
.. code-block:: json


    dmgenplug tschacon{CODE}
    and set autostart in the admin UI.
    
    Creating an appliance device
    *****************************
    
    
    In the administration panel, go to the ''Organization > Devices'' page. Create a new device like this :
    Name : Short name
    Description : Describe your device!
    Address : Module address, like "A1"
    Reference : only for information string
    Type : tschacon.switch
    Usage : Appliance
    
    Pairing devices
    ****************
    
    To pair your device with the address you will use in domogik, start adding a new device switch and choose an address for it (must be something like A1, as in the X10 protocole).
    Once done, put your chacon device into learning mode, then power on the device from the UI. Your device should flicker 2 times to tell you the code is learnt. This way, you can register up to 6 codes to each chacon device.