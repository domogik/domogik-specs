!Web UI : creating new devices
{maketoc}

!!Ideas
* For actuators, add a field for the device for the max power consumed by the appliance plugged on the actuator

!!Administration view
When creating a new device, the user will have 2 choices:

* Unique address, for physical device of software service where the features can be reached by a unique address. (X10, plcBus, ...)
* Multi addresses, for physical or virtual devices where the features are identified by their own individual addresses. (KNX, ...) 

The user will have to choose a techno, or a specific device type for pre-populated feature list.

It will be possible to add, remove or disable any feature.
And Configure the Domogik Type for each feature.

As actually the features will be separated in 2 categories:
* Actuator: with reference for command and reference for state
* Sensor: only with state reference 

!!!Unique address device
* Will ask for a global address
* For each feature it will require, the command name (for command) or key name (for state) as references 
!!Multi address device
* For each feature it will require, the addresses (for command and for state) as references 

Points to see :
* auto discovery (modify below pic)
* make pictures examples for techno/type
* make pictures examples for address

{IMG(attId=&quot;269&quot;)}{IMG}

!!Auto discovery process
!!!Plugin side
At startup, the plugin create one or more listeners for :
* type = xpl-cmnd
* schema = domogik.helpers
* command = autodiscovery
* techno = &lt;plugin technology&gt;
If a plugin/technology can make the difference between features : the lsitener is also on :
* feature/type = &lt;feature/type (same than UI value)
 
A listener makes reference to a callback function that will :
* refresh devices list
* send a list as xpl-trig domogik.helpers. &quot;plugin = &lt;plugin name&gt;&quot; is added in xpl message

!!!xPL
Request : 
{CODE()}
xpl-cmnd
{
...
}
domogik.helper
{
command = autodiscovery
technology = &lt;technology asking for discovery&gt;
[ type = &lt;filter on type : switch, light, temperature, etc&gt; ]
}
{CODE}

Answer : 
{CODE()}
xpl-trig
{
...
}
domogik.helper
{
command = autodiscovery
technology = &lt;technology asking for discovery&gt;
[ type = &lt;filter on type : switch, light, temperature, etc&gt; ]
plugin = &lt;plugin providing device&gt;
host = &lt;host on which is plugin&gt;
dev0-address = &lt;address&gt;
dev0-reference = &lt;reference&gt;
dev1-address = ...
dev1-reference = ...
...
}
{CODE}

!!!UI/REST side
When clicking in the address field, a box appears. On box opening, REST is called : 
* /autodiscovery/technology/&lt;techno&gt; [ /type/&lt;type&gt; ]
This makes REST send a ''xpl-cmnd domogik.helpers'' &quot;command=autodiscovery&quot; message. Then REST waits for several replies.