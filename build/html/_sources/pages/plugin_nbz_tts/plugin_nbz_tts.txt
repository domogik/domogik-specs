.. toctree::




{IMG(src="http://upload.wikimedia.org/wikipedia/commons/thumb/d/d4/Nabaztagtag_large.jpg/220px-Nabaztagtag_large.jpg")}

********
Purpose
********

This plugin allows sending notification to your `Nabaztag <http://fr.wikipedia.org/wiki/Nabaztag>`_. This plugin shloud work with a Karotz if you put his name in the serial field.

It use the free `Wizz.cc <http://nabaztag.forumactif.fr/t13483-ojn-api-unifiee-wizzcc-pour-nabaztag-karotz>`_ Service and an OpenJabNab Server.


this service is free.
author of this plugin: Kriss@domogik.org
 

**************
prerequisites
**************

You need to know your serial and token id. You can find them in your OpenJabNab Admin Panel.



*********************
Plugin configuration
*********************

Enabling plugin
================

You can enable plugin by using :
.. code-block:: json


    
    dmgenplug nbz_tts
    

if it don't work, try with -f option.


You just have to reload administration page to see the plugin in the list.

Configuration
==============

startup-plugin
***************

You can enable or disable the auto-start of the plugin.

name
*****

It is necessary to indicate the name of your nabaztag/Karotz.

serial
*******

It is necessary to indicate the serial of your Nabaztag. For Karotz, you need to indicate the name of your Karotz instead of a serial.

token
******

It is necessary to indicate the token of your Nabaztag/Karotz.  

voice
******

It is necessary to indicate the voice of your Nabaztag/Karotz. It can be voice=xx or ws\_kajedo=xxxx or ws\_acapela=xxxx . You can find a list of different voice `here <http://nabaztag.forumactif.fr/t13483-ojn-api-unifiee-wizzcc-pour-nabaztag-karotz>`_.


You can add more nabaztag/Karotz with the "add interface" button.
Once the configuration is done, you can start the plugin (start button).

{img fileId="278" thumb="y" rel="box[g]"}

*****************
Developper Notes
*****************


How the online plugin to test of order? 
=========================================

In a final one, since the catalog xpl/bin it is necessary to launch the order. 
.. code-block:: json


    
    ./nbz_tts.py -f
    


In a final other, since the catalog xpl/bin it is necessary to launch the order. 
.. code-block:: json


    
    ./send.py xpl-cmnd sendmsg.push "to=nameofyournabaztag,body=yourmessage"
    


where nameofyournabaztag is the name you have configure in the configuration page of the plugin.
where yourmessage is the message that must be transmitted


XPL-CMND Structure
*******************

.. code-block:: json


    
    sendmsg.push
    {
    to=<Email address, User ID or Phone Number>
    title=<titleof the message> (optional)
    body=<Message body>
    signature=<signature of the message> (optional)
    }
    


* [|sendmsg.push]


