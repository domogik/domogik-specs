Note : this page is actually a draft for the reflexion on facilities to adapt external plugins to Domogik

************************************************
How to adapt a non-python xpl plugin to domogik
************************************************

To make a non-domogik plugin work with Domogik, you have several things to do :

1 - Give info to manager when plugins is asked to
==================================================

When you launch plugin with option "config", You should obtain on stdout something like that :

||TODO : complete with last evolutions||

.. code-block:: json


    
    $ my_plugin.pl config
    IS_DOMOGIK_PLUGIN = True                                                                                                
    DOMOGIK_PLUGIN_TECHNOLOGY = "rfid"                                                                                      
    DOMOGIK_PLUGIN_DESCRIPTION = "Use Mir:ror device"                                                                       
    DOMOGIK_PLUGIN_VERSION = "0.1"                                                                                          
    DOMOGIK_PLUGIN_DOCUMENTATION_LINK = "http://wiki.domogik.org/tiki-index.php?page=plugins/Mirror"                        
    DOMOGIK_PLUGIN_CONFIGURATION=[                                                                                          
          {"id" : 0,                                                                                                        
           "key" : "startup-plugin",                                                                                        
           "description" : "Automatically start plugin at Domogik startup",                                                 
           "default" : "False"},                                                                                            
          {"id" : 1,                                                                                                        
           "key" : "device",                                                                                                
           "description" : "Mir:ror device (ex : /dev/hidraw0)",                                                            
           "default" : "/dev/hidraw0"},                                                                                     
          {"id" : 2,                                                                                                        
           "key" : "nbmaxtry",                                                                                              
           "description" : "Max number of tries to open Mir:ror device",                                                    
           "default" : 5,                                                                                                   
          {"id" : 3,                                                                                                        
           "key" : "interval",                                                                                              
           "description" : "Delay between each try to open Mir:ror device",                                                 
           "default" : 10}]                           
    


The plugin must stop after displaying this.

These informations will be used by Domogik Manager (which at startup will launch each plugin with "config" option) to get informations about plugins. These informations will be get by REST server with /plugin/list/<plugin name> and /plugin/detail/<plugin name> to give informations to UI.

By setting these informations, you will be able to configure your plugin directly from UI!


2 - Implement "-f" option 
=====================================

Without -f option, plugin must launch itself in background.

With -f option, plugin should launch itself on foreground.



3 - Stop plugin when requested
===============================

When plugin receives this xpl message, it should stop itself.
||TODO : update if it changed||

.. code-block:: json


    
    DOMOGIK.SYSTEM
    {
    COMMAND=command to send
    HOST=name of the host where a component should be started/stopped
    [PLUGIN=name of the plugin concerned by the command]
    [FORCE=0||1]
    }
    



4 - Get config with xPL queries
================================

At startup, plugin should get configuration from Domogik database. To do this, plugin will ask with a xPL message on network for its configuration. The Database Manager will reply to this request with the config values

||TODO : describe xpl dialog here||


5 - Where the plugin should be put ?
=====================================

||TODO : see if we use an external folder dedicated to non-python plugins||


				