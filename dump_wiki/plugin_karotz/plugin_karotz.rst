{maketoc}


{IMG(src=&quot;http://last48hours.com/wp-content/uploads/2010/10/karotz-nabaztag-270x300.jpg&quot;)}{IMG}

!Purpose
This plugin allows control your Karotz (tts, ears and led)

!Prerequisites
You must install &quot;Domogik controller&quot; in your Karotz

Click below:
[http://www.karotz.com/appz/app?id=1862&amp;category_id=0&amp;filter=mindscape|Domogik controller]

!Plugin configuration
!!Enabling plugin
You can enable plugin by using :
{CODE()}
dmgenplug karotz
{CODE}
if it don't work, try with -f option.


You just have to reload administration page to see the plugin in the list.

!!Configuration
!!!startup-plugin
You can enable or disable the auto-start of the plugin.

!!!name
Indicate the name of your Karotz (not used at the moment)

!!!installid
It is necessary to indicate the &quot;Domogik controller&quot; installid of your Karotz.

{img fileId=&quot;315&quot; thumb=&quot;y&quot; rel=&quot;box[g]&quot;}

!!!language
Language spoken by the Kartoz (EN: English, FR: French, DE: German, ES: Spanish)

!!Start plugin
You can now start the plugin (start button)

!Developper Notes

!!How the online plugin to test of order? 
In a final one, since the catalog xpl/bin it is necessary to launch the order. 
{CODE()}
./karotz.py -f
{CODE}

In a final other, since the catalog xpl/bin it is necessary to launch the order. 
for example: tts command
{CODE()}
./send.py xpl-cmnd karotz.basic &quot;device=nameofyourkarotz,command=tts,value=yourmessage &quot;
{CODE}

where nameofyourkarotz is the name you have configure in the configuration page of the plugin.
where yourmessage is the message that must be transmitted


!!XPL-CMND Structure
{CODE()}
tts example:

karotz.basic
{
device=&lt;Name of your karotz&gt;
command=tts
value=&lt;text to speech&gt;
}

led example:

karotz.basic
{
device=&lt;Name of your karotz&gt;
command=led
value=&lt;color value (hex) for example : 0000FF&gt;
time=10 (in secondes)
}

ears example:

karotz.basic
{
device=&lt;Name of your karotz&gt;
command=ears
right=&lt;Position (dec) for example : 20&gt;
left=&lt;Position (dec) for example : 10&gt;
}

{CODE}