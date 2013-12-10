There are a few things to avoid to make sure your plugin will stop correctly :
* No 'While True'
* No 'sleep(xx)'

The first one will never end, the second one will hang during xx seconds even if we asked the plugin to stop.

All the plugins have a method .. code-block:: json


    get_stop(){CODE} provided by XplPlugin class that they extends from.
    This method returns a ''threading.Event'' instance which is set when the plugin is asked to stop.
    
    So, to use it, replace :
.. code-block:: json

wrap="1", pythonln=""
    while True:
        do something


with :

.. code-block:: json

wrap="1", pythonln=""
    while not self.get_stop().isSet():
        do something


And :

.. code-block:: json

wrap="1", pythonln=""
    sleep(xx){CODE}
    
    with :
.. code-block:: json

wrap="1", pythonln=""
    self.get_stop().wait(xx){CODE}

which will exit as soon as the Event is set, whereas sleep() will wait the whole time.
'''NOTE : '''If you need to use such a feature in the library part of your plugin, you can do something like : 

* In bin/myplugin.py :
.. code-block:: json

colors='python'
    
    from domogik.xpl.common import XplPlugin
    from domogik.xpl.lib import myplugin
    
    
    class MyPlugin(XplPlugin):
        def __init__(self):
            self._mypluginlib = myplugin.MyPluginLib(some,other,param,self.get_stop())
    
    


* in lib/myplugin.py :
.. code-block:: json

colors='python'
    
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
    


Extra things to do when shutting down
======================================

If you need to do some more things when your plugins shutdowns, you can use the ''add_stop_cb'' method provided by the XplPlugin class. For example : 
* In bin/myplugin.py :
.. code-block:: json

colors='python'
    
    from domogik.xpl.common import XplPlugin
    from domogik.xpl.lib import myplugin
    
    
    class MyPlugin(XplPlugin):
        def __init__(self):
            self._mypluginlib = myplugin.MyPluginLib(some,other,param)
            self.add_stop_cb(self._mypluginlib.stop)
    
    


* in lib/myplugin.py :
.. code-block:: json

colors='python'
    
    class MyPluginLib:
        def __init__(self, some, other, param):
            self._some = some
            self._other = other
            self._param = param
    
        def stop(self):
            do something here, like close your serial port or network socket or ...
    
