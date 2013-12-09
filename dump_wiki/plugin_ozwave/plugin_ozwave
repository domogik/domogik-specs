!OZWAVE plugin
{maketoc}

!!Purpose
Z-Wave is a wireless ecosystem that lets all your home electronics talk to each other, and to you, via remote control. This plugin allows to control zwave devices. 

It uses open source [http://code.google.com/p/open-zwave/|library openZwave c++ project|nocache] and py-openzwave as interfacing cython,
The Zwave network manager is directly integrated into the plugin

Simple action/sensor of devices have access via domogik devices (widgets).
Viewing and setting Zwave devices is accessed via a special plugin page from the admin panel.

Actualy only supported by domogik develop branch default.
Development is in progress, features will get gradually

!!Controller/devices Compatibility List   
Following interfaces are supported and verify with domogik:
* Aeon Labs Z-Stick Series 2  

Others controllers are supported by openzwave, [http://code.google.com/p/open-zwave/wiki/Controller_Compatibility_List| you can check here|nocache]

Following devices are supported :
* Everspring ST814
* Everspring (C.T.) HSM02
* Fibaro FGS211
* Fibaro FGS221

!Installation instructions
!!Prerequisite

Domogik ((Installation_for_developpers|developpers installation)) ~~#00C:(default branch)~~
You need to install python-openzwave :
((plugin_pyozw|python-openzwave))

!!Create an udev rules for controller
Currently, your PC controller is known as &quot;/dev/ttyUSBx&quot; (by default). This is not very convenient nor meaningful. We will then create a new udev rule that will create a link called &quot;/dev/zwave&quot; that will point to &quot;/dev/ttyUSBx&quot;.
!!!Gather information about your device controller (USB)
Use &quot;lsusb&quot; command for listing of USB devices, check before and after plug your USB controller.
{CODE()}
$ lsusb
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 005 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 006 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 007 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 008 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 009 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 005 Device 002: ID 0040:073d
Bus 004 Device 002: ID 10c4:ea60 Cygnal Integrated Products, Inc. CP210x Composite Device
Bus 004 Device 006: ID 0403:6001 Future Technology Devices International, Ltd FT232 USB-Serial (UART) IC
Bus 007 Device 002: ID 0b05:179c ASUSTek Computer, Inc.
{CODE}

Use &quot;ls /dev/ttyUSB*&quot; to check your num USB, check before and after plug your USB controller.
* Before
{CODE()}
$ ls /dev/ttyUSB*
/dev/ttyUSB2
{CODE}
* After USB plug
{CODE()}
$ ls /dev/ttyUSB*
/dev/ttyUSB0  /dev/ttyUSB2
{CODE}

Use &quot;udevadm&quot; command to gather information about your device :
{CODE()}
$ udevadm info  -a -n /dev/ttyUSB0

Udevadm info starts with the device specified by the devpath and then
walks up the chain of parent devices. It prints for every device
found, all possible attributes in the udev rules key format.
A rule to match, can be composed by the attributes of the device
and the attributes from one single parent device.

  looking at device '/devices/pci0000:00/0000:00:12.0/usb4/4-3/4-3:1.0/ttyUSB0/tty/ttyUSB0':
    KERNEL==&quot;ttyUSB0&quot;
    SUBSYSTEM==&quot;tty&quot;
    DRIVER==&quot;&quot;

  looking at parent device '/devices/pci0000:00/0000:00:12.0/usb4/4-3/4-3:1.0/ttyUSB0':
    KERNELS==&quot;ttyUSB0&quot;
    SUBSYSTEMS==&quot;usb-serial&quot;
    DRIVERS==&quot;cp210x&quot;
    ATTRS{port_number}==&quot;0&quot;

  looking at parent device '/devices/pci0000:00/0000:00:12.0/usb4/4-3/4-3:1.0':
    KERNELS==&quot;4-3:1.0&quot;
    SUBSYSTEMS==&quot;usb&quot;
    DRIVERS==&quot;cp210x&quot;
    ATTRS{bInterfaceNumber}==&quot;00&quot;
    ATTRS{bAlternateSetting}==&quot; 0&quot;
    ATTRS{bNumEndpoints}==&quot;02&quot;
    ATTRS{bInterfaceClass}==&quot;ff&quot;
    ATTRS{bInterfaceSubClass}==&quot;00&quot;
    ATTRS{bInterfaceProtocol}==&quot;00&quot;
    ATTRS{supports_autosuspend}==&quot;1&quot;
    ATTRS{interface}==&quot;CP2102 USB to UART Bridge Controller&quot;

  looking at parent device '/devices/pci0000:00/0000:00:12.0/usb4/4-3':
    KERNELS==&quot;4-3&quot;
    SUBSYSTEMS==&quot;usb&quot;
    DRIVERS==&quot;usb&quot;
    ATTRS{configuration}==&quot;&quot;
    ATTRS{bNumInterfaces}==&quot; 1&quot;
    ATTRS{bConfigurationValue}==&quot;1&quot;
    ATTRS{bmAttributes}==&quot;80&quot;
    ATTRS{bMaxPower}==&quot;100mA&quot;
    ATTRS{urbnum}==&quot;10835&quot;
    ATTRS{idVendor}==&quot;10c4&quot;
    ATTRS{idProduct}==&quot;ea60&quot;
    ATTRS{bcdDevice}==&quot;0100&quot;
    ATTRS{bDeviceClass}==&quot;00&quot;
    ATTRS{bDeviceSubClass}==&quot;00&quot;
    ATTRS{bDeviceProtocol}==&quot;00&quot;
    ATTRS{bNumConfigurations}==&quot;1&quot;
    ATTRS{bMaxPacketSize0}==&quot;64&quot;
    ATTRS{speed}==&quot;12&quot;
    ATTRS{busnum}==&quot;4&quot;
    ATTRS{devnum}==&quot;2&quot;
    ATTRS{devpath}==&quot;3&quot;
    ATTRS{version}==&quot; 1.10&quot;
    ATTRS{maxchild}==&quot;0&quot;
    ATTRS{quirks}==&quot;0x0&quot;
    ATTRS{avoid_reset_quirk}==&quot;0&quot;
    ATTRS{authorized}==&quot;1&quot;
    ATTRS{manufacturer}==&quot;Silicon Labs&quot;
    ATTRS{product}==&quot;CP2102 USB to UART Bridge Controller&quot;
    ATTRS{serial}==&quot;0001&quot;

  looking at parent device '/devices/pci0000:00/0000:00:12.0/usb4':
    KERNELS==&quot;usb4&quot;
    SUBSYSTEMS==&quot;usb&quot;
    DRIVERS==&quot;usb&quot;
    ATTRS{configuration}==&quot;&quot;
    ATTRS{bNumInterfaces}==&quot; 1&quot;
    ATTRS{bConfigurationValue}==&quot;1&quot;
    ATTRS{bmAttributes}==&quot;e0&quot;
    ATTRS{bMaxPower}==&quot;  0mA&quot;
    ATTRS{urbnum}==&quot;134&quot;
    ATTRS{idVendor}==&quot;1d6b&quot;
    ATTRS{idProduct}==&quot;0001&quot;
    ATTRS{bcdDevice}==&quot;0300&quot;
    ATTRS{bDeviceClass}==&quot;09&quot;
    ATTRS{bDeviceSubClass}==&quot;00&quot;
    ATTRS{bDeviceProtocol}==&quot;00&quot;
    ATTRS{bNumConfigurations}==&quot;1&quot;
    ATTRS{bMaxPacketSize0}==&quot;64&quot;
    ATTRS{speed}==&quot;12&quot;
    ATTRS{busnum}==&quot;4&quot;
    ATTRS{devnum}==&quot;1&quot;
    ATTRS{devpath}==&quot;0&quot;
    ATTRS{version}==&quot; 1.10&quot;
    ATTRS{maxchild}==&quot;5&quot;
    ATTRS{quirks}==&quot;0x0&quot;
    ATTRS{avoid_reset_quirk}==&quot;0&quot;
    ATTRS{authorized}==&quot;1&quot;
    ATTRS{manufacturer}==&quot;Linux 3.0.0-24-generic ohci_hcd&quot;
    ATTRS{product}==&quot;OHCI Host Controller&quot;
    ATTRS{serial}==&quot;0000:00:12.0&quot;
    ATTRS{authorized_default}==&quot;1&quot;

  looking at parent device '/devices/pci0000:00/0000:00:12.0':
    KERNELS==&quot;0000:00:12.0&quot;
    SUBSYSTEMS==&quot;pci&quot;
    DRIVERS==&quot;ohci_hcd&quot;
    ATTRS{vendor}==&quot;0x1002&quot;
    ATTRS{device}==&quot;0x4397&quot;
    ATTRS{subsystem_vendor}==&quot;0x1043&quot;
    ATTRS{subsystem_device}==&quot;0x8496&quot;
    ATTRS{class}==&quot;0x0c0310&quot;
    ATTRS{irq}==&quot;18&quot;
    ATTRS{local_cpus}==&quot;00000000,00000000,00000000,00000000,00000000,00000000,00000000,00000003&quot;
    ATTRS{local_cpulist}==&quot;0-1&quot;
    ATTRS{numa_node}==&quot;-1&quot;
    ATTRS{dma_mask_bits}==&quot;32&quot;
    ATTRS{consistent_dma_mask_bits}==&quot;32&quot;
    ATTRS{broken_parity_status}==&quot;0&quot;
    ATTRS{msi_bus}==&quot;&quot;

  looking at parent device '/devices/pci0000:00':
    KERNELS==&quot;pci0000:00&quot;
    SUBSYSTEMS==&quot;&quot;
    DRIVERS==&quot;&quot;

{CODE}
Those information will be useful to determinate for sure that this device is your Zwave controller. We will use several information, flagged above as &quot;DRIVERS&quot;, &quot;ATTRS{manufacturer}&quot; and &quot;ATTRS{product}&quot;. With that, we will be sure that we'll be talking to our controller. You can chose others attributs.
!!!Create rule.
*Create a new file, in folder &quot;/etc/udev/rules.d&quot;. Let's call it &quot;98-usbcp210x.rules&quot;. 
*Enter those information in the file : 
{CODE()}
# for z-Stick serie 2 to domogik /dev/zwave
DRIVERS==&quot;usb&quot;, ATTRS{manufacturer}==&quot;Silicon Labs&quot;, ATTRS{product}==&quot;CP2102 USB to UART Bridge Controller&quot;, SYMLINK+=&quot;zwave&quot;, MODE=&quot;0666&quot;
{CODE}
The &quot;DRIVERS&quot;, &quot;ATTRS{manufacturer}&quot;, &quot;ATTRS{product}&quot; values must be coherent with what you have found above.
*Ask udev to rediscover your device :
{CODE()}
# udevadm test $(udevadm info --query path --name ttyUSB0)
{CODE}
*Your device should now be re-discovered, let's confirm it :
{CODE()}
$ ls -l /dev/zwave
lrwxrwxrwx 1 root root 7 2012-08-27 00:46 /dev/zwave -&gt; ttyUSB0
{CODE}

!How to use plugin
!!Configure plugin
TODO : Images and comments.
{img fileId=338,stylebox=&quot;border&quot;,align=&quot;center&quot;}

!!Get Zwave network informations
TODO : Images and comments.
{img fileId=339,stylebox=&quot;border&quot;,align=&quot;center&quot;}
{img fileId=340,stylebox=&quot;border&quot;,align=&quot;center&quot;}

!!Configure domogik devices
TODO : Images and comments.

AdressTy : 'homename-1'.NodeId.instance
Example : ZWHome.5.1
{img fileId=341,stylebox=&quot;border&quot;,align=&quot;center&quot;}
{img fileId=342,stylebox=&quot;border&quot;,align=&quot;center&quot;}


!Developper notes

TODO : .....

!!Resources

* [http://code.google.com/p/open-zwave|An opensource project for zwave]
* [http://www.digiwave.dk/en/programming/an-introduction-to-the-z-wave-protocol|Introduction to zwave protocol]
* [http://www.digiwave.dk/en/programming/an-introduction-to-z-wave-programming-in-c|Introduction to zwave programming in C]
* [http://wiki.linuxmce.org/index.php/ZWave_API|Zwave API - LinuxMCE wiki]
* [http://z-wave.alsenet.com/index.php/Main_Page|Python development]