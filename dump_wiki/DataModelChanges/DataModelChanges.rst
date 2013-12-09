!Database modifications
!!core_device
!!!Actual table
{FANCYTABLE(head=&gt;id~|~name~|~description~|~address~|~reference~|~device_usage_id~|~device_type_id)}
1~|~Lampe~|~~|~A2~|~2263D~|~light~|~plcbus.dimmer
2~|~Capteur~|~~|~508587010000~|~DS18B20~|~temperature~|~onewire.thermometer
{FANCYTABLE}

!!!New table
* address will be removed
* add a field for unique/multi addresses
* add a field for techno
* device_type can be empty 
{FANCYTABLE(head=&gt;id~|~name~|~description~|~reference~|~technology_id~|~type)}
1~|~Lampe~|~~|~2263D~|~plcbus~|~plcbus.dimmer
2~|~Capteur~|~~|~DS18B20~|~onewire~|~onewire.thermometer
3~|~Volet~|~~|~TXA302~|~knx~|~
{FANCYTABLE}

!!core_device_feature
!!!Actual table
{FANCYTABLE(head=&gt;id~|~device_id~|~device_feature_model_id)}
1~|~1~|~plcbus.switch.switch
2~|~2~|~onewire.thermometer.temperature
{FANCYTABLE}

!!!New table
* rename table to core_feature
* add feature model info fields
* remove device_type
* add address, type and command fields (for command reference)
* add address, type and key fields (for state reference) 
{FANCYTABLE(head=&gt;id~|~device_id~|~name~|~command_type~|~command_address~|~command_reference~|~state_type~|~state_address~|~state_reference)}
1~|~1~|~Switch~|~DT_Switch~|~A2~|~~|~DT_Switch~|~A2~|~command
2~|~2~|~Temperature~|~~|~~|~~|~DT_Temp~|~508587010000~|~temperature
3~|~3~|~Switch~|~DT_Switch~|~1/1/1~|~~|~DT_Switch~|~1/1/1~|~	
{FANCYTABLE}

!!!Pre-population process
In the actual model, the feature table is automatically populated , based on the device_type, when the device is created.
In the new model, the device_type is not required anymore (because of customs devices).

!!core_device_config
* Will be updated for 'core_feature_config'

!!core_device_type
* Will be renamed to 'core_device_model' 

!!core_feature_model
!!!Actual table
{FANCYTABLE(head=&gt;id~|~name~|~feature_type~|~device_type_id~|~parameters~|~value_type~|~stat_key~|~return_confirmation)}
plcbus.switch.switch~|~Switch~|~actuator~|~plcbus.switch~|~{&quot;command&quot;:&quot;&quot;,&quot;value0&amp;quo...~|~binary~|~command~|~1
onewire.thermometer.temperature~|~Temperature~|~sensor~|~onewire.thermometer~|~{&quot;unit&quot;:&quot;\u00B0C&quot;}~|~number~|~temperature~|~0
{FANCYTABLE}

!!!New table
* remove fields : parameters, return_confirmation
* add field : command_reference
* rename field : stat_key to state_reference
* change value_type to domogik type field 
{FANCYTABLE(head=&gt;id~|~name~|~device_type_id~|~command_type~|~command_reference~|~state_type~|~state_reference)}
plcbus.switch.switch~|~Switch~|~aplcbus.switch~|~DT_Switch~|~~|~DT_Switch~|~command
onewire.thermometer.temperature~|~Temperature~|~onewire.thermometer~|~~|~~|~DT_Temp~|~temperature
{FANCYTABLE}

!!core_device_stats
* Will be renamed to 'core_feature_states' 

!!!Actual table
{FANCYTABLE(head=&gt;date~|~timestamp~|~key~|~device_id~|~value_num~|~value_str)}
2010-12-26 11:31:45~|~1293359505~|~ping~|~3~|~NULL~|~high
2010-12-26 11:32:00~|~1293359520~|~temperature~|~2~|~15.25~|~15.25
{FANCYTABLE}

!!!New table
* device_id will be replaced by feature_id
* key will be removed
* DMG Type will be added for each stats (for easy access) 
{FANCYTABLE(head=&gt;id~|~date~|~timestamp~|~feature_id~|~type~|~value_num~|~value_str)}
1~|~2010-12-26 11:31:45~|~1293359505~|~6~|~DT_State~|~NULL~|~Active
2~|~2010-12-26 11:32:00~|~1293359520~|~8~|~DT_Temp~|~15.25~|~15.25
{FANCYTABLE}

!!!core_device_usage
* Will be removed. Usages are transferred to ((UICommonSettings||UI Common Settings))