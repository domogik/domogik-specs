{maketoc}

!Purpose
This plugin was design to control foscam camera relay command.

{img fileId=&quot;272&quot; thumb=&quot;y&quot; rel=&quot;box[g]&quot; title=&quot;foscam photo&quot; alt=&quot;foscam photo&quot;}

Right now this plugin was tested with :
* FI8908W
* But should work with all fosam equiped with relay command.

!Prerequisite
Domogik server should be able to access the foscam camera using http protocol. So be sure to open firewall if necessary.

This plugin doesn't use any specific python package.

plug your relay on pin 1 and 2 according to this picture :
{img fileId=&quot;273&quot; thumb=&quot;y&quot; rel=&quot;box[g]&quot; title=&quot;foscam relay&quot; alt=&quot;foscam relay&quot;}

!Plugin configuration
!!Enabling plugin
You can enable plugin by using :
{CODE()}
dmgenplug foscam
{CODE}

You just have to reload administration page to see the plugin in the list.

!!Configuration
In Domogik administration, go to foscam configuration page.
The plugin is preconfigured with an example :

{img fileId=&quot;271&quot; thumb=&quot;y&quot; rel=&quot;box[g]&quot; title=&quot;foscam plugin&quot; alt=&quot;foscam plugin&quot;}

!!!Name
Give a name to each camera you add, this name will be the adress device.

!!!Ip
Could also be a dns name

!!!port
use to reach the cam, default on is already 80.

!!!user &amp; password
It's recommend not to use &quot;admin&quot;, so i suggest you to create a new one from your foscam camera web site, and set a password too !

!!!delay
I implement this command for my special need, i will explain it a little later on this page, probably you never use it, so you could leave the default value for now (5).

Don't forget to save your configuration...

!!Device
Now it's time to create a device, stay in the administration section, but move to Organisation/Devices. On the Devices List, hit &quot;+&quot; .

{img fileId=&quot;270&quot; thumb=&quot;y&quot; rel=&quot;box[g]&quot; title=&quot;Device
&quot; alt=&quot;Device&quot;}

!!!Name
Enter the name of your choice

!!!Address
Rewrite exatly the plugin interface name your had enter in the previous chapter.

!!!Feature
Choose Foscam Camera and Relay

!!!Usage
Choose the icon you want.

!!!Description &amp; Reference
Not use.

!!Start plugin
So go back to the plugin configuraion and start the plugin (start button).

!!place the widget
!!! Switch
Move to Organisation / Widgets
Select the aera where you want to see the widget, a windows should appear, where you should see all your devices. Select the foscam device, switch and Basic widget.

{img fileId=&quot;269&quot; thumb=&quot;y&quot; rel=&quot;box[g]&quot; title=&quot;Widget placement&quot; alt=&quot;Widget placement&quot;} 

You should go back to visualisation mode and  your widget sould work.

In this example I made you select a switch widget which is an actuator LOW(open)/HIGH(close), each time you hit it, the relay switch from Open to Close to Open...etc

!!! Trigger
In some case relay should only be in contact for a specific duration. I implement Pulse command for this need.
If you need a such thing, folow the switch paragraph, just select trigger instead of switch.
Each time you hit the widget, your relay will be in contact and after a delay, release.This delay can be set in the plugin configuration page.




!Developper Notes

!!xPL schema
No official xPL Schema exists for Foscam. A dedicated schema has been made for this feature.
[http://xplproject.org.uk/forums/viewtopic.php?f=2&amp;t=908&amp;|Discussion on official xPL Forum about this xPL schema]

!!!xpl-cmnd
{CODE()}
{
hop=1
source=xpl-rest.domogik
target=*
}
control.basic
{
current=HIGH
device=Camera1
type=output
}
{CODE}
!!!xpl-trig
{CODE()}
{
hop=1
source=xpl-foscam.machine_name
target=*
}
sensor.basic
{
device=Camera1
type=output
current=HIGH
}
{CODE}

!!!Command

Manual command example, assuming your usercode is &quot;FF&quot;

First go to ~/domogik/src/domogik/xpl/bin/

* Turn HIGH Camera1 relay :
{CODE()} python ./send.py xpl-cmnd sensor.basic &quot;device=Camera1,type=output,current=HIGH&quot;
{CODE}

* Turn LOW Camera1 relay :
{CODE()} python ./send.py xpl-cmnd sensor.basic &quot;device=Camera1,type=output,current=LOW&quot;
{CODE}

* Turn PULSE Camera1 relay :
{CODE()} python ./send.py xpl-cmnd sensor.basic &quot;device=Camera1,type=output,current=PULSE&quot;
{CODE}





