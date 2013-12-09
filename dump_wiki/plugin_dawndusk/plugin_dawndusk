The purpose of this plugin is to manage the dawn and dusk over XPL.
It sends a dawn (or dusk) message over XPL when dawn (or dusk) occurs.
It can also be asked to know if it is the day or the night.
See documentation [http://xplproject.org.uk/wiki/index.php?title=Schema_-_DAWNDUSK.BASIC|here] for more details.

!!Prerequisites
Normally you don't need to do this, but ...
- install the apscheduler extension for python:
__sudo easy_install apscheduler__
- install the pyephem package for python
__sudo easy_install pyephem__

!!Install the plugin
This plugin is available in the development sources. Follow this [http://wiki.domogik.org/Developers_installation|documentation|nocache] to install them.
Enable the plugin :
__sudo dmgenplug -f dawndusk__

!!Configure and start the plugin
{IMG(attId=&quot;428&quot;)}{IMG}

You must specify the latitude and the longitude of your house. Use your GPS or Google maps to find them.
If you have the cron plugin installed, you can use it instead of the internal one.


You can add a list of devices that should be activated at dawn and deactivated at dusk (like your shutters).
Here are the parameters :

xpltype: the xpl type to use (ie xpl-cmnd)
schema : the schema to use to send the command (ie x10.basic)	
addname : the name of the adress field (ie device)
add : the adresse of the device (ie A1, 04-1)	
command : the name of the command field (ie command, level)
dawn : Value of command when dawn event	occurs (ie on, 0)
dusk : Value of command when dusk event	occurs (ie off, 255)
dawnseconds : Value in +/- minutes after/before dawn event
duskseconds : Value in +/- minutes after/before dusk event

Save the configuration and start the plugin.
That's all.

!!Configuration examples
!!!Velbus Light
xpltype : xpl-cmnd
schema : lighting.basic
addname : device
add : 04-1
command : level
dawn : 0
dusk : 255

!!!Velbus Shutter
xpltype : xpl-cmnd
schema : shutter.basic
addname : device
add : 07-1
command : command
dawn : up
dusk : down

!!!scene.Fake device
xpltype : xpl-cmnd
schema : scene.basic
addname : number
add : fake1 (the address of your scene.Fake device)
command : command
dawn : fake-true
dusk : fake-false