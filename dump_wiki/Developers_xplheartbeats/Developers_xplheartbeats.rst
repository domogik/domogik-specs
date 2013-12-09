***************
XPL Heartbeats
***************
.. toctree::



XPL Specifications
===================

Heartbeat behaviour at initial device startup 
***********************************************
When the xPL device/application starts, it should start sending xPL heartbeats as soon as it can and send them every 3-10 seconds until it hears/receives one of it's own heartbeats. The reception by a device of that devices own heartbeat indicates that there is a functioning xPL hub. Once the heartbeat is received, the application can drop back to sending a heartbeat once every "interval" minutes.

Until the device/application hears it's own echo, it should not send or expect to receive any other message. In fact, until a hub is confirmed, the device is not really part of the xPL network.
If no echoed heartbeat has been received after 2 minutes, the device should drop to sending a heartbeat once every 30 seconds indefinetly until it hears it's own echo. 

Heartbeat behaviour at device shutdown or identity change 
***********************************************************

When an xPL device is about to shutdown or if the device is about to change any part of it's identity (vendor ID, device ID or instance ID), the device should send a special "shutdown" heartbeat message as it's last act. That message should have a schema type of "end" (i.e. hbeat.end or config.end). Many xPL devices, upon reception of such a message, will remove the device from any internal caches or uses. Other than using the schema type of "end", the message is otherwise a normal heartbeat message for the device.

 Reference
***********

Source: `XPL heartbeat specifications <http://xplproject.org.uk/wiki/index.php?title=XPL\_Specification\_Document#Heartbeat\_Messages>`_
XPL Hbeat: `HBEAT Schema <http://xplproject.org.uk/wiki/index.php?title=Schema\_-\_HBEAT>`_ 
Evolution: `728 (hbeat discovery) <http://tracker.domogik.org/issues/728>`_
Evolution: `717 (hbeat.end) <http://tracker.domogik.org/issues/717>`_


Domogik integration
====================

Because the hub discovery should be done before the startup of the xpl device (the plugin in this case) it will be integrated into the (xpl)Manager class inside the __init__ methode.

An XPLTimer is started at init, with a random interval between 3 and 10 seconds, this will send out the heartbeats.

At the monitor method (receiving packets), a new part is added to check for hbeat echos, this check is only done when no hub is found yet.

in the hbeat.app message a new key/value pair is added, this pair will display the status of the plugin:
*0 = plugin started, no hub found
*1 = plugin started hub found, waiting for config
*2 = plugin started, hub found and plugin configured.

Inside the (xpl)Manager leave methode the hbeat.end message will be sent.

New vars
*********
*status = int (see description above)
*_lock_status =  semaphore because different threads update/read the status
*foundhub = threading.event to keep track if a hub is found