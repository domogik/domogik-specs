!Device template
||__Created:__|20/08/2011
__Creator:__|Ferllings
__Reviewers:__|
__Status:__|{GAUGE(value=&gt;30, max=&gt;100, label=&gt;''draft'', perc=&gt;true, labelsize=&gt;50, height=&gt;20, color=&gt;green, bgcolor=&gt;#EEEEEE)}{GAUGE}
__Target:__|?
__References:__|((Database_device_structure|Device structure)), ((Spec_domogik_data_types|Domogik data types specification)), ((Spec_field_types|Field types))||

The template system will be used to simplify the creation of commands/states for the device.

!!Template process
*When filling the device entries, a device type is chosen from a template list.
*The UI automatically retrieve the template data from the plugin declaration file (Using REST API).
*The UI fill the device entries, the commands and states.
*The user can adjust and save the data to the ((Database_device_structure|Database device structure)).
With this template system, a device structure can be created easily, customized or completely created manually.

!! JSON declaration
For the ''type'' attribute defined in the ''command'' tag, see ((Spec_domogik_data_types|the data types specification)).
{CODE()}
{
	&quot;device_templates&quot;:[
		{
			&quot;version&quot;:&quot;(version number used for devices updates)&quot;,
			&quot;id&quot;:&quot;(The template identifier. It will be added to the created device, for reference and filtering)&quot;,
			&quot;data&quot;:[
				{
					&quot;reference&quot;:&quot;(A reference name to identify the data. Unique in a device)&quot;,
					&quot;dmgtype&quot;:&quot;(The Domogik type of the value)&quot;,
					&quot;no_log&quot;:&quot;(Set true if the data should not be logged)&quot;,
				}
				...
			],
			&quot;xplstat&quot;:[
				{
					&quot;reference&quot;:&quot;(A reference name to identify the stat. Unique in a device)&quot;,
					&quot;schema&quot;: &quot;(xpl schema used by the xpl message)&quot;,
					&quot;data&quot;: [(list of data used by the xpl message)
						{&quot;reference&quot;: &quot;(data reference)&quot;, &quot;rename&quot;: &quot;Set if the attribute name is different in the xplmessage&quot;},
						...
					],
					&quot;parameters_static&quot;: [(list of static values used by the xpl message)
						{
							&quot;key&quot;:&quot;(parameter id)&quot;,
							&quot;static&quot;:true,
							&quot;value&quot;:&quot;(static parameter value)&quot;,
						},
						...
					],
					&quot;parameters_user&quot;: [(list of user parameters used by the xpl message)
						{
							&quot;key&quot;:&quot;(parameter id)&quot;,
							&quot;static&quot;:false,
							&quot;name&quot;:&quot;(Label of the parameter)&quot;,
							&quot;description&quot;:&quot;(Short description to help the user)&quot;,
							&quot;type&quot;:&quot;(Type of the expected value, ((Spec_field_types|See here for the full list of types)))&quot;,
							&quot;default&quot;:&quot;(default value)&quot;,
							&quot;required&quot;:&quot;(If the value is required)&quot;,
							...
							((Spec_field_types|See here for the full list of type options))
							...
						}
					]
				}
			],
			&quot;xplcommand&quot;:[
				{
					&quot;reference&quot;:&quot;(A reference name to identify the command. Unique in a device)&quot;,
					&quot;schema&quot;: &quot;(xpl schema used by the xpl message)&quot;,
					&quot;xplstat_ack&quot;: &quot;(reference of the stat message used to ACK the command)&quot;,
					&quot;data&quot;: [(list of data used by the xpl message)
						{&quot;reference&quot;: &quot;(data reference)&quot;, &quot;rename&quot;: &quot;Set if the attribute name is different in the xplmessage&quot;},
						...
					],
					&quot;parameters_static&quot;: [(list of static values used by the xpl message)
						{
							&quot;key&quot;:&quot;(parameter id)&quot;,
							&quot;static&quot;:true,
							&quot;value&quot;:&quot;(static parameter value)&quot;,
						},
						...
					],
					&quot;parameters_user&quot;: [(list of user parameters used by the xpl message)
						{
							&quot;key&quot;:&quot;(parameter id)&quot;,
							&quot;static&quot;:false,
							&quot;name&quot;:&quot;(Label of the parameter)&quot;,
							&quot;description&quot;:&quot;(Short description to help the user)&quot;,
							&quot;type&quot;:&quot;(Type of the expected value, ((Spec_field_types|See here for the full list of types)))&quot;,
							&quot;default&quot;:&quot;(default value)&quot;,
							&quot;required&quot;:&quot;(If the value is required)&quot;,
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
{CODE}

!! Example for the PLCBus member
{CODE(caption=&quot;plcbus.xml&quot;)}
&lt;device_templates version='0.5'&gt;
    &lt;device&gt;
        &lt;id&gt;plcbus.switch&lt;/id&gt;
        &lt;name&gt;Switch&lt;/name&gt;
        &lt;description&gt;Switch&lt;/description&gt;
        &lt;commands&gt;
           &lt;command name='On' type='DT_Trigger' reference='on' /&gt;
           &lt;command name='Off' type='DT_Trigger' reference='off' /&gt;
        &lt;/commands&gt;
        &lt;states&gt;
           &lt;state name='Switch' type='DT_Switch' reference='command' /&gt;
        &lt;/states&gt;
        &lt;references&gt;
           &lt;reference name='2027G' category='appliance'&gt;
               &lt;description&gt;Plug-In Appliance Module&lt;/description&gt;
               &lt;image&gt;2027g.jpg&lt;/image&gt;
           &lt;/reference&gt;
        &lt;/references&gt;
    &lt;/device&gt;
    &lt;device&gt;
        &lt;id&gt;plcbus.dimmer&lt;/id&gt;
        &lt;name&gt;Dimmer&lt;/name&gt;
        &lt;description&gt;Dimmer&lt;/description&gt;
        &lt;commands&gt;
           &lt;command name='On' type='DT_Trigger' reference='on' /&gt;
           &lt;command name='Off' type='DT_Trigger' reference='off' /&gt;
           &lt;command name='Change' type='DT_Trigger' reference='preset_dim' /&gt;
        &lt;/commands&gt;
        &lt;states&gt;
           &lt;state name='Switch' type='DT_Switch' reference='command' /&gt;
           &lt;state name='Level' type='DT_Scaling' reference='level' /&gt;
        &lt;/states&gt;
        &lt;references&gt;
           &lt;reference name='2263D' category='light'&gt;
               &lt;description&gt;One-Load Lamp Module&lt;/description&gt;
               &lt;image&gt;2263d.jpg&lt;/image&gt;
           &lt;/reference&gt;
        &lt;/references&gt;
    &lt;/device&gt;
&lt;/device_templates&gt;
{CODE}

!! Example for the OneWire member
{CODE(caption=&quot;onewire.xml&quot;)}
&lt;device_templates version='1.2'&gt;
    &lt;device&gt;
        &lt;id&gt;onewire.thermometer&lt;/id&gt;
        &lt;name&gt;Thermometer&lt;/name&gt;
        &lt;description&gt;Thermometer&lt;/description&gt;
        &lt;states&gt;
           &lt;state name='Temperature' type='DT_Temp' reference='temperature' /&gt;
        &lt;/states&gt;
        &lt;references&gt;
           &lt;reference name='DS18B20' category='light'&gt;
               &lt;description&gt;Programmable Resolution 1-Wire Digital Thermometer&lt;/description&gt;
               &lt;image&gt;ds18b20.jpg&lt;/image&gt;
               &lt;documentation&gt;http://www.maxim-ic.com/datasheet/index.mvp/id/2812&lt;/documentation&gt;
           &lt;/reference&gt;
        &lt;/references&gt;
    &lt;/device&gt;
    &lt;device&gt;
        &lt;id&gt;onewire.temperature_and_humidity&lt;/id&gt;
        &lt;name&gt;Temperature and Humidity&lt;/name&gt;
        &lt;description&gt;Temperature and Humidity&lt;/description&gt;
        &lt;states&gt;
           &lt;state name='Temperature' type='DT_Temp' reference='temperature' /&gt;
           &lt;state name='Humidity' type='DT_Humidity' reference='humidity' /&gt;
        &lt;/states&gt;
    &lt;/device&gt;
    &lt;device&gt;
        &lt;id&gt;onewire.serial_number&lt;/id&gt;
        &lt;name&gt;Serial number&lt;/name&gt;
        &lt;description&gt;Serial number&lt;/description&gt;
        &lt;states&gt;
           &lt;state name='Connected' type='DT_State' reference='present' /&gt;
        &lt;/states&gt;
    &lt;/device&gt;
&lt;/device_templates&gt;
{CODE}