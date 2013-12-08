{maketoc}


{IMG(src=&quot;http://upload.wikimedia.org/wikipedia/commons/thumb/d/d4/Nabaztagtag_large.jpg/220px-Nabaztagtag_large.jpg&quot;)}{IMG}

!Purpose
This plugin allows sending notification to your [http://fr.wikipedia.org/wiki/Nabaztag|Nabaztag]. This plugin shloud work with a Karotz if you put his name in the serial field.

It use the free [http://nabaztag.forumactif.fr/t13483-ojn-api-unifiee-wizzcc-pour-nabaztag-karotz|Wizz.cc] Service and an OpenJabNab Server.


this service is free.
author of this plugin: Kriss@domogik.org
 

!prerequisites
You need to know your serial and token id. You can find them in your OpenJabNab Admin Panel.



!Plugin configuration
!!Enabling plugin
You can enable plugin by using :
{CODE()}
dmgenplug nbz_tts
{CODE}
if it don't work, try with -f option.


You just have to reload administration page to see the plugin in the list.

!!Configuration
!!!startup-plugin
You can enable or disable the auto-start of the plugin.

!!!name
It is necessary to indicate the name of your nabaztag/Karotz.

!!!serial
It is necessary to indicate the serial of your Nabaztag. For Karotz, you need to indicate the name of your Karotz instead of a serial.

!!!token
It is necessary to indicate the token of your Nabaztag/Karotz.  

!!!voice
It is necessary to indicate the voice of your Nabaztag/Karotz. It can be voice=xx or ws_kajedo=xxxx or ws_acapela=xxxx . You can find a list of different voice [http://nabaztag.forumactif.fr/t13483-ojn-api-unifiee-wizzcc-pour-nabaztag-karotz|here].


You can add more nabaztag/Karotz with the &quot;add interface&quot; button.
Once the configuration is done, you can start the plugin (start button).

{img fileId=&quot;278&quot; thumb=&quot;y&quot; rel=&quot;box[g]&quot;}

!Developper Notes

!!How the online plugin to test of order? 
In a final one, since the catalog xpl/bin it is necessary to launch the order. 
{CODE()}
./nbz_tts.py -f
{CODE}

In a final other, since the catalog xpl/bin it is necessary to launch the order. 
{CODE()}
./send.py xpl-cmnd sendmsg.push &quot;to=nameofyournabaztag,body=yourmessage&quot;
{CODE}

where nameofyournabaztag is the name you have configure in the configuration page of the plugin.
where yourmessage is the message that must be transmitted


!!!XPL-CMND Structure
{CODE()}
sendmsg.push
{
to=&lt;Email address, User ID or Phone Number&gt;
title=&lt;titleof the message&gt; (optional)
body=&lt;Message body&gt;
signature=&lt;signature of the message&gt; (optional)
}
{CODE}

* [|sendmsg.push]


