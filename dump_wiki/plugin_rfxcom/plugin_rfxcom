!Plugin for the RFXCOM Usb Model
{maketoc}

!!Purpose
This plugin handle the [http://www.rfxcom.com/transceivers.htm#12103|new RFXCOM Usb model].

{img attId=&quot;381&quot;,stylebox=&quot;border&quot;,align=&quot;center&quot;}

In this page, it will be explainder how to :
#Know where you can find your Rfxcom in Linux
#Upgrade the firmware of the USB Rfxcom and use Rfxcom utilities
#Configure your device under Linux, in order to be use in Domogik
#Find a device/sensor

!!Know where the Rfxcom device is in Linux
In Linux, a peripheral is usually available in &quot;/dev&quot; folder. Linux will create new files in order for you (and for the software) to communicate with the device.
In order to know where is the &quot;device file&quot; corresponding to your Rfxcom, plug your device in your computer, and issue a &quot;dmesg&quot; command as root.
You should see something similar to this :
{CODE()}
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
{CODE}
Yeah, I know, this is not very meaningful, but we'll cover that. You have an important information : the news device is &quot;now attached to ttyUSB0&quot;. You can find the relevant file in &quot;/dev/ttyUSB0&quot;.
In order to be sure that this is your rfxcom device, issue :
{CODE()}
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
{CODE}
There some information here. Notice the ID_VENDOR and the ID_MODEL. That's indeed your Rfxcom !

!!Upgrade the firmware of the USB Rfxcom
If you don't have the last firmware, don't hesitate to upgrade it. We will just cover the firmware upgrade under linux. Under Windows, it's pretty straigtforward, just follow the &quot;Rfxcom user guide&quot; located [http://www.rfxcom.com/downloads.htm|here]
!!!Install Mono 
First of all, you need to install &quot;mono&quot;, in order to be able to use Rfxcom's firmware update or the Rfxcom manager.
RFXCOM utilities can be run with __mono__ under GNU/Linux. To install &quot;mono&quot; on Debian :
{CODE()}
# apt-get install mono-runtime
# apt-get install libmono-microsoft-visualbasic8.0-cil
{CODE}
!!!Upload a new firmware
!!!!Download the last firmware
Download the last firware for your hardware, [http://www.rfxcom.com/downloads.htm|on this page]
{CODE()}
# wget http://www.rfxcom.com/documents/RFXtrx433_firmware.zip
# unzip RFXtrx433_firmware.zip
{CODE}
You will have a &quot;.hex&quot; file unzipped from the archive.
!!!!Launch the utility 
Download __RFXflash.exe__ on [http://www.rfxcom.com/documents/RFXflash.zip|the official RFXCOM website].
Launch __RFXflash.exe : 
{CODE()}
$ mono RFXflash.exe
{CODE}
!!!!Upload firmware
We have see in the previous section that your device should be recognised as &quot;/dev/ttyUSB0&quot; (or something similar). Select it now.
Click on the icon ''Connect to device''. You should read now : 
{CODE()}
Connecting...

Device found...
{CODE}

{img attId=&quot;382&quot;,stylebox=&quot;border&quot;,align=&quot;center&quot;}

Click on the icon ''Open HEX File''. 

{img attId=&quot;383&quot;,stylebox=&quot;border&quot;,align=&quot;center&quot;}

Select the firmware. Click on ''Open''.

{img attId=&quot;384&quot;,stylebox=&quot;border&quot;,align=&quot;center&quot;}

You should read now : 
{CODE()}
HEX file imported...
{CODE}

{img attId=&quot;385&quot;,stylebox=&quot;border&quot;,align=&quot;center&quot;}

Click on the icon ''Write Device''. You should read now : 
{CODE()}
Erasing...
Erasing: 13A00

Finished operation...
Not connected...
Connecting...
Device found...
Erase step finished...
Start Writing Program memory

Finished operation...
{CODE}

{img attId=&quot;386&quot;,stylebox=&quot;border&quot;,align=&quot;center&quot;}

Now, click on the icon ''Normal execution mode to end the flash process''. You RFXCOM is upgraded with a new firmware.

{img attId=&quot;387&quot;,stylebox=&quot;border&quot;,align=&quot;center&quot;}

!!Configure your device under Linux, in order to be use in Domogik
In this section, we will do two things :
*Create a udev rule to map your Rfxcom to a meaningful &quot;device file&quot;.
*Allow domogik user to talk to your Rfxcom
!!!Create a udev rule for the Rfxcom.
Currently, your Rfxcom is known as &quot;/dev/ttyUSB0&quot; (by default). This is not very convenient nor meaningful. We will then create a new udev rule that will create a link called &quot;/dev/rfxcom&quot; that will point to &quot;/dev/ttyUSB0&quot;.
!!!!Gather information about your device
Use &quot;udevadm&quot; command to gather information about your device :
{CODE()}
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
{CODE}
Those information will be useful to determinate for sure that this device is your Rfxcom. We will use several information, flagged above as &quot;SUBSYSTEM&quot;, &quot;ID_VENDOR&quot; and &quot;ID_MODEL&quot;. With that, we will be sure that we'll be talking to our Rfxcom.
!!!!Create a udev rule.
*Create a new file, in folder &quot;/etc/udev/rules.d&quot;. Let's call it &quot;71-rfxcom.rules&quot;.
*Enter those information in the file :
{CODE()}
SUBSYSTEM==&quot;tty&quot;, ENV{ID_MODEL}==&quot;RFXtrx433&quot;, ENV{ID_VENDOR}==&quot;RFXCOM&quot;, SYMLINK+=&quot;rfxcom&quot;,  MODE=&quot;0666&quot;
{CODE}
The &quot;SUBSYSTEM&quot;, the &quot;ENV{ID_MODEL}&quot; and &quot;ENV{ID_VENDOR}&quot; values must be coherent with what you have found above.
*Ask udev to rediscover your device :
{CODE()}
# udevadm test $(udevadm info --query path --name ttyUSB0)
{CODE}
Your device should now be re-discovered, let's confirm it :
{CODE()}
# ls -l /dev/rfxcom
lrwxrwxrwx 1 root root 7 juin  18 23:24 /dev/rfxcom -&gt; ttyUSB0
{CODE}
!!!Allow domogik to use the Rfxcom.
Now that the Rfxcom is know &quot;/dev/rfxcom&quot; by the system, let's allow Domogik to use it.
At this point, you should have installed at least Domogik. Normally, the setup should have asked for the creation of a user (by default, it's called &quot;domogik&quot;).
Now, we must allow the &quot;domogik&quot; user to talk to the Rfxcom.
The Rfxcom device file have some specific rights : &quot;root&quot; is the owner, but &quot;dialout&quot; is the group. This group is used to allow users to use &quot;modem&quot;-type devices, and the Rfxcom is being discovered as one of this type by the system. The only thing we have to do is to add &quot;domogik&quot; to the group &quot;dialout&quot;.
{CODE()}
# adduser domogik dialout
{CODE}
That's all, &quot;domogik&quot; will be able to use the Rfxcom, thanks to the &quot;group&quot; rights (read and write)
{CODE()}
# ls -l /dev/ttyUSB0 
crw-rw---T 1 root dialout 188, 0 juin  18 23:24 /dev/ttyUSB0
{CODE}

!!How to find a device address for a sensor
You can launch the __dump_xpl.py__ tool to see all xpl messages and try to catch the on
{CODE()}
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
{CODE}


!!Usb model known features
!!!Unit code forced to 1 with Homeasy products with a program/learn button
Actually Domogik can't handle addresses split in 2 parts. So, the unit code is for the moment forced to &quot;1&quot; for all these devices in Domogik. 
So, the remote command of this [http://www.planete-domotique.com/autres/par-technologie/chacon-sans-fils/telecommande-3-canaux-3-modules-prise-on-off-2300w-di-o.html|this kind of product] can be use only for 1 plug if you set all the three plugs on unit 1.

This issue will be fixed with Domogik next database model.

!!Address formats
{FANCYTABLE(head=&gt;Device type~|~Description~|~Address format)}
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


!!Links
*[http://www.rfxcom.com/downloads.htm|http://www.rfxcom.com/downloads.htm]
*[http://www.rfxcom.com/documents/xPL.zip|Latest xPL firmware for the RFXLAN]
*[http://www.rfxcom.com/documents/RFXCOM%20implementation%20xPL.pdf|RFXxPL xPL implementation on RFXLAN documentation]

!Developer notes
!!xPL
All xpl messages are make in [http://www.rfxcom.com/documents/RFXCOM%20implementation%20xPL.pdf|the same way the RFXCOM Lan xPL generates them].

!!Set up addresses and examples
!!!DI.O PDR-2300
!!!!Delete learned addresses
Plug the module.
Call this command before the led stop blinking : ./send.py xpl-cmnd ac.basic &quot;address=0x1,unit=1,__command=group_off__&quot;
The plugged light should blink twice for acknowlegment.
!!!!Learn a new address
Plug the module.
Call this command before the led stop blinking : ./send.py xpl-cmnd ac.basic &quot;__address=0x111__,unit=1,__command=on__&quot;
The plugged light should blink twice for acknowlegment.

!!!Chacon 54561, 54565, 54566, 54567, 54581, 54582, 54585, 54585
!!!!Delete learned addresses
Plug the module. Press the button until the led blinks (about 6 seconds). Press the button one more time. The plugged light should blink twice for acknowlegment.

!!!!Learn a new address
Plug the module. Press the button. Call this command before the led stop blinking : ./send.py xpl-cmnd ac.basic &quot;__address=0x111__,unit=1,__command=on__&quot;
The plugged light should blink twice for acknowlegment.

!!!!Play with the light
{CODE()}
$ ./send.py xpl-cmnd ac.basic &quot;address=0x0038abfe,unit=10,command=off&quot;
$ ./send.py xpl-cmnd ac.basic &quot;address=0x0038abfe,unit=10,command=on&quot;
$ ./send.py xpl-cmnd ac.basic &quot;address=0x0038abfe,unit=10,command=preset,level=1&quot;
{CODE}


!List
{FANCYTABLE(head=&gt;Type | Subtype    | Description                                                            | status         | Remarks)}
Lighting1           | x10           | X10 lighting devices                                                   | Dev(x) Test( ) | &quot;All off&quot; and &quot;All on&quot; are implemented but xml and features not activated
                    | arc           | ARC is the protocol used by different brands with units having code wheels A-P/1-16: KlikAanKlikUit, NEXA, CHACON, HomeEasy, Proove, DomiaLite | Dev(x) Test( ) | 
                    | elro          | ELRO AB400D                                                            | Dev(x) Test( ) | ..
                    | waveman       | Waveman                                                                | Dev(x) Test( ) | ..
                    | chacon        | Chacon EMW200                                                          | Dev(x) Test( ) | ..
                    | impuls        | Impuls                                                                 | Dev(x) Test( ) | ..
Lighting2           | ac            | AC is the protocol used by different brands with units having a learning mode button: KlikAanKlikUit, NEXA, CHACON, HomeEasy UK | Dev(x) Test( ) |\\Unit code is restricted to &quot;1&quot; with Domogik actual database model.&lt;br/&gt; Group command is implemented but xml and features not activated.
                    | homeeasy_eu   | Homeeasy EU                                                            | Dev(x) Test( ) 
Lighting3           | koppla        | Ikea Koppla                                                            | Dev(x) Test( ) |
Lighting4           | pt2262        | PT2262 - futur use                                                     | Dev( ) Test( ) |
Lighting5           | lightwaverf   | LightwaveRF Siemens - futur use                                        | Dev( ) Test( ) |
Lighting6           | novatys       | Novatys - futur use                                                    | Dev( ) Test( ) |
Curtain1            | harrison      | Harrison curtains                                                      | Dev(x) Test( ) | &quot;on&quot; open curtains, &quot;off&quot; close, &quot;dim&quot; or &quot;bright&quot; stop and &quot;all_light_*&quot; set program mode

{FANCYTABLE}
