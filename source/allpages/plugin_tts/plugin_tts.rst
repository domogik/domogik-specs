.. toctree::



********
Purpose
********

This plugin allows sending message by TTS (Text To Speech).  

*********************
Package Installation
*********************

 TTS festival
==============

For use TTS with festival for english language:

.. code-block:: json


    
    # apt-get install festival
    


 TTS espeak
============


 TTS SVOX pico
===============

.. code-block:: json


    
    # apt-get install libttspico-utils
    



*********************
Plugin configuration
*********************

Enabling plugin
================

You can enable plugin by using :
.. code-block:: json


    
    dmgenplug tts
    


You just have to reload administration page to see the plugin in the list.

Configuration
==============

Start plugin
=============

You can now start the plugin (start button).

software : Command line for use TTS software
*********************************************

* for french language with SVOX pico:
** pico2wave -l fr-FR -w tts.wav \"%s\" | paplay tts.wav 

* for french language with espeak:
** espeak -v fr \"%s\"

* for english language :
** echo \"%s\" | festival --tts




*****************
Developper Notes
*****************


How the online plugin to test of order? 
=========================================

In a final one, since the catalog xpl/bin it is necessary to launch the order. 
.. code-block:: json


    
    ./tts.py -f
    


In a final other, since the catalog xpl/bin it is necessary to launch the order. 
.. code-block:: json


    
    ./send.py xpl-cmnd tts.basic “speech=your_text"
    




xPL schema
***********

* `tts.basic <http://xplproject.org.uk/wiki/index.php?title=Schema\_-\_TTS.BASIC>`_


!!!!Message to send to plugin for send message to TTS software
To ask a plugin to send a message, you should send this __xpl-cmnd__ message :
.. code-block:: json


    
    TTS.BASIC
    {
    SPEECH=<text to announce>
    [VOLUME=<0 to 100>]
    [SPEED=<-10 to 10>]
    [VOICE=<name of voice to use>]
    }
    


For this moment only field "speech" is use.
