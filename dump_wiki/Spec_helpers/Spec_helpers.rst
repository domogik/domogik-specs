*********************************************
Specs of helpers that will use the MQ system
*********************************************
||__Created:__|07/04/2013
__Creator:__|Cereal
__Reviewers:__|
__Status:__|{GAUGE(value=>10, max=>100, label=>''draft'', perc=>true, labelsize=>50, height=>20, color=>green, bgcolor=>#EEEEEE)}{GAUGE}
__Target:__|
__References:__| ||

.. toctree::



problems with current helpers
==============================
there are a few problems with the current helpers, i'll try to create a list here

*usage of the xpl network
*the plugin needs to be stopped (if the plugin uses the same hardware)


idea
=====
the new helpers will use the mq message system (req/rep), the plugins will be a mq worker, so they can respond to a mq request. This way the plugin can keep running, and over an mq message a certain helper request comes in to do a certain action on the plugin. The plugin can then just call some internal procedures to access the same hardware as the plugin does.

This gives some advantages:
#the plugin can run at the same time as the helper (its actually the same code)
#the system doesn't use the xpl network

req/rep messages
=================

action: helper.*
data will be a json with some key/values that are specifick to the helper action

helper.list
************
request: from ui to plugin
action: helper.list
data: None
=> returns a list of possible helper actions

helper.do
**********
request: from ui to plugin
action: helper.do
data:
*command = a command that was returned by the helper
* data = a key/value pair of the params needed for this command

helper.help
************
request: from ui to plugin
action: helper.help
data:
*None => display full help
or
*comand = a command from list => display the help for this command

helper.result
**************
reply: fromplugin to ui
action: helper.result
data:
*request => the action where this is the result for
*data => the resulting data
