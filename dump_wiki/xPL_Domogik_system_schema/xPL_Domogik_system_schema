!System schema of Domogik in xPL
{maketoc}

!!xPL dialog between REST and Manager
!!!Command
xpl-cmnd :
{CODE()}
DOMOGIK.SYSTEM
{
COMMAND=command to send
HOST=name of the host where a component should be started/stopped
[PLUGIN=name of the plugin concerned by the command]
}
{CODE}

COMMAND can have one of the following values : 
* start
* stop
* list
* detail
* enable
* disable

!!!Common features
To start and stop features : 
{CODE()}
xpl-trig 
{
...
}
DOMOGIK.SYSTEM
{
COMMAND=&lt;start|stop&gt;
HOST=Host sending the message
[PLUGIN=name of the plugin concerned by the command)
[ERROR=error|message if error occurs, 255 char max]
}
{CODE}

!!!List features
xpl-trig format : 
{CODE()}
DOMOGIK.SYSTEM
{
COMMAND=LIST
HOST = Host sending the message
[PLUGIN0-TYPE = &lt;type : plugin, hardware&gt;]
[PLUGIN0-NAME = &lt;name&gt;]
[PLUGIN0-TECHNO = &lt;technology&gt;]
[PLUGIN0-STATUS = &lt;status&gt;]
[PLUGIN0-HOST = &lt;host&gt;]
[PLUGIN1-TYPE = ]
[PLUGIN1-NAME = ]
[PLUGIN1-TECHN0 = ]
[PLUGIN1-STATUS = ]
[PLUGIN1-HOST = ]
...
}
{CODE}

!!!Detail of a feature

xpl-trig format : 
{CODE()}
DOMOGIK.SYSTEM
{
COMMAND=DETAIL
HOST = &lt;Plugin host&gt;
PLUGIN-NAME = &lt;plugin name&gt;
TECHNOLOGY = &lt;plugin technology&gt;
DESCRIPTION0 = &lt;plugin description part 0&gt;
[DESCRIPTION1 = &lt;plugin description part 1&gt;]
[...]
[DESCRIPTIONN = &lt;plugin description part N&gt;]
STATUS = &lt;plugin status&gt;
VERSION = &lt;plugin version&gt;
DOCUMENTATION = &lt;plugin link to find documentation&gt;
[CFG0-KEY = &lt;key&gt;]
[CFG0-TYPE = &lt;key type (boolean, string, number, list)&gt;]
[CFG0-DESC = &lt;key description&gt;]
[CFG0-LIST = &lt;values for list separated by comma (only if TYPE = &quot;LIST/list&quot;)&gt;]
[CFG0-DEFAULT = &lt;default value for key&gt;]
[CFG0-INT = &lt;yes | no : is config item an element of the interface ?&gt;]
[CFG0-OPT = &lt;yes | no : is it an optionnal element (for info only) ?&gt;]
[CFG1-KEY = ]
[CFG1-TYPE = ]
[CFG1-DESC = ]
[CFG1-LIST = ]
[CFG1-DEFAULT = ]
[CFG1-INT = ]
[CFG1-OPT = ]

}
{CODE}

__Important notice : only one group is allowed__

__Important notice : key 'nb-int' is used to register number of defined interfaces for UI display and xPL usage. See REST /plugin/config/* methods for UI usage and Query.config for plugins usage.__

!!!Enable/disable plugins on a host
Command :
{CODE()}
xpl-cmnd
{
}
domogik.system
{
command=&lt;enable|disable&gt;
host=&lt;target host&gt;
plugin=&lt;name&gt;
}
{CODE}

Response :
{CODE()}
xpl-cmnd
{
}
domogik.package
{
command=&lt;enable|disable&gt;
host=&lt;target host&gt;
plugin=&lt;name&gt;
[error = &lt;error message&gt;]
}
{CODE}

!!xPL dialog between REST and Manager --- hardware specific
!!!Detail of the feature
Notice : this evolution is made because hardware detail gives information about hardware (real and read only info) : for plugins, the detail gives a list of parameters and the possibility to set them. Moreover, a hardware can't be started/stopped, so related buttons are not needed.

New xpl-trig format : 
{CODE()}
DOMOGIK.SYSTEM
{
COMMAND=DETAIL
HOST = &lt;Hardware host&gt;
PLUGIN = &lt;plugin name&gt;
TECHNOLOGY = &lt;plugin technology&gt;
DESCRIPTION = &lt;plugin description&gt;
STATUS = &lt;plugin status&gt;
VERSION = &lt;plugin version&gt;
DOCUMENTATION = &lt;plugin link to find documentation&gt;
[CFG0-KEY = &lt;key&gt;]
[CFG0-VALUE = &lt;value&gt;]
[CFG1-KEY = ]
[CFG1-VALUE = ]
...
}
{CODE}