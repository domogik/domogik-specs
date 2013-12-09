Note : this page is actually a draft for the reflexion on facilities to adapt external plugins to Domogik

!How to adapt a non-python xpl plugin to domogik
To make a non-domogik plugin work with Domogik, you have several things to do :

!!1 - Give info to manager when plugins is asked to
When you launch plugin with option &quot;config&quot;, You should obtain on stdout something like that :

||TODO : complete with last evolutions||

{CODE()}
$ my_plugin.pl config
IS_DOMOGIK_PLUGIN = True                                                                                                
DOMOGIK_PLUGIN_TECHNOLOGY = &quot;rfid&quot;                                                                                      
DOMOGIK_PLUGIN_DESCRIPTION = &quot;Use Mir:ror device&quot;                                                                       
DOMOGIK_PLUGIN_VERSION = &quot;0.1&quot;                                                                                          
DOMOGIK_PLUGIN_DOCUMENTATION_LINK = &quot;http://wiki.domogik.org/tiki-index.php?page=plugins/Mirror&quot;                        
DOMOGIK_PLUGIN_CONFIGURATION=[                                                                                          
      {&quot;id&quot; : 0,                                                                                                        
       &quot;key&quot; : &quot;startup-plugin&quot;,                                                                                        
       &quot;description&quot; : &quot;Automatically start plugin at Domogik startup&quot;,                                                 
       &quot;default&quot; : &quot;False&quot;},                                                                                            
      {&quot;id&quot; : 1,                                                                                                        
       &quot;key&quot; : &quot;device&quot;,                                                                                                
       &quot;description&quot; : &quot;Mir:ror device (ex : /dev/hidraw0)&quot;,                                                            
       &quot;default&quot; : &quot;/dev/hidraw0&quot;},                                                                                     
      {&quot;id&quot; : 2,                                                                                                        
       &quot;key&quot; : &quot;nbmaxtry&quot;,                                                                                              
       &quot;description&quot; : &quot;Max number of tries to open Mir:ror device&quot;,                                                    
       &quot;default&quot; : 5,                                                                                                   
      {&quot;id&quot; : 3,                                                                                                        
       &quot;key&quot; : &quot;interval&quot;,                                                                                              
       &quot;description&quot; : &quot;Delay between each try to open Mir:ror device&quot;,                                                 
       &quot;default&quot; : 10}]                           
{CODE}

The plugin must stop after displaying this.

These informations will be used by Domogik Manager (which at startup will launch each plugin with &quot;config&quot; option) to get informations about plugins. These informations will be get by REST server with /plugin/list/&lt;plugin name&gt; and /plugin/detail/&lt;plugin name&gt; to give informations to UI.

By setting these informations, you will be able to configure your plugin directly from UI!


!!2 - Implement &quot;-f&quot; option 
Without -f option, plugin must launch itself in background.

With -f option, plugin should launch itself on foreground.



!!3 - Stop plugin when requested
When plugin receives this xpl message, it should stop itself.
||TODO : update if it changed||

{CODE()}
DOMOGIK.SYSTEM
{
COMMAND=command to send
HOST=name of the host where a component should be started/stopped
[PLUGIN=name of the plugin concerned by the command]
[FORCE=0||1]
}
{CODE}


!!4 - Get config with xPL queries
At startup, plugin should get configuration from Domogik database. To do this, plugin will ask with a xPL message on network for its configuration. The Database Manager will reply to this request with the config values

||TODO : describe xpl dialog here||


!!5 - Where the plugin should be put ?
||TODO : see if we use an external folder dedicated to non-python plugins||


				