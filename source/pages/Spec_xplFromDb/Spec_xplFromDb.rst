**********************************
Generate XPL messages from the DB
**********************************

.. toctree::


Original idea
==============

((Spec_device_template|Device Template))
DB schema
==========

{IMG(attId="439")}{IMG}
table description
******************

*Device => holds each device known by domogik
*Command => every possible command that can be sent, there can be multiple commands for each device, the command can be an xplcommand if the xpl_command_id is not Null
*Command_param => the needed parameters for this command (typically the result of a widget action)
*xplcommand => if a command is an xplcommand we can find the definition of this xplcommand here, an xpl command can have a xplstat linked to it
*Xplcommand_param => the parameters that have to be in the xpl message, these parameters together with the command parameters will define the xpl message to sent
*XplStat => All xplstat messages that domogic can know. This message can either be linked to a xplCommand or to a sensor
*XplStat_param => the parameters for each xplstat message (used for filtering)
*Sensors => used inside the stat manager define what parameters need to be stored inside the db

Upgrading
==========

Upgrading will be difficult, so everything will be deleted except the device_stats.
We will keep the old devices but will not return them in rets urls (address field should be null to be able to return devices)

The admin can then create the new devices and we will create an upgrade interface, this inetrface will do the folowing
#  link an old device to a new device id
   * /base/device/listold => get all the old devices
   * /base/device/list => will get the new devices
   * /base/sensor/list-by-device => get all sensors for the device
   * /base/migrate/<old dev id>/<new dev id>/<new sensor id>
#  select the sensor to import the data to
#  rest url will insert the data into the the sensor_history table to keep the history

Implementation
===============

Plugin JSON
************

.. code-block:: json

caption="New json for plugins"
    
        {
        "configuration": [
            {
                "default": "False", 
                "description": "Automatically start plugin at Domogik startup", 
                "id": "0", 
                "interface": "no", 
                "key": "startup-plugin", 
                "optionnal": "no", 
                "options": [], 
                "type": "boolean"
            }, 
            {
                "default": "0", 
                "description": "define the connection type to velbus", 
                "id": "1", 
                "interface": "no", 
                "key": "connection-type", 
                "optionnal": "no", 
                "options": [
                    "serial", 
                    "socket"
                ], 
                "type": "enum"
            }, 
            {
                "default": "/dev/ttyACM0", 
                "description": "velbus device (/dev/ttyACM0 for serial, or ip:port for socket", 
                "id": "2", 
                "interface": "no", 
                "key": "device", 
                "optionnal": "no", 
                "options": [], 
                "type": "string"
            }
        ], 
        "xpl_commands": {
             "set_level_bin": {
                "name": "blah",
                "schema": "lighting.basic",
                "xplstat_name": "get_level",
                "parameters": {
                        "static": [
                            {
                                "key": "stat",
                                "value": "stat"
                            }
                        ],
                        "device_type": [
                            {
                                "key": "channel",
                                "description": "The channel number",
                                "type": "integer",
                                "max_value": 4,
                                "min_value": 1
                            },
                            {
                                "key": "address",
                                "description": "The decimal address",
                                "type": "integer",
                                "max_value": 255,
                                "min_value": 0
                            }
                        ],
                        "device": [
                            {
                                "key": "dummy",
                                "description": "a dummy param",
                                "type": "string"
                            }
                        ]
                    }
             },
             "set_level_range": {
                "name": "set_level_range",
                "schema": "lighting.basic",
                "xplstat_name": "get_level",
                "parameters": {
                        "static": [
                            {
                                "key": "stat",
                                "value": "stat"
                            }
                         ],
                        "device_type": [
                            {
                                "key": "channel",
                                "description": "The channel number",
                                "type": "integer",
                                "max_value": 4,
                                "min_value": 1
                            },
                            {
                                "key": "address",
                                "description": "The decimal address",
                                "type": "integer",
                                "max_value": 255,
                                "min_value": 0
                            }
                        ],
                        "device": []
                    }
             }
        },
        "xpl_stats": {
           "get_level": {
                "name": "get_level",
                "schema": "lighting.device",
                "parameters": {
                        "static": [
                            {
                                "key": "stat",
                                "value": "stat"
                            }
                        ],
                        "device_type": [
                            {
                                "key": "channel",
                                "description": "The channel number",
                                "type": "integer",
                                "max_value": 4,
                                "min_value": 1
                            },
                            {
                                "key": "address",
                                "description": "The decimal address",
                                "type": "integer",
                                "max_value": 255,
                                "min_value": 0
                            }
                        ],
                        "device": [],
                        "dynamic": [
                            {
                                 "key": "level",
                                 "sensor": "level"
                            }
                        ]
                    }
           }
        },
        "commands": {
           "set_level_bin": {
               "name": "Switch On or Off",
               "return_confirmation": true,
               "params": [
                   {
                       "key": "level",
                       "value_type": "binary",
                       "values": [0, 255]
                   }
               ],
               "xpl_command": "set_level_bin"
            },
            "set_level_range": {
               "name": "Set to a level",
               "return_confirmation": true,
               "params": [
                   {
                       "key": "level",
                       "value_type": "range",
                       "values": [0, 255]
                   }
               ],
               "xpl_command": "set_level_bin"
            }
        },
        "sensors": {
    	"level": {
    		"name": "level",
                    "unit": "%",
                    "value_type": "range",
                    "values": [0, 100]
    	}
        },
        "device_types": {
            "velbus.relay": {
                "id": "velbus.relay",
                "description": "Switch one channel on a device", 
                "name": "Switch",
                "commands": ["set_level_bin"],
                "sensors": ["level"]
            }, 
            "velbus.dimmer": {
                "id": "velbus.dimmer",
                "description": "Dim one channel on a device", 
                "id": "velbus.dimmer", 
                "name": "Dimmer",
                "commands": ["set_level_bin", "set_level_range"],
                "sensors": ["level"]
            }, 
            "velbus.shutter": {
                "id": "velbus.shutter",
                "description": "Shutter control (up, down)", 
                "name": "Shutter",
                "xpl_commands": ["set_blind"]
            },
            "velbus.temp": {
                "id": "velbus.temp",
                "description": "Temperature Sensor", 
                "name": "Temperature"
            },
            "velbus.input": {
                "id": "velbus.input",
                "description": "Input contact", 
                "name": "Input"
            }
        }, 
        "files": [
            "src/share/domogik/plugins/velbus.json", 
            "src/share/domogik/design/plugin/velbus/icon.png", 
            "src/domogik_packages/xpl/bin/velbus.py", 
            "src/domogik_packages/xpl/lib/velbus.py", 
            "src/domogik_packages/xpl/helper/velbus.py"
        ], 
        "identity": {
            "author": "Maikel Punie", 
            "author_email": "maikel.puni@gmail.com", 
            "category": "velbus", 
            "changelog": "0.1.0\n- relays only\n- serial comunication only \n0.2.0\n- added socket comunication\n0.3.0\n- added dimmer support\n0.4.0\n- added blind (up/down) support\n0.5.0\n- added temperature sensor support", 
            "dependencies": [
                {
                    "id": "pyserial (>=2.6)", 
                    "type": "python"
                }
            ], 
            "description": "velbus interface", 
            "documentation": "http://wiki.domogik.org/plugin_velbus", 
            "domogik_min_version": "0.2.0", 
            "id": "velbus", 
            "type": "plugin", 
            "version": "0.5.0"
        }, 
        "json_version": 2, 
        "technology": {
            "description": "Velbus http://www.velbus.eu", 
            "id": "velbus", 
            "name": "Velbus"
        }, 
        "udev-rules": [
            {
                "description": "Velbus USB interface", 
                "filename": "velbus.rules", 
                "model": "VMB1USB", 
                "rule": "SUBSYSTEM==\"tty\" ATTRS(manufacturer)==\"Velleman Projects\" ATTRS{product}==\"VMB1USB Velbus USB interface\" SYMLINK+=\"velbus\" MODE=\"0666\""
            }
        ]
    }
    



Command sending
****************


a new rest url is created
.. code-block:: json


    /cmd/<command Id>/<param 1>/<val 1>/.../<param N>/<val N>{CODE}
    
    The param fields have to match the fields inside command_param table for the given command id.
    
    If the command has an associated XPL command then the xplcommand will be sent onto the network using the parameters from the commd_param table together with the parameters from the xplcommand table
    
     GUI add device steps
    **********************
    
    #select the correct device_type
    #rinor will request the device specifick parameters (device section in json file) for the needed commands and for the needed stats (/base/device/params/<device_type>)
    #display the input fields for this device
    #add the device (/base/device/add), this will create the needed commands, xplcommands, xplstats and sensors
    #add the devicetype parameters (/base/device/addglobal), this will append these parameters to all xplmessages associated with the device
    #add the device specifick parameters to a specifick xpl command or xplstat (/base/device/xpl(COMMAND|STAT)params/
    
    Admin urls
    ***********
    
    
    */plugin/json/<id>
    */base/device/params/(?P<dev_type_id>[\.a-z0-9]+)
.. code-block:: json


    {
           "status": "OK",
           "code": 0,
           "description": "None",
           "deviceparams":
           [
               {
                   "xpl_stat":
                   [
                       {
                           "params":
                           [
                           ],
                           "name": "get_level",
                           "schema": "lighting.device"
                       },
                       {
                           "params":
                           [
                           ],
                           "name": "get_level",
                           "schema": "lighting.device"
                       }
                   ],
                   "xpl_cmd":
                   [
                       {
                           "params":
                           [
                               {
                                   "type": "string",
                                   "description": "a dummy param",
                                   "key": "dummy"
                               }
                           ],
                           "xplstat_name": "get_level",
                           "name": "set_level_bin",
                           "schema": "lighting.basic"
                       },
                       {
                           "params":
                           [
                               {
                                   "type": "string",
                                   "description": "a dummy param",
                                   "key": "dummy"
                               }
                           ],
                           "xplstat_name": "get_level",
                           "name": "set_level_bin",
                           "schema": "lighting.basic"
                       }
                   ],
                   "global":
                   [
                       {
                           "max_value": 4,
                           "min_value": 1,
                           "type": "integer",
                           "description": "The channel number",
                           "key": "channel"
                       },
                       {
                           "max_value": 255,
                           "min_value": 0,
                           "type": "integer",
                           "description": "The decimal address",
                           "key": "address"
                       }
                   ]
               }
           ]
        }

*/base/device/add => will add a device and the xpl command + stats into the db
/base/device/params/(?P<dev_type_id>[\.a-z0-9]+) => will return the needed parameters for this device type
*/base/device/addglobal/id/(?P<id>[0-9]+)/.* => will add the 'device_type' parameters to every command/stat message
*/base/device/xplcmdparams/id/(?P<id>[0-9]+)/<key1>/<value1>/... => will addd the key/value pairs to the xpl command
*/base/device/xplstatparams/id/(?P<id>[0-9]+)/<key1>/<value1>/... => will addd the key/value pairs to the xpl stat message
*/cmd/id/<id>/<key1>/<value1>/<key2>/<value2>/.... => sends out the xplcommand

the urls below need an update (not a fixed format yet)
*/base/xplcommand/add/schema/<schema>/reference/<ref>/device_id/<devid>/stat_id/<statid>
*/base/xplstat/add/schema/<schema>/reference/<ref>/device_id/<devid>/
*/base/xplcommandparam/add/stat_id/<statId>/key/<key>/value/<value>/static/<static>
*/base/xplstatparam/add/stat_id/<statId>/key/<key>/value/<value>/static/<static>
*/base/xplcommand/update/id/<id>/schema/<schema>/reference/<ref>/device_id/<devid>/stat_id/<statid>
*/base/xplstat/udpate/id/<id>/schema/<schema>/reference/<ref>/device_id/<devid>/
*/base/xplcommandparam/update/stat_id/<statId>/key/<key>/value/<value>/static/<static>
*/base/xplstatparam/update/stat_id/<statId>/key/<key>/value/<value>/static/<static>
*/base/xplcommand/delete/id/<id>
*/base/xplstat/delete/id/<id>
*/base/xplcommandparam/delete/stat_id/<statId>/key/<key>
*/base/xplstatparam/delete/stat_id/<statId>/key/<key>