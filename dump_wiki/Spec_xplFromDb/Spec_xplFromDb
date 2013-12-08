!Generate XPL messages from the DB
{maketoc}
!!Original idea
((Spec_device_template|Device Template))
!!DB schema
{IMG(attId=&quot;439&quot;)}{IMG}
!!!table description
*Device =&gt; holds each device known by domogik
*Command =&gt; every possible command that can be sent, there can be multiple commands for each device, the command can be an xplcommand if the xpl_command_id is not Null
*Command_param =&gt; the needed parameters for this command (typically the result of a widget action)
*xplcommand =&gt; if a command is an xplcommand we can find the definition of this xplcommand here, an xpl command can have a xplstat linked to it
*Xplcommand_param =&gt; the parameters that have to be in the xpl message, these parameters together with the command parameters will define the xpl message to sent
*XplStat =&gt; All xplstat messages that domogic can know. This message can either be linked to a xplCommand or to a sensor
*XplStat_param =&gt; the parameters for each xplstat message (used for filtering)
*Sensors =&gt; used inside the stat manager define what parameters need to be stored inside the db

!!Upgrading
Upgrading will be difficult, so everything will be deleted except the device_stats.
We will keep the old devices but will not return them in rets urls (address field should be null to be able to return devices)

The admin can then create the new devices and we will create an upgrade interface, this inetrface will do the folowing
#  link an old device to a new device id
   * /base/device/listold =&gt; get all the old devices
   * /base/device/list =&gt; will get the new devices
   * /base/sensor/list-by-device =&gt; get all sensors for the device
   * /base/migrate/&lt;old dev id&gt;/&lt;new dev id&gt;/&lt;new sensor id&gt;
#  select the sensor to import the data to
#  rest url will insert the data into the the sensor_history table to keep the history

!!Implementation
!!!Plugin JSON
{CODE(caption=&quot;New json for plugins&quot;)}
    {
    &quot;configuration&quot;: [
        {
            &quot;default&quot;: &quot;False&quot;, 
            &quot;description&quot;: &quot;Automatically start plugin at Domogik startup&quot;, 
            &quot;id&quot;: &quot;0&quot;, 
            &quot;interface&quot;: &quot;no&quot;, 
            &quot;key&quot;: &quot;startup-plugin&quot;, 
            &quot;optionnal&quot;: &quot;no&quot;, 
            &quot;options&quot;: [], 
            &quot;type&quot;: &quot;boolean&quot;
        }, 
        {
            &quot;default&quot;: &quot;0&quot;, 
            &quot;description&quot;: &quot;define the connection type to velbus&quot;, 
            &quot;id&quot;: &quot;1&quot;, 
            &quot;interface&quot;: &quot;no&quot;, 
            &quot;key&quot;: &quot;connection-type&quot;, 
            &quot;optionnal&quot;: &quot;no&quot;, 
            &quot;options&quot;: [
                &quot;serial&quot;, 
                &quot;socket&quot;
            ], 
            &quot;type&quot;: &quot;enum&quot;
        }, 
        {
            &quot;default&quot;: &quot;/dev/ttyACM0&quot;, 
            &quot;description&quot;: &quot;velbus device (/dev/ttyACM0 for serial, or ip:port for socket&quot;, 
            &quot;id&quot;: &quot;2&quot;, 
            &quot;interface&quot;: &quot;no&quot;, 
            &quot;key&quot;: &quot;device&quot;, 
            &quot;optionnal&quot;: &quot;no&quot;, 
            &quot;options&quot;: [], 
            &quot;type&quot;: &quot;string&quot;
        }
    ], 
    &quot;xpl_commands&quot;: {
         &quot;set_level_bin&quot;: {
            &quot;name&quot;: &quot;blah&quot;,
            &quot;schema&quot;: &quot;lighting.basic&quot;,
            &quot;xplstat_name&quot;: &quot;get_level&quot;,
            &quot;parameters&quot;: {
                    &quot;static&quot;: [
                        {
                            &quot;key&quot;: &quot;stat&quot;,
                            &quot;value&quot;: &quot;stat&quot;
                        }
                    ],
                    &quot;device_type&quot;: [
                        {
                            &quot;key&quot;: &quot;channel&quot;,
                            &quot;description&quot;: &quot;The channel number&quot;,
                            &quot;type&quot;: &quot;integer&quot;,
                            &quot;max_value&quot;: 4,
                            &quot;min_value&quot;: 1
                        },
                        {
                            &quot;key&quot;: &quot;address&quot;,
                            &quot;description&quot;: &quot;The decimal address&quot;,
                            &quot;type&quot;: &quot;integer&quot;,
                            &quot;max_value&quot;: 255,
                            &quot;min_value&quot;: 0
                        }
                    ],
                    &quot;device&quot;: [
                        {
                            &quot;key&quot;: &quot;dummy&quot;,
                            &quot;description&quot;: &quot;a dummy param&quot;,
                            &quot;type&quot;: &quot;string&quot;
                        }
                    ]
                }
         },
         &quot;set_level_range&quot;: {
            &quot;name&quot;: &quot;set_level_range&quot;,
            &quot;schema&quot;: &quot;lighting.basic&quot;,
            &quot;xplstat_name&quot;: &quot;get_level&quot;,
            &quot;parameters&quot;: {
                    &quot;static&quot;: [
                        {
                            &quot;key&quot;: &quot;stat&quot;,
                            &quot;value&quot;: &quot;stat&quot;
                        }
                     ],
                    &quot;device_type&quot;: [
                        {
                            &quot;key&quot;: &quot;channel&quot;,
                            &quot;description&quot;: &quot;The channel number&quot;,
                            &quot;type&quot;: &quot;integer&quot;,
                            &quot;max_value&quot;: 4,
                            &quot;min_value&quot;: 1
                        },
                        {
                            &quot;key&quot;: &quot;address&quot;,
                            &quot;description&quot;: &quot;The decimal address&quot;,
                            &quot;type&quot;: &quot;integer&quot;,
                            &quot;max_value&quot;: 255,
                            &quot;min_value&quot;: 0
                        }
                    ],
                    &quot;device&quot;: []
                }
         }
    },
    &quot;xpl_stats&quot;: {
       &quot;get_level&quot;: {
            &quot;name&quot;: &quot;get_level&quot;,
            &quot;schema&quot;: &quot;lighting.device&quot;,
            &quot;parameters&quot;: {
                    &quot;static&quot;: [
                        {
                            &quot;key&quot;: &quot;stat&quot;,
                            &quot;value&quot;: &quot;stat&quot;
                        }
                    ],
                    &quot;device_type&quot;: [
                        {
                            &quot;key&quot;: &quot;channel&quot;,
                            &quot;description&quot;: &quot;The channel number&quot;,
                            &quot;type&quot;: &quot;integer&quot;,
                            &quot;max_value&quot;: 4,
                            &quot;min_value&quot;: 1
                        },
                        {
                            &quot;key&quot;: &quot;address&quot;,
                            &quot;description&quot;: &quot;The decimal address&quot;,
                            &quot;type&quot;: &quot;integer&quot;,
                            &quot;max_value&quot;: 255,
                            &quot;min_value&quot;: 0
                        }
                    ],
                    &quot;device&quot;: [],
                    &quot;dynamic&quot;: [
                        {
                             &quot;key&quot;: &quot;level&quot;,
                             &quot;sensor&quot;: &quot;level&quot;
                        }
                    ]
                }
       }
    },
    &quot;commands&quot;: {
       &quot;set_level_bin&quot;: {
           &quot;name&quot;: &quot;Switch On or Off&quot;,
           &quot;return_confirmation&quot;: true,
           &quot;params&quot;: [
               {
                   &quot;key&quot;: &quot;level&quot;,
                   &quot;value_type&quot;: &quot;binary&quot;,
                   &quot;values&quot;: [0, 255]
               }
           ],
           &quot;xpl_command&quot;: &quot;set_level_bin&quot;
        },
        &quot;set_level_range&quot;: {
           &quot;name&quot;: &quot;Set to a level&quot;,
           &quot;return_confirmation&quot;: true,
           &quot;params&quot;: [
               {
                   &quot;key&quot;: &quot;level&quot;,
                   &quot;value_type&quot;: &quot;range&quot;,
                   &quot;values&quot;: [0, 255]
               }
           ],
           &quot;xpl_command&quot;: &quot;set_level_bin&quot;
        }
    },
    &quot;sensors&quot;: {
	&quot;level&quot;: {
		&quot;name&quot;: &quot;level&quot;,
                &quot;unit&quot;: &quot;%&quot;,
                &quot;value_type&quot;: &quot;range&quot;,
                &quot;values&quot;: [0, 100]
	}
    },
    &quot;device_types&quot;: {
        &quot;velbus.relay&quot;: {
            &quot;id&quot;: &quot;velbus.relay&quot;,
            &quot;description&quot;: &quot;Switch one channel on a device&quot;, 
            &quot;name&quot;: &quot;Switch&quot;,
            &quot;commands&quot;: [&quot;set_level_bin&quot;],
            &quot;sensors&quot;: [&quot;level&quot;]
        }, 
        &quot;velbus.dimmer&quot;: {
            &quot;id&quot;: &quot;velbus.dimmer&quot;,
            &quot;description&quot;: &quot;Dim one channel on a device&quot;, 
            &quot;id&quot;: &quot;velbus.dimmer&quot;, 
            &quot;name&quot;: &quot;Dimmer&quot;,
            &quot;commands&quot;: [&quot;set_level_bin&quot;, &quot;set_level_range&quot;],
            &quot;sensors&quot;: [&quot;level&quot;]
        }, 
        &quot;velbus.shutter&quot;: {
            &quot;id&quot;: &quot;velbus.shutter&quot;,
            &quot;description&quot;: &quot;Shutter control (up, down)&quot;, 
            &quot;name&quot;: &quot;Shutter&quot;,
            &quot;xpl_commands&quot;: [&quot;set_blind&quot;]
        },
        &quot;velbus.temp&quot;: {
            &quot;id&quot;: &quot;velbus.temp&quot;,
            &quot;description&quot;: &quot;Temperature Sensor&quot;, 
            &quot;name&quot;: &quot;Temperature&quot;
        },
        &quot;velbus.input&quot;: {
            &quot;id&quot;: &quot;velbus.input&quot;,
            &quot;description&quot;: &quot;Input contact&quot;, 
            &quot;name&quot;: &quot;Input&quot;
        }
    }, 
    &quot;files&quot;: [
        &quot;src/share/domogik/plugins/velbus.json&quot;, 
        &quot;src/share/domogik/design/plugin/velbus/icon.png&quot;, 
        &quot;src/domogik_packages/xpl/bin/velbus.py&quot;, 
        &quot;src/domogik_packages/xpl/lib/velbus.py&quot;, 
        &quot;src/domogik_packages/xpl/helper/velbus.py&quot;
    ], 
    &quot;identity&quot;: {
        &quot;author&quot;: &quot;Maikel Punie&quot;, 
        &quot;author_email&quot;: &quot;maikel.puni@gmail.com&quot;, 
        &quot;category&quot;: &quot;velbus&quot;, 
        &quot;changelog&quot;: &quot;0.1.0\n- relays only\n- serial comunication only \n0.2.0\n- added socket comunication\n0.3.0\n- added dimmer support\n0.4.0\n- added blind (up/down) support\n0.5.0\n- added temperature sensor support&quot;, 
        &quot;dependencies&quot;: [
            {
                &quot;id&quot;: &quot;pyserial (&gt;=2.6)&quot;, 
                &quot;type&quot;: &quot;python&quot;
            }
        ], 
        &quot;description&quot;: &quot;velbus interface&quot;, 
        &quot;documentation&quot;: &quot;http://wiki.domogik.org/plugin_velbus&quot;, 
        &quot;domogik_min_version&quot;: &quot;0.2.0&quot;, 
        &quot;id&quot;: &quot;velbus&quot;, 
        &quot;type&quot;: &quot;plugin&quot;, 
        &quot;version&quot;: &quot;0.5.0&quot;
    }, 
    &quot;json_version&quot;: 2, 
    &quot;technology&quot;: {
        &quot;description&quot;: &quot;Velbus http://www.velbus.eu&quot;, 
        &quot;id&quot;: &quot;velbus&quot;, 
        &quot;name&quot;: &quot;Velbus&quot;
    }, 
    &quot;udev-rules&quot;: [
        {
            &quot;description&quot;: &quot;Velbus USB interface&quot;, 
            &quot;filename&quot;: &quot;velbus.rules&quot;, 
            &quot;model&quot;: &quot;VMB1USB&quot;, 
            &quot;rule&quot;: &quot;SUBSYSTEM==\&quot;tty\&quot; ATTRS(manufacturer)==\&quot;Velleman Projects\&quot; ATTRS{product}==\&quot;VMB1USB Velbus USB interface\&quot; SYMLINK+=\&quot;velbus\&quot; MODE=\&quot;0666\&quot;&quot;
        }
    ]
}
{CODE}


!!!Command sending

a new rest url is created
{CODE()}/cmd/&lt;command Id&gt;/&lt;param 1&gt;/&lt;val 1&gt;/.../&lt;param N&gt;/&lt;val N&gt;{CODE}

The param fields have to match the fields inside command_param table for the given command id.

If the command has an associated XPL command then the xplcommand will be sent onto the network using the parameters from the commd_param table together with the parameters from the xplcommand table

!!! GUI add device steps
#select the correct device_type
#rinor will request the device specifick parameters (device section in json file) for the needed commands and for the needed stats (/base/device/params/&lt;device_type&gt;)
#display the input fields for this device
#add the device (/base/device/add), this will create the needed commands, xplcommands, xplstats and sensors
#add the devicetype parameters (/base/device/addglobal), this will append these parameters to all xplmessages associated with the device
#add the device specifick parameters to a specifick xpl command or xplstat (/base/device/xpl(COMMAND|STAT)params/

!!!Admin urls

*/plugin/json/&lt;id&gt;
*/base/device/params/(?P&lt;dev_type_id&gt;[\.a-z0-9]+)
{CODE()}{
       &quot;status&quot;: &quot;OK&quot;,
       &quot;code&quot;: 0,
       &quot;description&quot;: &quot;None&quot;,
       &quot;deviceparams&quot;:
       [
           {
               &quot;xpl_stat&quot;:
               [
                   {
                       &quot;params&quot;:
                       [
                       ],
                       &quot;name&quot;: &quot;get_level&quot;,
                       &quot;schema&quot;: &quot;lighting.device&quot;
                   },
                   {
                       &quot;params&quot;:
                       [
                       ],
                       &quot;name&quot;: &quot;get_level&quot;,
                       &quot;schema&quot;: &quot;lighting.device&quot;
                   }
               ],
               &quot;xpl_cmd&quot;:
               [
                   {
                       &quot;params&quot;:
                       [
                           {
                               &quot;type&quot;: &quot;string&quot;,
                               &quot;description&quot;: &quot;a dummy param&quot;,
                               &quot;key&quot;: &quot;dummy&quot;
                           }
                       ],
                       &quot;xplstat_name&quot;: &quot;get_level&quot;,
                       &quot;name&quot;: &quot;set_level_bin&quot;,
                       &quot;schema&quot;: &quot;lighting.basic&quot;
                   },
                   {
                       &quot;params&quot;:
                       [
                           {
                               &quot;type&quot;: &quot;string&quot;,
                               &quot;description&quot;: &quot;a dummy param&quot;,
                               &quot;key&quot;: &quot;dummy&quot;
                           }
                       ],
                       &quot;xplstat_name&quot;: &quot;get_level&quot;,
                       &quot;name&quot;: &quot;set_level_bin&quot;,
                       &quot;schema&quot;: &quot;lighting.basic&quot;
                   }
               ],
               &quot;global&quot;:
               [
                   {
                       &quot;max_value&quot;: 4,
                       &quot;min_value&quot;: 1,
                       &quot;type&quot;: &quot;integer&quot;,
                       &quot;description&quot;: &quot;The channel number&quot;,
                       &quot;key&quot;: &quot;channel&quot;
                   },
                   {
                       &quot;max_value&quot;: 255,
                       &quot;min_value&quot;: 0,
                       &quot;type&quot;: &quot;integer&quot;,
                       &quot;description&quot;: &quot;The decimal address&quot;,
                       &quot;key&quot;: &quot;address&quot;
                   }
               ]
           }
       ]
    }{CODE}
*/base/device/add =&gt; will add a device and the xpl command + stats into the db
/base/device/params/(?P&lt;dev_type_id&gt;[\.a-z0-9]+) =&gt; will return the needed parameters for this device type
*/base/device/addglobal/id/(?P&lt;id&gt;[0-9]+)/.* =&gt; will add the 'device_type' parameters to every command/stat message
*/base/device/xplcmdparams/id/(?P&lt;id&gt;[0-9]+)/&lt;key1&gt;/&lt;value1&gt;/... =&gt; will addd the key/value pairs to the xpl command
*/base/device/xplstatparams/id/(?P&lt;id&gt;[0-9]+)/&lt;key1&gt;/&lt;value1&gt;/... =&gt; will addd the key/value pairs to the xpl stat message
*/cmd/id/&lt;id&gt;/&lt;key1&gt;/&lt;value1&gt;/&lt;key2&gt;/&lt;value2&gt;/.... =&gt; sends out the xplcommand

the urls below need an update (not a fixed format yet)
*/base/xplcommand/add/schema/&lt;schema&gt;/reference/&lt;ref&gt;/device_id/&lt;devid&gt;/stat_id/&lt;statid&gt;
*/base/xplstat/add/schema/&lt;schema&gt;/reference/&lt;ref&gt;/device_id/&lt;devid&gt;/
*/base/xplcommandparam/add/stat_id/&lt;statId&gt;/key/&lt;key&gt;/value/&lt;value&gt;/static/&lt;static&gt;
*/base/xplstatparam/add/stat_id/&lt;statId&gt;/key/&lt;key&gt;/value/&lt;value&gt;/static/&lt;static&gt;
*/base/xplcommand/update/id/&lt;id&gt;/schema/&lt;schema&gt;/reference/&lt;ref&gt;/device_id/&lt;devid&gt;/stat_id/&lt;statid&gt;
*/base/xplstat/udpate/id/&lt;id&gt;/schema/&lt;schema&gt;/reference/&lt;ref&gt;/device_id/&lt;devid&gt;/
*/base/xplcommandparam/update/stat_id/&lt;statId&gt;/key/&lt;key&gt;/value/&lt;value&gt;/static/&lt;static&gt;
*/base/xplstatparam/update/stat_id/&lt;statId&gt;/key/&lt;key&gt;/value/&lt;value&gt;/static/&lt;static&gt;
*/base/xplcommand/delete/id/&lt;id&gt;
*/base/xplstat/delete/id/&lt;id&gt;
*/base/xplcommandparam/delete/stat_id/&lt;statId&gt;/key/&lt;key&gt;
*/base/xplstatparam/delete/stat_id/&lt;statId&gt;/key/&lt;key&gt;