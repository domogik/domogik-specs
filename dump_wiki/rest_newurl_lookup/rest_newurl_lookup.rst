!New URL lookup sequence for rest

!!Old way
have a bunch of if cycle to reach the correct function to call

!!New purposed way

{CODE(caption=&quot;example&quot;,wrap=&quot;0&quot;)}urls = {
        '^//$':                                                                                   'rest_status',
        '^/plugin/list$':                                                                        '_rest_plugin_list',
        '^/plugin/detail/(?P&lt;host&gt;[a-z]+)/(?P&lt;id&gt;[a-z]+)$':                                      '_rest_plugin_detail',
        '^/plugin/dependency/(?P&lt;host&gt;[a-z]+)/(?P&lt;id&gt;[a-z]+)$':                                  '_rest_plugin_dependency',
        '^/plugin/udev-rule/(?P&lt;host&gt;[a-z]+)/(?P&lt;id&gt;[a-z]+)$':                                   '_rest_plugin_udev_rule',
        '^/plugin/(?P&lt;command&gt;enable|disable)/(?P&lt;host&gt;[a-z]+)/(?P&lt;plugin&gt;[a-z]+)$':             '_rest_plugin_enable_disable',
    }
{CODE}

!!!how this works:
when an url is passed to the processRequest class the 'do_for_all_methode' function is called,

this function will test each url inside the above list and see if the passed url is matched to any of them, if its matched it will return an python object with all matched criteria, then the function thats defined as the value for this matched url will be called with all matched parameters:

example 1:
url = /plugin/list
matched items = {}
called function = self._rest_plugin_list()

example 2:
url = /plugin/enable/igor/velbus
matched items = {command: enable, host: igor, plugin: velbus}
called function = self._rest_plugin_enable_disable( command=enable, host=igor, plugin=velbus)