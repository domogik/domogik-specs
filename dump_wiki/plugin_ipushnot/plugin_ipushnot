{maketoc}

!Purpose
This plugin allows sending notification to your [http://www.apple.com/fr/iphone/|Iphone]/[http://www.apple.com/fr/ipad/|Ipad].

It use the free [http://pushme.to|pushme.to] application and you can download it from [http://itunes.apple.com/fr/genre/ios/id36?mt=8|itunes].

this service is free.
author of this plugin: Kriss@domogik.org
 
Iphone/Ipad and itunes are [http://www.apple.com|Apple]'s mark.

!Application Installation required
{CODE()}
install the pushme.to apps from itunes to your iphone.
When install is finish, launch this app and create your account (nickname).
{CODE}

!Plugin configuration
!!Enabling plugin
You can enable plugin by using :
{CODE()}
dmgenplug ipushnot
{CODE}

You just have to reload administration page to see the plugin in the list.

!!Configuration
!!Start plugin
You can enable or disable the auto-start of the plugin.

{img fileId=&quot;277&quot; thumb=&quot;y&quot; rel=&quot;box[g]&quot;}

Once the configuration is done, you can start the plugin (start button).


!Developper Notes
!!How the online plugin to test of order? 
In a final one, since the catalog xpl/bin it is necessary to launch the order. 
{CODE()}
./ipushnot.py -f
{CODE}

In a final other, since the catalog xpl/bin it is necessary to launch the order. 
{CODE()}
./send.py xpl-cmnd sendmsg.push &quot;to=yourpushmenickname,body=yourmessage,signature=yoursignature&quot;
{CODE}

where yourpushmenickname is your pushme nickname (your account to pushme service)
where yourmessage is the message that must be transmitted
where yoursignature is the signature you want to put in your message


!!!xPL schema

{CODE()}
sendmsg.push
{
to=&lt;Email address, User ID or Phone Number&gt;
title=&lt;title of the message&gt; (optional)
body=&lt;Message body&gt;
signature=&lt;signature of the message&gt; (optional)
}
{CODE}


* [|sendmsg.push]


