.. toctree::



********
Purpose
********
This plugin allows sending notification to your `Iphone]/[http://www.apple.com/fr/ipad/|Ipad <http://www.apple.com/fr/iphone/>`_.

It use the free `pushme.to] application and you can download it from [http://itunes.apple.com/fr/genre/ios/id36?mt=8|itunes <http://pushme.to>`_.

this service is free.
author of this plugin: Kriss@domogik.org
 
Iphone/Ipad and itunes are `Apple <http://www.apple.com>`_'s mark.

**********************************
Application Installation required
**********************************
.. code-block::
    
    install the pushme.to apps from itunes to your iphone.
    When install is finish, launch this app and create your account (nickname).
    


*********************
Plugin configuration
*********************
Enabling plugin
================
You can enable plugin by using :
.. code-block::
    
    dmgenplug ipushnot
    


You just have to reload administration page to see the plugin in the list.

Configuration
==============
Start plugin
=============
You can enable or disable the auto-start of the plugin.

{img fileId="277" thumb="y" rel="box[g]"}

Once the configuration is done, you can start the plugin (start button).


*****************
Developper Notes
*****************
How the online plugin to test of order? 
=========================================
In a final one, since the catalog xpl/bin it is necessary to launch the order. 
.. code-block::
    
    ./ipushnot.py -f
    


In a final other, since the catalog xpl/bin it is necessary to launch the order. 
.. code-block::
    
    ./send.py xpl-cmnd sendmsg.push "to=yourpushmenickname,body=yourmessage,signature=yoursignature"
    


where yourpushmenickname is your pushme nickname (your account to pushme service)
where yourmessage is the message that must be transmitted
where yoursignature is the signature you want to put in your message


xPL schema
***********

.. code-block::
    
    sendmsg.push
    {
    to=<Email address, User ID or Phone Number>
    title=<title of the message> (optional)
    body=<Message body>
    signature=<signature of the message> (optional)
    }
    



* [|sendmsg.push]


