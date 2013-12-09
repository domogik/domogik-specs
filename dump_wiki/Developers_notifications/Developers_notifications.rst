!Notifications
{maketoc}

See HTML5 notifications for definitions : http://www.w3.org/TR/notifications/

!!What is a notification ?
It is a way to &quot;notify&quot; an event for example :
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

!!Sending a notification
To test notifications, just use this command : 
{CODE()}
./send.py xpl-trig notify.basic &quot;title=titre,message=blabl
a,type=info,timestamp=1286522935812&quot;  
{CODE}
More details about options in the ''xPL Schema chapter''

!!How to listen for notifications from an UI
When a notification is received by the statistic manager (REST), an event is created for a device with id=0. So, you just have to put the device with ''id=0'' in your ''__/events/request__'' calls to REST.

!!!Example
For this request,
{CODE()}
wget -qO- http://192.168.0.10:40405/events/request/new/0
{CODE}

After a notification reception, it will receive :
{CODE()}
{
	&quot;status&quot; : &quot;OK&quot;, 
	&quot;code&quot; : 0, 
	&quot;description&quot; : &quot;None&quot;, 
	&quot;event&quot; : [
		{
			&quot;timestamp&quot; : 1286529227,
			&quot;data&quot; : [
				{
					&quot;value&quot; : &quot;titre&quot;,
					&quot;key&quot; : &quot;title&quot;
				},
				{
					&quot;value&quot; : &quot;blabla&quot;,
					&quot;key&quot; : &quot;message&quot;
				},
				{
					&quot;value&quot; : &quot;info&quot;,
					&quot;key&quot; : &quot;type&quot;
				},
				{
					&quot;value&quot; : &quot;1286522935812&quot;,
					&quot;key&quot; : &quot;timestamp&quot;
				}
			],
			&quot;ticket_id&quot; : &quot;1&quot;,
			&quot;device_id&quot; : 0
		}
	]
}
{CODE}

Notice the four elements :
* title
* message
* type (optionnal) : info, warning, error, success
* timestamp (optionnal) : time linked to notification

!!!xPL Schema
A notification is an event, so __only ''xpl-trig''__ is supported.

!!!xpl-trig
{CODE()}
xpl-trig
{
...
}
notify.basic
{
title = &lt;notification title&gt;
message = &lt;content of notification&gt;
[type = &lt;INFO|WARNING|ERROR|SUCCESS&gt;]
[timestamp = &lt;date/time to diplay in timestamp format (the universal)&gt;]
}
{CODE}

By default, if no type is defined, consider that it is an ''__INFO__'' notification.