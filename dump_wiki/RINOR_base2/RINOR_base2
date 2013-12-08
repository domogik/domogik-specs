!!Devices
{CODE()}/base/device/list 
/base/device/add/name/&lt;name&gt;/description/&lt;description&gt;/reference/&lt;reference&gt;/usage_id/&lt;usage id&gt;/technology_id/&lt;technology id&gt;/type/&lt;type&gt;
/base/device/update/&lt;id&gt;/name/&lt;name&gt;/description/&lt;description&gt;/reference/&lt;reference&gt;/usage_id/&lt;usage id&gt;
/base/device/del/&lt;id&gt;{CODE}
{REMARKSBOX(type=&gt;note)}
device technology and device type can not be updated after creation
{REMARKSBOX}

!!Device parameters
~~#C00:__To update with database model__~~

!!Features
{CODE()}/base/feature/list/by-id/&lt;id&gt;
/base/feature/list/by-device_id/&lt;id&gt; 
/base/feature/add/device_id/&lt;device_id&gt;/name/&lt;name&gt;/command_type/&lt;DMG type&gt;/command_address/&lt;command address&gt;/command_reference/&lt;command reference&gt;/state_type/&lt;DMG type&gt;/state_address/&lt;state address&gt;/state_reference/&lt;state reference&gt;
/base/feature/update/&lt;id&gt;/name/&lt;name&gt;/command_type/&lt;DMG type&gt;/command_address/&lt;command address&gt;/command_reference/&lt;command reference&gt;/state_type/&lt;DMG type&gt;/state_address/&lt;state address&gt;/state_reference/&lt;state reference&gt;
/base/feature/del/by-id/&lt;id&gt;
/base/feature/del/by-device_id/&lt;id&gt; 
{CODE}
{REMARKSBOX(type=&gt;note)}
device_id can not be updated
{REMARKSBOX}

!!Feature parameters
~~#C00:__To update with database model__~~
{CODE()}/base/feature_config/set/feature_id/&lt;feature id&gt;/key/&lt;key&gt;/value/&lt;value&gt;
/base/feature_config/del/by-feature_id/&lt;feature id&gt;
/base/feature_config/del/by-key/&lt;feature id&gt;/&lt;key&gt;
{CODE}

!!Device templates
{CODE()}/base/device_template/list/by-id/&lt;device type&gt;{CODE}
{REMARKSBOX(type=&gt;note)}
There is no need for writing REST urls as they are updated using the xml process
{REMARKSBOX}

!!Feature templates
{CODE()}/base/feature_template/list/by-device_id/&lt;device type&gt;{CODE}
{REMARKSBOX(type=&gt;note)}
There is no need for writing REST urls as they are updated using the xml process
{REMARKSBOX}

!!Features states
{CODE()}/states/&lt;feature id&gt;/all
/states/&lt;feature id&gt;/latest
/states/&lt;feature id&gt;/last/&lt;number of item to get&gt;
/states/&lt;feature id&gt;/from/&lt;start time&gt; {/to/&lt;end time&gt;}
/states/&lt;feature id&gt;/from/&lt;start time&gt; {/to/&lt;end time&gt;}/interval/&lt;year, month, week, day, hour, minute, second&gt;/selector/&lt;min(number only), max(number only), avg(number only), first, last, x&gt;{CODE}

!!Plugin config
~~#C00:__To update with database model__~~
{CODE()}
/plugin/config/set/name/&lt;plugin name&gt;/hostname/&lt;hostname&gt;/key/&lt;key&gt;/value/&lt;value&gt; {/interface/&lt;interface number : 0..n&gt;}
{CODE}

!!Pages
{CODE()}/base/page/list
/base/page/add/name/&lt;name&gt;/description/&lt;description&gt;/parent/&lt;parent id&gt;
/base/page/update/&lt;id&gt;/name/&lt;name&gt;/description/&lt;description&gt;/parent/&lt;parent id&gt;
/base/page/del/&lt;id&gt;
/base/page/view/&lt;id&gt;
/base/page/tree/&lt;id&gt;
/base/page/path/&lt;id&gt;
{CODE}