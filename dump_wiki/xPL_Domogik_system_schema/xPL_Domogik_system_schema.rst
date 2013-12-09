********************************
System schema of Domogik in xPL
********************************
.. toctree::



xPL dialog between REST and Manager
====================================
Command
********
xpl-cmnd :
.. code-block::
    
    DOMOGIK.SYSTEM
    {
    COMMAND=command to send
    HOST=name of the host where a component should be started/stopped
    [PLUGIN=name of the plugin concerned by the command]
    }
    


COMMAND can have one of the following values : 
* start
* stop
* list
* detail
* enable
* disable

Common features
****************
To start and stop features : 
.. code-block::
    
    xpl-trig 
    {
    ...
    }
    DOMOGIK.SYSTEM
    {
    COMMAND=<start|stop>
    HOST=Host sending the message
    [PLUGIN=name of the plugin concerned by the command)
    [ERROR=error|message if error occurs, 255 char max]
    }
    


List features
**************
xpl-trig format : 
.. code-block::
    
    DOMOGIK.SYSTEM
    {
    COMMAND=LIST
    HOST = Host sending the message
    [PLUGIN0-TYPE = <type : plugin, hardware>]
    [PLUGIN0-NAME = <name>]
    [PLUGIN0-TECHNO = <technology>]
    [PLUGIN0-STATUS = <status>]
    [PLUGIN0-HOST = <host>]
    [PLUGIN1-TYPE = ]
    [PLUGIN1-NAME = ]
    [PLUGIN1-TECHN0 = ]
    [PLUGIN1-STATUS = ]
    [PLUGIN1-HOST = ]
    ...
    }
    


Detail of a feature
********************

xpl-trig format : 
.. code-block::
    
    DOMOGIK.SYSTEM
    {
    COMMAND=DETAIL
    HOST = <Plugin host>
    PLUGIN-NAME = <plugin name>
    TECHNOLOGY = <plugin technology>
    DESCRIPTION0 = <plugin description part 0>
    [DESCRIPTION1 = <plugin description part 1>]
    [...]
    [DESCRIPTIONN = <plugin description part N>]
    STATUS = <plugin status>
    VERSION = <plugin version>
    DOCUMENTATION = <plugin link to find documentation>
    [CFG0-KEY = <key>]
    [CFG0-TYPE = <key type (boolean, string, number, list)>]
    [CFG0-DESC = <key description>]
    [CFG0-LIST = <values for list separated by comma (only if TYPE = "LIST/list")>]
    [CFG0-DEFAULT = <default value for key>]
    [CFG0-INT = <yes | no : is config item an element of the interface ?>]
    [CFG0-OPT = <yes | no : is it an optionnal element (for info only) ?>]
    [CFG1-KEY = ]
    [CFG1-TYPE = ]
    [CFG1-DESC = ]
    [CFG1-LIST = ]
    [CFG1-DEFAULT = ]
    [CFG1-INT = ]
    [CFG1-OPT = ]
    
    }
    


__Important notice : only one group is allowed__

__Important notice : key 'nb-int' is used to register number of defined interfaces for UI display and xPL usage. See REST /plugin/config/* methods for UI usage and Query.config for plugins usage.__

Enable/disable plugins on a host
*********************************
Command :
.. code-block::
    
    xpl-cmnd
    {
    }
    domogik.system
    {
    command=<enable|disable>
    host=<target host>
    plugin=<name>
    }
    


Response :
.. code-block::
    
    xpl-cmnd
    {
    }
    domogik.package
    {
    command=<enable|disable>
    host=<target host>
    plugin=<name>
    [error = <error message>]
    }
    


xPL dialog between REST and Manager --- hardware specific
==========================================================
Detail of the feature
**********************
Notice : this evolution is made because hardware detail gives information about hardware (real and read only info) : for plugins, the detail gives a list of parameters and the possibility to set them. Moreover, a hardware can't be started/stopped, so related buttons are not needed.

New xpl-trig format : 
.. code-block::
    
    DOMOGIK.SYSTEM
    {
    COMMAND=DETAIL
    HOST = <Hardware host>
    PLUGIN = <plugin name>
    TECHNOLOGY = <plugin technology>
    DESCRIPTION = <plugin description>
    STATUS = <plugin status>
    VERSION = <plugin version>
    DOCUMENTATION = <plugin link to find documentation>
    [CFG0-KEY = <key>]
    [CFG0-VALUE = <value>]
    [CFG1-KEY = ]
    [CFG1-VALUE = ]
    ...
    }
    
