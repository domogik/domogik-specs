**************
OZWAVE plugin
**************
.. toctree::



Purpose
========
Z-Wave is a wireless ecosystem that lets all your home electronics talk to each other, and to you, via remote control. This plugin allows to control zwave devices. 

It uses open source `library openZwave c++ project|nocache <http://code.google.com/p/open-zwave/>`_ and py-openzwave as interfacing cython,
The Zwave network manager is directly integrated into the plugin

Simple action/sensor of devices have access via domogik devices (widgets).
Viewing and setting Zwave devices is accessed via a special plugin page from the admin panel.

Actualy only supported by domogik develop branch default.
Development is in progress, features will get gradually

Controller/devices Compatibility List   
=========================================
Following interfaces are supported and verify with domogik:
* Aeon Labs Z-Stick Series 2  

Others controllers are supported by openzwave, ` you can check here|nocache <http://code.google.com/p/open-zwave/wiki/Controller\_Compatibility\_List>`_

Following devices are supported :
* Everspring ST814
* Everspring (C.T.) HSM02
* Fibaro FGS211
* Fibaro FGS221

**************************
Installation instructions
**************************
Prerequisite
=============

Domogik ((Installation_for_developpers|developpers installation)) ~~#00C:(default branch)~~
You need to install python-openzwave :
((plugin_pyozw|python-openzwave))

Create an udev rules for controller
====================================
Currently, your PC controller is known as "/dev/ttyUSBx" (by default). This is not very convenient nor meaningful. We will then create a new udev rule that will create a link called "/dev/zwave" that will point to "/dev/ttyUSBx".
Gather information about your device controller (USB)
******************************************************
Use "lsusb" command for listing of USB devices, check before and after plug your USB controller.
.. code-block::
    
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
    


Use "ls /dev/ttyUSB*" to check your num USB, check before and after plug your USB controller.
* Before
.. code-block::
    
    $ ls /dev/ttyUSB*
    /dev/ttyUSB2
    

* After USB plug
.. code-block::
    
    $ ls /dev/ttyUSB*
    /dev/ttyUSB0  /dev/ttyUSB2
    


Use "udevadm" command to gather information about your device :
.. code-block::
    
    $ udevadm info  -a -n /dev/ttyUSB0
    
    Udevadm info starts with the device specified by the devpath and then
    walks up the chain of parent devices. It prints for every device
    found, all possible attributes in the udev rules key format.
    A rule to match, can be composed by the attributes of the device
    and the attributes from one single parent device.
    
      looking at device '/devices/pci0000:00/0000:00:12.0/usb4/4-3/4-3:1.0/ttyUSB0/tty/ttyUSB0':
        KERNEL=="ttyUSB0"
        SUBSYSTEM=="tty"
        DRIVER==""
    
      looking at parent device '/devices/pci0000:00/0000:00:12.0/usb4/4-3/4-3:1.0/ttyUSB0':
        KERNELS=="ttyUSB0"
        SUBSYSTEMS=="usb-serial"
        DRIVERS=="cp210x"
        ATTRS{port_number}=="0"
    
      looking at parent device '/devices/pci0000:00/0000:00:12.0/usb4/4-3/4-3:1.0':
        KERNELS=="4-3:1.0"
        SUBSYSTEMS=="usb"
        DRIVERS=="cp210x"
        ATTRS{bInterfaceNumber}=="00"
        ATTRS{bAlternateSetting}==" 0"
        ATTRS{bNumEndpoints}=="02"
        ATTRS{bInterfaceClass}=="ff"
        ATTRS{bInterfaceSubClass}=="00"
        ATTRS{bInterfaceProtocol}=="00"
        ATTRS{supports_autosuspend}=="1"
        ATTRS{interface}=="CP2102 USB to UART Bridge Controller"
    
      looking at parent device '/devices/pci0000:00/0000:00:12.0/usb4/4-3':
        KERNELS=="4-3"
        SUBSYSTEMS=="usb"
        DRIVERS=="usb"
        ATTRS{configuration}==""
        ATTRS{bNumInterfaces}==" 1"
        ATTRS{bConfigurationValue}=="1"
        ATTRS{bmAttributes}=="80"
        ATTRS{bMaxPower}=="100mA"
        ATTRS{urbnum}=="10835"
        ATTRS{idVendor}=="10c4"
        ATTRS{idProduct}=="ea60"
        ATTRS{bcdDevice}=="0100"
        ATTRS{bDeviceClass}=="00"
        ATTRS{bDeviceSubClass}=="00"
        ATTRS{bDeviceProtocol}=="00"
        ATTRS{bNumConfigurations}=="1"
        ATTRS{bMaxPacketSize0}=="64"
        ATTRS{speed}=="12"
        ATTRS{busnum}=="4"
        ATTRS{devnum}=="2"
        ATTRS{devpath}=="3"
        ATTRS{version}==" 1.10"
        ATTRS{maxchild}=="0"
        ATTRS{quirks}=="0x0"
        ATTRS{avoid_reset_quirk}=="0"
        ATTRS{authorized}=="1"
        ATTRS{manufacturer}=="Silicon Labs"
        ATTRS{product}=="CP2102 USB to UART Bridge Controller"
        ATTRS{serial}=="0001"
    
      looking at parent device '/devices/pci0000:00/0000:00:12.0/usb4':
        KERNELS=="usb4"
        SUBSYSTEMS=="usb"
        DRIVERS=="usb"
        ATTRS{configuration}==""
        ATTRS{bNumInterfaces}==" 1"
        ATTRS{bConfigurationValue}=="1"
        ATTRS{bmAttributes}=="e0"
        ATTRS{bMaxPower}=="  0mA"
        ATTRS{urbnum}=="134"
        ATTRS{idVendor}=="1d6b"
        ATTRS{idProduct}=="0001"
        ATTRS{bcdDevice}=="0300"
        ATTRS{bDeviceClass}=="09"
        ATTRS{bDeviceSubClass}=="00"
        ATTRS{bDeviceProtocol}=="00"
        ATTRS{bNumConfigurations}=="1"
        ATTRS{bMaxPacketSize0}=="64"
        ATTRS{speed}=="12"
        ATTRS{busnum}=="4"
        ATTRS{devnum}=="1"
        ATTRS{devpath}=="0"
        ATTRS{version}==" 1.10"
        ATTRS{maxchild}=="5"
        ATTRS{quirks}=="0x0"
        ATTRS{avoid_reset_quirk}=="0"
        ATTRS{authorized}=="1"
        ATTRS{manufacturer}=="Linux 3.0.0-24-generic ohci_hcd"
        ATTRS{product}=="OHCI Host Controller"
        ATTRS{serial}=="0000:00:12.0"
        ATTRS{authorized_default}=="1"
    
      looking at parent device '/devices/pci0000:00/0000:00:12.0':
        KERNELS=="0000:00:12.0"
        SUBSYSTEMS=="pci"
        DRIVERS=="ohci_hcd"
        ATTRS{vendor}=="0x1002"
        ATTRS{device}=="0x4397"
        ATTRS{subsystem_vendor}=="0x1043"
        ATTRS{subsystem_device}=="0x8496"
        ATTRS{class}=="0x0c0310"
        ATTRS{irq}=="18"
        ATTRS{local_cpus}=="00000000,00000000,00000000,00000000,00000000,00000000,00000000,00000003"
        ATTRS{local_cpulist}=="0-1"
        ATTRS{numa_node}=="-1"
        ATTRS{dma_mask_bits}=="32"
        ATTRS{consistent_dma_mask_bits}=="32"
        ATTRS{broken_parity_status}=="0"
        ATTRS{msi_bus}==""
    
      looking at parent device '/devices/pci0000:00':
        KERNELS=="pci0000:00"
        SUBSYSTEMS==""
        DRIVERS==""
    
    

Those information will be useful to determinate for sure that this device is your Zwave controller. We will use several information, flagged above as "DRIVERS", "ATTRS{manufacturer}" and "ATTRS{product}". With that, we will be sure that we'll be talking to our controller. You can chose others attributs.
Create rule.
*************
*Create a new file, in folder "/etc/udev/rules.d". Let's call it "98-usbcp210x.rules". 
*Enter those information in the file : 
.. code-block::
    
    # for z-Stick serie 2 to domogik /dev/zwave
    DRIVERS=="usb", ATTRS{manufacturer}=="Silicon Labs", ATTRS{product}=="CP2102 USB to UART Bridge Controller", SYMLINK+="zwave", MODE="0666"
    

The "DRIVERS", "ATTRS{manufacturer}", "ATTRS{product}" values must be coherent with what you have found above.
*Ask udev to rediscover your device :
.. code-block::
    
    # udevadm test $(udevadm info --query path --name ttyUSB0)
    

*Your device should now be re-discovered, let's confirm it :
.. code-block::
    
    $ ls -l /dev/zwave
    lrwxrwxrwx 1 root root 7 2012-08-27 00:46 /dev/zwave -> ttyUSB0
    


******************
How to use plugin
******************
Configure plugin
=================
TODO : Images and comments.
{img fileId=338,stylebox="border",align="center"}

Get Zwave network informations
===============================
TODO : Images and comments.
{img fileId=339,stylebox="border",align="center"}
{img fileId=340,stylebox="border",align="center"}

Configure domogik devices
==========================
TODO : Images and comments.

AdressTy : 'homename-1'.NodeId.instance
Example : ZWHome.5.1
{img fileId=341,stylebox="border",align="center"}
{img fileId=342,stylebox="border",align="center"}


*****************
Developper notes
*****************

TODO : .....

Resources
==========

* `An opensource project for zwave <http://code.google.com/p/open-zwave>`_
* `Introduction to zwave protocol <http://www.digiwave.dk/en/programming/an-introduction-to-the-z-wave-protocol>`_
* `Introduction to zwave programming in C <http://www.digiwave.dk/en/programming/an-introduction-to-z-wave-programming-in-c>`_
* `Zwave API - LinuxMCE wiki <http://wiki.linuxmce.org/index.php/ZWave\_API>`_
* `Python development <http://z-wave.alsenet.com/index.php/Main\_Page>`_