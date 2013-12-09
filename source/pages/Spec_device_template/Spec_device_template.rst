****************
Device template
****************

||__Created:__|20/08/2011
__Creator:__|Ferllings
__Reviewers:__|
__Status:__|{GAUGE(value=>30, max=>100, label=>''draft'', perc=>true, labelsize=>50, height=>20, color=>green, bgcolor=>#EEEEEE)}{GAUGE}
__Target:__|?
__References:__|((Database_device_structure|Device structure)), ((Spec_domogik_data_types|Domogik data types specification)), ((Spec_field_types|Field types))||

The template system will be used to simplify the creation of commands/states for the device.

Template process
=================

*When filling the device entries, a device type is chosen from a template list.
*The UI automatically retrieve the template data from the plugin declaration file (Using REST API).
*The UI fill the device entries, the commands and states.
*The user can adjust and save the data to the ((Database_device_structure|Database device structure)).
With this template system, a device structure can be created easily, customized or completely created manually.

 JSON declaration
==================

For the ''type'' attribute defined in the ''command'' tag, see ((Spec_domogik_data_types|the data types specification)).
.. code-block:: json


    
    {
    	"device_templates":[
    		{
    			"version":"(version number used for devices updates)",
    			"id":"(The template identifier. It will be added to the created device, for reference and filtering)",
    			"data":[
    				{
    					"reference":"(A reference name to identify the data. Unique in a device)",
    					"dmgtype":"(The Domogik type of the value)",
    					"no_log":"(Set true if the data should not be logged)",
    				}
    				...
    			],
    			"xplstat":[
    				{
    					"reference":"(A reference name to identify the stat. Unique in a device)",
    					"schema": "(xpl schema used by the xpl message)",
    					"data": [(list of data used by the xpl message)
    						{"reference": "(data reference)", "rename": "Set if the attribute name is different in the xplmessage"},
    						...
    					],
    					"parameters_static": [(list of static values used by the xpl message)
    						{
    							"key":"(parameter id)",
    							"static":true,
    							"value":"(static parameter value)",
    						},
    						...
    					],
    					"parameters_user": [(list of user parameters used by the xpl message)
    						{
    							"key":"(parameter id)",
    							"static":false,
    							"name":"(Label of the parameter)",
    							"description":"(Short description to help the user)",
    							"type":"(Type of the expected value, ((Spec_field_types|See here for the full list of types)))",
    							"default":"(default value)",
    							"required":"(If the value is required)",
    							...
    							((Spec_field_types|See here for the full list of type options))
    							...
    						}
    					]
    				}
    			],
    			"xplcommand":[
    				{
    					"reference":"(A reference name to identify the command. Unique in a device)",
    					"schema": "(xpl schema used by the xpl message)",
    					"xplstat_ack": "(reference of the stat message used to ACK the command)",
    					"data": [(list of data used by the xpl message)
    						{"reference": "(data reference)", "rename": "Set if the attribute name is different in the xplmessage"},
    						...
    					],
    					"parameters_static": [(list of static values used by the xpl message)
    						{
    							"key":"(parameter id)",
    							"static":true,
    							"value":"(static parameter value)",
    						},
    						...
    					],
    					"parameters_user": [(list of user parameters used by the xpl message)
    						{
    							"key":"(parameter id)",
    							"static":false,
    							"name":"(Label of the parameter)",
    							"description":"(Short description to help the user)",
    							"type":"(Type of the expected value, ((Spec_field_types|See here for the full list of types)))",
    							"default":"(default value)",
    							"required":"(If the value is required)",
    							...
    							((Spec_field_types|See here for the full list of type options))
    							...
    						}
    					]
    				}
    			],
    		}
    	]
    }
    


 Example for the PLCBus member
===============================

.. code-block:: json

caption="plcbus.xml"
    
    <device_templates version='0.5'>
        <device>
            <id>plcbus.switch</id>
            <name>Switch</name>
            <description>Switch</description>
            <commands>
               <command name='On' type='DT_Trigger' reference='on' />
               <command name='Off' type='DT_Trigger' reference='off' />
            </commands>
            <states>
               <state name='Switch' type='DT_Switch' reference='command' />
            </states>
            <references>
               <reference name='2027G' category='appliance'>
                   <description>Plug-In Appliance Module</description>
                   <image>2027g.jpg</image>
               </reference>
            </references>
        </device>
        <device>
            <id>plcbus.dimmer</id>
            <name>Dimmer</name>
            <description>Dimmer</description>
            <commands>
               <command name='On' type='DT_Trigger' reference='on' />
               <command name='Off' type='DT_Trigger' reference='off' />
               <command name='Change' type='DT_Trigger' reference='preset_dim' />
            </commands>
            <states>
               <state name='Switch' type='DT_Switch' reference='command' />
               <state name='Level' type='DT_Scaling' reference='level' />
            </states>
            <references>
               <reference name='2263D' category='light'>
                   <description>One-Load Lamp Module</description>
                   <image>2263d.jpg</image>
               </reference>
            </references>
        </device>
    </device_templates>
    


 Example for the OneWire member
================================

.. code-block:: json

caption="onewire.xml"
    
    <device_templates version='1.2'>
        <device>
            <id>onewire.thermometer</id>
            <name>Thermometer</name>
            <description>Thermometer</description>
            <states>
               <state name='Temperature' type='DT_Temp' reference='temperature' />
            </states>
            <references>
               <reference name='DS18B20' category='light'>
                   <description>Programmable Resolution 1-Wire Digital Thermometer</description>
                   <image>ds18b20.jpg</image>
                   <documentation>http://www.maxim-ic.com/datasheet/index.mvp/id/2812</documentation>
               </reference>
            </references>
        </device>
        <device>
            <id>onewire.temperature_and_humidity</id>
            <name>Temperature and Humidity</name>
            <description>Temperature and Humidity</description>
            <states>
               <state name='Temperature' type='DT_Temp' reference='temperature' />
               <state name='Humidity' type='DT_Humidity' reference='humidity' />
            </states>
        </device>
        <device>
            <id>onewire.serial_number</id>
            <name>Serial number</name>
            <description>Serial number</description>
            <states>
               <state name='Connected' type='DT_State' reference='present' />
            </states>
        </device>
    </device_templates>
    
