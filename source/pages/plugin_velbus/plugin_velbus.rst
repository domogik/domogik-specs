Table of contents
******************

.. toctree::



**************
 General info
**************

`Velbus] is a protocol from [http://www.vellman.eu|Velleman <http://www.velbus.eu>`_.

Velbus is a __robust and reliable__ modular home automation system. The Velbus System is a 4-wire Home Automation System perfect for the DIY enthusiast or professional contractor, thanks to it's easy installation. To interconnect the modules a bus or cat5 cable can be used. Only 4 wires are used (2 for power and 2 for data). There is no central unit making the system extremely reliable and simple. Professional home automation is now __within everyone’s reach__. 

How does Velbus work?
======================


A typical arrangement consists of two basic modules: an input and an output module. Input modules translate the information coming from outside (e.g. pushbuttons, switches, sensors, etc.) to bus instructions. Output Modules interpret these instructions and in turn control lighting, heating, air conditioning, electrical outlets, window blinds, etc. The status of the output module is indicated by feedback LEDs on the input module. Applications: home automation, office or business, process monitoring, etc.

 Protocol Description
======================

`Velbus Protocol Summary <http://www.velleman.be/downloads/Velbus\_ProtocolSummary.pdf>`_

 Supported Velbus messages
===========================

TODO

 Tested modules
================

* VMB4YRLD = PROGRAMMABLE 4-CHANNEL VOLTAGE-OUT RELAY MODULE 
* VMB4RYNO = PROGRAMMABLE 4-CHANNEL RELAY MODULE
* VMB1DM   = DIMMER MODULE
* VMB1BL   = BLINDS MODULE
* VMB2BL   = 2-CHANNEL BLINDS MODULE
* VMB4RY   = 4-CHANNEL RELAY MODULE 
* VMB1RY   = RELAY MODULE


 Modules that should work
==========================

 V0.1.0 and V0.2.0 and up
**************************

See Tested modules chapter

 V0.3.0 and UP
***************

* VMB4DC = 4-CHANNEL 0(1)...10V CONTROLLER
* VMBDME = DIMMER FOR ELEKTRONIc/RESISTIEVE LOAD
* VMBDMI = DIMMER FOR INDUCTIEVE/RESISTIEVE LOAD
* VMB1DMDC = 0…10VDC CONTROLED DIMMER
* VMB1LED = DIMMER FOR LED CONTROL

********
 Plugin
********

 Config
========

defaults to /dev/ttyACM0
/dev/ttyACM0 for the VMB1USB module

 Workflow
==========

 Init
******

* request the config with domogik.config request
* try to open the device (default /dev/ttyACM0)
* TODO: scan the Velbus so the plugin knows all connected modules and store them
* start listener for xpl messages
* start xpl heartbeat

 On receiving of xpl message
*****************************

* translate the xpl message to a coresponding Velbus message

 On receiving of a Velbus message
**********************************

* check in the discoverd list what module type the message is coming from and select the correct xpl schema (lighting.basic, sensor.basic, ...)
* build the xpl message and transmit

 TODO
======

* scan the Velbus on startup