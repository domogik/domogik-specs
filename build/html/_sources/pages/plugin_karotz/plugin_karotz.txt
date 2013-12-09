.. toctree::




{IMG(src="http://last48hours.com/wp-content/uploads/2010/10/karotz-nabaztag-270x300.jpg")}{IMG}

********
Purpose
********

This plugin allows control your Karotz (tts, ears and led)

**************
Prerequisites
**************

You must install "Domogik controller" in your Karotz

Click below:
`Domogik controller <http://www.karotz.com/appz/app?id=1862&amp;category\_id=0&amp;filter=mindscape>`_

*********************
Plugin configuration
*********************

Enabling plugin
================

You can enable plugin by using :
.. code-block:: json


    
    dmgenplug karotz
    

if it don't work, try with -f option.


You just have to reload administration page to see the plugin in the list.

Configuration
==============

startup-plugin
***************

You can enable or disable the auto-start of the plugin.

name
*****

Indicate the name of your Karotz (not used at the moment)

installid
**********

It is necessary to indicate the "Domogik controller" installid of your Karotz.

{img fileId="315" thumb="y" rel="box[g]"}

language
*********

Language spoken by the Kartoz (EN: English, FR: French, DE: German, ES: Spanish)

Start plugin
=============

You can now start the plugin (start button)

*****************
Developper Notes
*****************


How the online plugin to test of order? 
=========================================

In a final one, since the catalog xpl/bin it is necessary to launch the order. 
.. code-block:: json


    
    ./karotz.py -f
    


In a final other, since the catalog xpl/bin it is necessary to launch the order. 
for example: tts command
.. code-block:: json


    
    ./send.py xpl-cmnd karotz.basic "device=nameofyourkarotz,command=tts,value=yourmessage "
    


where nameofyourkarotz is the name you have configure in the configuration page of the plugin.
where yourmessage is the message that must be transmitted


XPL-CMND Structure
===================

.. code-block:: json


    
    tts example:
    
    karotz.basic
    {
    device=<Name of your karotz>
    command=tts
    value=<text to speech>
    }
    
    led example:
    
    karotz.basic
    {
    device=<Name of your karotz>
    command=led
    value=<color value (hex) for example : 0000FF>
    time=10 (in secondes)
    }
    
    ears example:
    
    karotz.basic
    {
    device=<Name of your karotz>
    command=ears
    right=<Position (dec) for example : 20>
    left=<Position (dec) for example : 10>
    }
    
    
