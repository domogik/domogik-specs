**************
Notifications
**************

.. toctree::



See HTML5 notifications for definitions : http://www.w3.org/TR/notifications/

What is a notification ?
=========================

It is a way to "notify" an event for example :
* incoming call
* mail reception
* a door opens
* etc

The ways to notify could be :
* a lightbox on a web ui
* a notification on a smartphone
* a voice (TTS) message in your house
* a message box in the media center (possible in xbmc for example)

There are 2 ways to check for notifications :
* listening to xpl (plugin case : voice message, sms message, xbmc plugin, etc)
* listening to REST (web ui, smartphone's ui)

Sending a notification
=======================

To test notifications, just use this command : 
.. code-block:: json


    
    ./send.py xpl-trig notify.basic "title=titre,message=blabl
    a,type=info,timestamp=1286522935812"  
    

More details about options in the ''xPL Schema chapter''

How to listen for notifications from an UI
===========================================

When a notification is received by the statistic manager (REST), an event is created for a device with id=0. So, you just have to put the device with ''id=0'' in your ''__/events/request__'' calls to REST.

Example
********

For this request,
.. code-block:: json


    
    wget -qO- http://192.168.0.10:40405/events/request/new/0
    


After a notification reception, it will receive :
.. code-block:: json


    
    {
    	"status" : "OK", 
    	"code" : 0, 
    	"description" : "None", 
    	"event" : [
    		{
    			"timestamp" : 1286529227,
    			"data" : [
    				{
    					"value" : "titre",
    					"key" : "title"
    				},
    				{
    					"value" : "blabla",
    					"key" : "message"
    				},
    				{
    					"value" : "info",
    					"key" : "type"
    				},
    				{
    					"value" : "1286522935812",
    					"key" : "timestamp"
    				}
    			],
    			"ticket_id" : "1",
    			"device_id" : 0
    		}
    	]
    }
    


Notice the four elements :
* title
* message
* type (optionnal) : info, warning, error, success
* timestamp (optionnal) : time linked to notification

xPL Schema
***********

A notification is an event, so __only ''xpl-trig''__ is supported.

xpl-trig
*********

.. code-block:: json


    
    xpl-trig
    {
    ...
    }
    notify.basic
    {
    title = <notification title>
    message = <content of notification>
    [type = <INFO|WARNING|ERROR|SUCCESS>]
    [timestamp = <date/time to diplay in timestamp format (the universal)>]
    }
    


By default, if no type is defined, consider that it is an ''__INFO__'' notification.