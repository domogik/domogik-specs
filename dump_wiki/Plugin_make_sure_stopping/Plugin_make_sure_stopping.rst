There are a few things to avoid to make sure your plugin will stop correctly :
* No 'While True'
* No 'sleep(xx)'

The first one will never end, the second one will hang during xx seconds even if we asked the plugin to stop.

All the plugins have a method {CODE()}get_stop(){CODE} provided by XplPlugin class that they extends from.
This method returns a ''threading.Event'' instance which is set when the plugin is asked to stop.

So, to use it, replace :
{CODE(wrap=&quot;1&quot;,colors=&quot;python&quot;,ln=&quot;&quot;)}while True:
    do something{CODE}

with :

{CODE(wrap=&quot;1&quot;,colors=&quot;python&quot;,ln=&quot;&quot;)}while not self.get_stop().isSet():
    do something{CODE}

And :

{CODE(wrap=&quot;1&quot;,colors=&quot;python&quot;,ln=&quot;&quot;)}sleep(xx){CODE}

with :
{CODE(wrap=&quot;1&quot;,colors=&quot;python&quot;,ln=&quot;&quot;)}self.get_stop().wait(xx){CODE}

which will exit as soon as the Event is set, whereas sleep() will wait the whole time.
'''NOTE : '''If you need to use such a feature in the library part of your plugin, you can do something like : 

* In bin/myplugin.py :
{CODE(colors='python')}
from domogik.xpl.common import XplPlugin
from domogik.xpl.lib import myplugin


class MyPlugin(XplPlugin):
    def __init__(self):
        self._mypluginlib = myplugin.MyPluginLib(some,other,param,self.get_stop())

{CODE}

* in lib/myplugin.py :
{CODE(colors='python')}
class MyPluginLib:
    def __init__(self, some, other, param, stop):
        self._some = some
        self._other = other
        self._param = param
        self._stop = stop

    def some_method(self):
        while not self._stop.isSet():
            do something
            self._stop.wait(xx)
{CODE}

!!Extra things to do when shutting down
If you need to do some more things when your plugins shutdowns, you can use the ''add_stop_cb'' method provided by the XplPlugin class. For example : 
* In bin/myplugin.py :
{CODE(colors='python')}
from domogik.xpl.common import XplPlugin
from domogik.xpl.lib import myplugin


class MyPlugin(XplPlugin):
    def __init__(self):
        self._mypluginlib = myplugin.MyPluginLib(some,other,param)
        self.add_stop_cb(self._mypluginlib.stop)

{CODE}

* in lib/myplugin.py :
{CODE(colors='python')}
class MyPluginLib:
    def __init__(self, some, other, param):
        self._some = some
        self._other = other
        self._param = param

    def stop(self):
        do something here, like close your serial port or network socket or ...
{CODE}