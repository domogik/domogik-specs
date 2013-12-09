Domogik implements logging features, so you must use them when you develop your own plugin.

!Minimal requirement 
Here, we want ot use default log file : myplugin.log.

First, you have to include XplPlugin (your plugin main class will inherit from it) and logger which wil provide you access to logging features :
{CODE(colors='python')}
from domogik.xpl.common.plugin import XplPlugin           
{CODE}

Then, as usual, declare your plugin (xpl/bin/&lt;myplugin&gt;.py) as an inheritance of XplPlugin :
{CODE(colors='python')}
class MyPlugin(XplPlugin):                       
{CODE}

And in your ___init___() function, after calling XplPlugin.___init___() as usual and you can access log feature directly with self.log :
{CODE(colors='python')}
    def __init__(self):
        XplPlugin.__init__(self, name = 'myplugin')

        # log info
        self.log.info(&quot;This is an info&quot;)
        self.log.debug(&quot;This is debug&quot;)  
        self.log.warning(&quot;This is a warning&quot;) 
        self.log.error(&quot;This is an error&quot;) 
{CODE}

Next, in order to be able to log from your plugin lib part (xpl/lib/myplugin.py), simply pass self.log as an argument to your __init__ functions of your library classes ;)

!Advanced usage
When you want to use more than one log file, you can declare a new logger like this : 
{CODE(colors='python')}
log_new = logger.Logger('myplugin-newlog')
self._log_new = log_new.get_logger()
self._log_new.info(&quot;This is an info&quot;)
{CODE}

!Things to know
There is no need for you to write a dedicated log line to indicate that plugin is starting. Call to XplPlugin._init_ will do this like this :
{CODE()}
2010-06-18 10:48:08,585 domogik-myplugin INFO ----------------------------------
2010-06-18 10:48:08,585 domogik-myplugin INFO Starting plugin 'myplugin' (new manager instance)
{CODE}