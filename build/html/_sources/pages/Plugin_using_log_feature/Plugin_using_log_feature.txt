Domogik implements logging features, so you must use them when you develop your own plugin.

*********************
Minimal requirement 
*********************

Here, we want ot use default log file : myplugin.log.

First, you have to include XplPlugin (your plugin main class will inherit from it) and logger which wil provide you access to logging features :
.. code-block:: json

colors='python'
    
    from domogik.xpl.common.plugin import XplPlugin           
    


Then, as usual, declare your plugin (xpl/bin/<myplugin>.py) as an inheritance of XplPlugin :
.. code-block:: json

colors='python'
    
    class MyPlugin(XplPlugin):                       
    


And in your ___init___() function, after calling XplPlugin.___init___() as usual and you can access log feature directly with self.log :
.. code-block:: json

colors='python'
    
        def __init__(self):
            XplPlugin.__init__(self, name = 'myplugin')
    
            # log info
            self.log.info("This is an info")
            self.log.debug("This is debug")  
            self.log.warning("This is a warning") 
            self.log.error("This is an error") 
    


Next, in order to be able to log from your plugin lib part (xpl/lib/myplugin.py), simply pass self.log as an argument to your __init__ functions of your library classes ;)

***************
Advanced usage
***************

When you want to use more than one log file, you can declare a new logger like this : 
.. code-block:: json

colors='python'
    
    log_new = logger.Logger('myplugin-newlog')
    self._log_new = log_new.get_logger()
    self._log_new.info("This is an info")
    


***************
Things to know
***************

There is no need for you to write a dedicated log line to indicate that plugin is starting. Call to XplPlugin._init_ will do this like this :
.. code-block:: json


    
    2010-06-18 10:48:08,585 domogik-myplugin INFO ----------------------------------
    2010-06-18 10:48:08,585 domogik-myplugin INFO Starting plugin 'myplugin' (new manager instance)
    
