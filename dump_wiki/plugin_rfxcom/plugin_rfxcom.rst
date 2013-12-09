********************************
Plugin for the RFXCOM Usb Model
********************************
.. toctree::



Purpose
========
This plugin handle the `new RFXCOM Usb model <http://www.rfxcom.com/transceivers.htm#12103>`_.

{img attId="381",stylebox="border",align="center"}

In this page, it will be explainder how to :
#Know where you can find your Rfxcom in Linux
#Upgrade the firmware of the USB Rfxcom and use Rfxcom utilities
#Configure your device under Linux, in order to be use in Domogik
#Find a device/sensor

Know where the Rfxcom device is in Linux
=========================================
In Linux, a peripheral is usually available in "/dev" folder. Linux will create new files in order for you (and for the software) to communicate with the device.
In order to know where is the "device file" corresponding to your Rfxcom, plug your device in your computer, and issue a "dmesg" command as root.
You should see something similar to this :
.. code-block::
    
    # dmesg
    ....
    [67273.205914] usb 1-1.2: new full speed USB device number 6 using xhci_hcd
    [67273.234518] ftdi_sio 1-1.2:1.0: FTDI USB Serial Device converter detected
    [67273.234576] usb 1-1.2: Detected FT232RL
    [67273.234579] usb 1-1.2: Number of endpoints 2
    [67273.234582] usb 1-1.2: Endpoint 1 MaxPacketSize 64
    [67273.234584] usb 1-1.2: Endpoint 2 MaxPacketSize 64
    [67273.234587] usb 1-1.2: Setting MaxPacketSize 64
    [67273.240229] usb 1-1.2: FTDI USB Serial Device converter now attached to ttyUSB0
    

Yeah, I know, this is not very meaningful, but we'll cover that. You have an important information : the news device is "now attached to ttyUSB0". You can find the relevant file in "/dev/ttyUSB0".
In order to be sure that this is your rfxcom device, issue :
.. code-block::
    
    # udevadm info --query=all --name ttyUSB0
    P: /devices/pci0000:00/0000:00:06.0/usb4/4-4/4-4:1.0/ttyUSB0/tty/ttyUSB0
    N: ttyUSB0
    S: serial/by-id/usb-RFXCOM_RFXtrx433_03VGWYV5-if00-port0
    S: serial/by-path/pci-0000:00:06.0-usb-0:4:1.0-port0
    E: DEVLINKS=/dev/serial/by-id/usb-RFXCOM_RFXtrx433_03VGWYV5-if00-port0 /dev/seri                                                                                                                               al/by-path/pci-0000:00:06.0-usb-0:4:1.0-port0
    E: DEVNAME=/dev/ttyUSB0
    E: DEVPATH=/devices/pci0000:00/0000:00:06.0/usb4/4-4/4-4:1.0/ttyUSB0/tty/ttyUSB0
    E: ID_BUS=usb
    E: ID_MODEL=RFXtrx433
    E: ID_MODEL_ENC=RFXtrx433
    E: ID_MODEL_FROM_DATABASE=FT232 USB-Serial (UART) IC
    E: ID_MODEL_ID=6001
    E: ID_PATH=pci-0000:00:06.0-usb-0:4:1.0
    E: ID_PATH_TAG=pci-0000_00_06_0-usb-0_4_1_0
    E: ID_REVISION=0600
    E: ID_SERIAL=RFXCOM_RFXtrx433_03VGWYV5
    E: ID_SERIAL_SHORT=03VGWYV5
    E: ID_TYPE=generic
    E: ID_USB_DRIVER=ftdi_sio
    E: ID_USB_INTERFACES=:ffffff:
    E: ID_USB_INTERFACE_NUM=00
    E: ID_VENDOR=RFXCOM
    E: ID_VENDOR_ENC=RFXCOM
    E: ID_VENDOR_FROM_DATABASE=Future Technology Devices International, Ltd
    E: ID_VENDOR_ID=0403
    E: MAJOR=188
    E: MINOR=0
    E: SUBSYSTEM=tty
    E: UDEV_LOG=3
    E: USEC_INITIALIZED=82954257684
    

There some information here. Notice the ID_VENDOR and the ID_MODEL. That's indeed your Rfxcom !

Upgrade the firmware of the USB Rfxcom
=======================================
If you don't have the last firmware, don't hesitate to upgrade it. We will just cover the firmware upgrade under linux. Under Windows, it's pretty straigtforward, just follow the "Rfxcom user guide" located `here <http://www.rfxcom.com/downloads.htm>`_
Install Mono 
**************
First of all, you need to install "mono", in order to be able to use Rfxcom's firmware update or the Rfxcom manager.
RFXCOM utilities can be run with __mono__ under GNU/Linux. To install "mono" on Debian :
.. code-block::
    
    # apt-get install mono-runtime
    # apt-get install libmono-microsoft-visualbasic8.0-cil
    

Upload a new firmware
**********************
!!!!Download the last firmware
Download the last firware for your hardware, `on this page <http://www.rfxcom.com/downloads.htm>`_
.. code-block::
    
    # wget http://www.rfxcom.com/documents/RFXtrx433_firmware.zip
    # unzip RFXtrx433_firmware.zip
    

You will have a ".hex" file unzipped from the archive.
!!!!Launch the utility 
Download \_\_RFXflash.exe\_\_ on `the official RFXCOM website <http://www.rfxcom.com/documents/RFXflash.zip>`_.
Launch __RFXflash.exe : 
.. code-block::
    
    $ mono RFXflash.exe
    

!!!!Upload firmware
We have see in the previous section that your device should be recognised as "/dev/ttyUSB0" (or something similar). Select it now.
Click on the icon ''Connect to device''. You should read now : 
.. code-block::
    
    Connecting...
    
    Device found...
    


{img attId="382",stylebox="border",align="center"}

Click on the icon ''Open HEX File''. 

{img attId="383",stylebox="border",align="center"}

Select the firmware. Click on ''Open''.

{img attId="384",stylebox="border",align="center"}

You should read now : 
.. code-block::
    
    HEX file imported...
    


{img attId="385",stylebox="border",align="center"}

Click on the icon ''Write Device''. You should read now : 
.. code-block::
    
    Erasing...
    Erasing: 13A00
    
    Finished operation...
    Not connected...
    Connecting...
    Device found...
    Erase step finished...
    Start Writing Program memory
    
    Finished operation...
    


{img attId="386",stylebox="border",align="center"}

Now, click on the icon ''Normal execution mode to end the flash process''. You RFXCOM is upgraded with a new firmware.

{img attId="387",stylebox="border",align="center"}

Configure your device under Linux, in order to be use in Domogik
=================================================================
In this section, we will do two things :
*Create a udev rule to map your Rfxcom to a meaningful "device file".
*Allow domogik user to talk to your Rfxcom
Create a udev rule for the Rfxcom.
***********************************
Currently, your Rfxcom is known as "/dev/ttyUSB0" (by default). This is not very convenient nor meaningful. We will then create a new udev rule that will create a link called "/dev/rfxcom" that will point to "/dev/ttyUSB0".
!!!!Gather information about your device
Use "udevadm" command to gather information about your device :
.. code-block::
    
    # udevadm info --query=all --name ttyUSB0
    P: /devices/pci0000:00/0000:00:06.0/usb4/4-4/4-4:1.0/ttyUSB0/tty/ttyUSB0
    N: ttyUSB0
    S: serial/by-id/usb-RFXCOM_RFXtrx433_03VGWYV5-if00-port0
    S: serial/by-path/pci-0000:00:06.0-usb-0:4:1.0-port0
    E: DEVLINKS=/dev/serial/by-id/usb-RFXCOM_RFXtrx433_03VGWYV5-if00-port0 /dev/seri                                                                                                                               al/by-path/pci-0000:00:06.0-usb-0:4:1.0-port0
    E: DEVNAME=/dev/ttyUSB0
    E: DEVPATH=/devices/pci0000:00/0000:00:06.0/usb4/4-4/4-4:1.0/ttyUSB0/tty/ttyUSB0
    E: ID_BUS=usb
    E: ID_MODEL=RFXtrx433
    E: ID_MODEL_ENC=RFXtrx433
    E: ID_MODEL_FROM_DATABASE=FT232 USB-Serial (UART) IC
    E: ID_MODEL_ID=6001
    E: ID_PATH=pci-0000:00:06.0-usb-0:4:1.0
    E: ID_PATH_TAG=pci-0000_00_06_0-usb-0_4_1_0
    E: ID_REVISION=0600
    E: ID_SERIAL=RFXCOM_RFXtrx433_03VGWYV5
    E: ID_SERIAL_SHORT=03VGWYV5
    E: ID_TYPE=generic
    E: ID_USB_DRIVER=ftdi_sio
    E: ID_USB_INTERFACES=:ffffff:
    E: ID_USB_INTERFACE_NUM=00
    E: ID_VENDOR=RFXCOM
    E: ID_VENDOR_ENC=RFXCOM
    E: ID_VENDOR_FROM_DATABASE=Future Technology Devices International, Ltd
    E: ID_VENDOR_ID=0403
    E: MAJOR=188
    E: MINOR=0
    E: SUBSYSTEM=tty
    E: UDEV_LOG=3
    E: USEC_INITIALIZED=82954257684
    

Those information will be useful to determinate for sure that this device is your Rfxcom. We will use several information, flagged above as "SUBSYSTEM", "ID_VENDOR" and "ID_MODEL". With that, we will be sure that we'll be talking to our Rfxcom.
!!!!Create a udev rule.
*Create a new file, in folder "/etc/udev/rules.d". Let's call it "71-rfxcom.rules".
*Enter those information in the file :
.. code-block::
    
    SUBSYSTEM=="tty", ENV{ID_MODEL}=="RFXtrx433", ENV{ID_VENDOR}=="RFXCOM", SYMLINK+="rfxcom",  MODE="0666"
    

The "SUBSYSTEM", the "ENV{ID_MODEL}" and "ENV{ID_VENDOR}" values must be coherent with what you have found above.
*Ask udev to rediscover your device :
.. code-block::
    
    # udevadm test $(udevadm info --query path --name ttyUSB0)
    

Your device should now be re-discovered, let's confirm it :
.. code-block::
    
    # ls -l /dev/rfxcom
    lrwxrwxrwx 1 root root 7 juin  18 23:24 /dev/rfxcom -> ttyUSB0
    

Allow domogik to use the Rfxcom.
*********************************
Now that the Rfxcom is know "/dev/rfxcom" by the system, let's allow Domogik to use it.
At this point, you should have installed at least Domogik. Normally, the setup should have asked for the creation of a user (by default, it's called "domogik").
Now, we must allow the "domogik" user to talk to the Rfxcom.
The Rfxcom device file have some specific rights : "root" is the owner, but "dialout" is the group. This group is used to allow users to use "modem"-type devices, and the Rfxcom is being discovered as one of this type by the system. The only thing we have to do is to add "domogik" to the group "dialout".
.. code-block::
    
    # adduser domogik dialout
    

That's all, "domogik" will be able to use the Rfxcom, thanks to the "group" rights (read and write)
.. code-block::
    
    # ls -l /dev/ttyUSB0 
    crw-rw---T 1 root dialout 188, 0 juin  18 23:24 /dev/ttyUSB0
    


How to find a device address for a sensor
==========================================
You can launch the __dump_xpl.py__ tool to see all xpl messages and try to catch the on
.. code-block::
    
    $ ./dump_xpl.py -f
    2011-07-24 11:56:08.590840 - xpl-trig
    {
    hop=1
    source=rfxcom-lan.0004a31bb6ac
    target=*
    }
    sensor.basic
    {
    device=th2 0x5803
    type=temp
    current=21.8
    units=c
    }
    



Usb model known features
=========================
Unit code forced to 1 with Homeasy products with a program/learn button
************************************************************************
Actually Domogik can't handle addresses split in 2 parts. So, the unit code is for the moment forced to "1" for all these devices in Domogik. 
So, the remote command of this `this kind of product <http://www.planete-domotique.com/autres/par-technologie/chacon-sans-fils/telecommande-3-canaux-3-modules-prise-on-off-2300w-di-o.html>`_ can be use only for 1 plug if you set all the three plugs on unit 1.

This issue will be fixed with Domogik next database model.

Address formats
================
{FANCYTABLE(head=>Device type~|~Description~|~Address format)}
x10.basic - X10 lighting~|~X10 lighting or ARC messages.~|~(house code(device code)) house code = A to P device code = 1 to 16. Device code is not present in case of all_lights_on/off.
ac.basic – AC code remotes and wall switches~|~AC type remotes or AC type RF wall switches (with program/learn button)~|~(0x1-0x3ffffff) The address used by the AC device. In the RF protocol this is a 26bit value, which should be specified as a hexadecimal number with a leading 0x. Never use an address with all zeroes!
x10.security~|~Visonic PowerCode/CodeSecure security or Chacon, Avidsen, NEXA smoke detector~|~(device id) The id is a hex number between 0x0 and 0xffffff. It is also referred to as the device address.
remote.basic~|~PC Remote, Medion remote, ATI Remote or ATI Remote Plus~|~(rf|ati|medion|ati_plus) pc is an X10 PC Remote, address is only used at cursor commands. ati is an ATI remote. medion is for the medion remote. ati_plus is an ATI-Plus remote. Address is the remote hex channel from 0x0 to 0xF.
Digimax~|~~|~(digimax 0x(hex device id))
RFXSensor~|~~|~(rfxsensor 0x(hex device id))
RFXMeter~|~~|~(rfxmeter 0x(hex device id))
sensor.basic – RFXLAN I/O lines~|~~|~(io0-io7) IO line to control
sensor.basic – Mertik-Maxitrol~|~~|~(0x0-0xF) mertik address is a hex code 0x0 to 0xF
Oregon sensors~|~Temperature, Temp-Hygro, Rain Gauge, Anemometer, UV sensor, Body Weight Monitor, Ampere meter, Power meter~|~(temp1-4|th1-6|thb1-2|rain1-2|wind1-3|uv1-2|weight1-2|elec1-3) 0x(hex sensor id)
{FANCYTABLE}


Links
======
*`http://www.rfxcom.com/downloads.htm <http://www.rfxcom.com/downloads.htm>`_
*`Latest xPL firmware for the RFXLAN <http://www.rfxcom.com/documents/xPL.zip>`_
*`RFXxPL xPL implementation on RFXLAN documentation <http://www.rfxcom.com/documents/RFXCOM%20implementation%20xPL.pdf>`_

****************
Developer notes
****************
xPL
====
All xpl messages are make in `the same way the RFXCOM Lan xPL generates them <http://www.rfxcom.com/documents/RFXCOM%20implementation%20xPL.pdf>`_.

Set up addresses and examples
==============================
DI.O PDR-2300
**************
!!!!Delete learned addresses
Plug the module.
Call this command before the led stop blinking : ./send.py xpl-cmnd ac.basic "address=0x1,unit=1,__command=group_off__"
The plugged light should blink twice for acknowlegment.
!!!!Learn a new address
Plug the module.
Call this command before the led stop blinking : ./send.py xpl-cmnd ac.basic "__address=0x111__,unit=1,__command=on__"
The plugged light should blink twice for acknowlegment.

Chacon 54561, 54565, 54566, 54567, 54581, 54582, 54585, 54585
**************************************************************
!!!!Delete learned addresses
Plug the module. Press the button until the led blinks (about 6 seconds). Press the button one more time. The plugged light should blink twice for acknowlegment.

!!!!Learn a new address
Plug the module. Press the button. Call this command before the led stop blinking : ./send.py xpl-cmnd ac.basic "__address=0x111__,unit=1,__command=on__"
The plugged light should blink twice for acknowlegment.

!!!!Play with the light
.. code-block::
    
    $ ./send.py xpl-cmnd ac.basic "address=0x0038abfe,unit=10,command=off"
    $ ./send.py xpl-cmnd ac.basic "address=0x0038abfe,unit=10,command=on"
    $ ./send.py xpl-cmnd ac.basic "address=0x0038abfe,unit=10,command=preset,level=1"
    



*****
List
*****
{FANCYTABLE(head=>Type | Subtype    | Description                                                            | status         | Remarks)}
Lighting1           | x10           | X10 lighting devices                                                   | Dev(x) Test( ) | "All off" and "All on" are implemented but xml and features not activated
                    | arc           | ARC is the protocol used by different brands with units having code wheels A-P/1-16: KlikAanKlikUit, NEXA, CHACON, HomeEasy, Proove, DomiaLite | Dev(x) Test( ) | 
                    | elro          | ELRO AB400D                                                            | Dev(x) Test( ) | ..
                    | waveman       | Waveman                                                                | Dev(x) Test( ) | ..
                    | chacon        | Chacon EMW200                                                          | Dev(x) Test( ) | ..
                    | impuls        | Impuls                                                                 | Dev(x) Test( ) | ..
Lighting2           | ac            | AC is the protocol used by different brands with units having a learning mode button: KlikAanKlikUit, NEXA, CHACON, HomeEasy UK | Dev(x) Test( ) |\\Unit code is restricted to "1" with Domogik actual database model.<br/> Group command is implemented but xml and features not activated.
                    | homeeasy_eu   | Homeeasy EU                                                            | Dev(x) Test( ) 
Lighting3           | koppla        | Ikea Koppla                                                            | Dev(x) Test( ) |
Lighting4           | pt2262        | PT2262 - futur use                                                     | Dev( ) Test( ) |
Lighting5           | lightwaverf   | LightwaveRF Siemens - futur use                                        | Dev( ) Test( ) |
Lighting6           | novatys       | Novatys - futur use                                                    | Dev( ) Test( ) |
Curtain1            | harrison      | Harrison curtains                                                      | Dev(x) Test( ) | "on" open curtains, "off" close, "dim" or "bright" stop and "all_light_*" set program mode

{FANCYTABLE}
