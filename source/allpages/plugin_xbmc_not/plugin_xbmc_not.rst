*********
 Status 
*********

First version released

 TODO 
=======

* Create and use a new xPL message more adapted to media centers.

****************
 Plugin's goal 
****************

This plugin allows to send notifications to XBMC.

*************
 xPL Schema 
*************

`Schema of the xPL project <http://xplproject.org.uk/wiki/index.php?title=Schema\_-\_OSD.BASIC>`_

* command="WRITE"
* delay=<duration of message>
* row=<0 for title, 1 for message>
* text=<titre or message. Depends on row>

****************
 Prerequisites 
****************


 Dependencies 
===============

An XBMC Media Center with web API activated is needed.

***************
 How it works 
***************

The xPL client listens to ''osd.basic messages''. When two are received (one for the title, the other for the message), it tells to the HTTP API of XBMC to display a notification within a delay. If too much time is elapsed between messages reception (cf ''maxdelay'' parameter), no notification is send.

****************
 Configuration 
****************

You need to add the following entries :

* address : ip:port of XBMC's web server
* delay: default delay for displaying notification. This value is used if ''delay!0'' is in the xPL message.
* maxdelay: the maximum delay between two messages the process will wait for before cancelling notification. This value must be low.

******************
Developpers notes
******************

http://wiki.xbmc.org/index.php?title=JSON_RPC