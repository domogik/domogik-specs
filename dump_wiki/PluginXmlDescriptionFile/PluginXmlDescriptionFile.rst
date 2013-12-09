!Plugin xml description file

~~#F00:__IMPORTANT NOTICE : This page is only about Domogik 0.1.0__~~

~~#F00:For Domogik &gt;= 0.2, see [Packages_info_json] ~~

{maketoc}
!!Xml description file
A description file (xml format) must be created for each plugin. It describes, plugin (name, technology, where is online documentation, etc) and configuration options (short description, more details are in plugin's online documentation).

!!Template
{CODE()}
&lt;package type=&quot;plugin&quot;&gt;                                                         
  &lt;id&gt;&lt;!--plugin id(same as python file name without .py)--&gt;&lt;/id&gt;
  &lt;description&gt;&lt;!--The plugin description (could eb multiline)--&gt;&lt;/description&gt;
  &lt;changelog&gt;&lt;!-- multiline changelog Ex : 
0.2.0
- feature A
- feature B

0.1.0
- create plugin --&gt;
  &lt;/changelog&gt;
  &lt;technology&gt;&lt;!--technology--&gt;&lt;/technology&gt;
  &lt;version&gt;&lt;!--plugin version : change it when publishing a new version--&gt;&lt;/version&gt;
  &lt;documentation&gt;&lt;!--url for online documentation about plugin--&gt;&lt;/documentation&gt;
  &lt;domogik-min-version&gt;&lt;!-- domogik minimum version requirement --&gt;&lt;/domogik-min-version&gt;
  &lt;author&gt;&lt;!-- plugin's author --&gt;&lt;/author&gt;                                                        
  &lt;author-email&gt;&lt;!-- plugin's author email --&gt;&lt;/author-email&gt;                           
  &lt;configuration-keys&gt;
    &lt;key&gt;
      &lt;!-- if you want to set several options for multi interfaces, add this entry to link them to an interface group :
      &lt;interface&gt;yes&lt;/interface&gt;
      --&gt;
      &lt;!-- if the parameter is optionnal (example : login/password for a relayboard which can need or not auth) :
      &lt;optionnal&gt;yes&lt;/optionnal&gt;
      --&gt;      
      &lt;order-id&gt;&lt;!--id only used to order configuration keys (0...n)--&gt;&lt;/order-id&gt;
      &lt;name&gt;&lt;!--key name : 14 caracters maximum. Available caracters : &quot;[a-z][0-9]&quot; and &quot;-&quot; --&gt;&lt;/name&gt;
      &lt;description&gt;&lt;!--key description. Should length at most 80 caracters. If you want to make more, do it in the documentation. Don't use any ','.--&gt;&lt;/description&gt;
      &lt;type&gt;&lt;!-- type of key data : boolean, number, string, enum. Only used by for a nicer display--&gt;&lt;/type&gt;
      &lt;!-- the following is only used in case of type enum --&gt;
      &lt;options&gt;
           &lt;option&gt;&lt;!-- option to select --&gt;&lt;/option&gt;
           &lt;option&gt;&lt;!-- option to select --&gt;&lt;/option&gt;
      &lt;/options&gt;
      &lt;!-- end enum specific --&gt;
      &lt;default-value&gt;&lt;!--defualt or recommended value for key configuration--&gt;&lt;/default-value&gt;
    &lt;/key&gt;
    &lt;key&gt;
      &lt;!-- .... --&gt;
    &lt;/key&gt;
  &lt;/configuration-keys&gt;
  &lt;files&gt;
    &lt;file path=&quot;&lt;!-- /path/to/first/file/needed/by/plugin --&gt;&quot;/&gt;
    &lt;file path=&quot;&lt;!-- /path/to/second/file/needed/by/plugin --&gt;&quot;/&gt;
    &lt;!-- ... --&gt;
  &lt;/files&gt;
  &lt;dependencies&gt;                                                                
    &lt;dep type=&quot;python=&quot; id=&quot;pyserial (&gt;=2.5)&quot;/&gt;&lt;!-- example for a python dependency (distutils2 format). Ex : 'pyserial (&gt;=2.5)', 'foo (&gt;1.0, &lt;1.8)', ... --&gt;
    &lt;dep type=&quot;plugin&quot; id=&quot;xpl_time&quot;/&gt;&lt;!-- example for a plugin dependency : another plugin must run in order this one could be functionnal --&gt;
    &lt;dep type=&quot;other&quot; id=&quot;owfs&quot;/&gt;&lt;!-- example for another dependency (example : owfs for onewire, which need a manual installation --&gt;
    &lt;!-- ... --&gt;
  &lt;/dependencies&gt; 
  &lt;udev-rules&gt;  &lt;!-- the list (optionnal) of possible udev rules for the plugin--&gt;
    &lt;rule model=&quot;the device model&quot; description=&quot;long description of the model&quot; filename=&quot;foo.rules&quot;&gt;
DEFINE HERE THE UDEV RULE TO WRITE IN foo.rules FILE
    &lt;/rule&gt;
    &lt;!-- ... --&gt;
  &lt;/udev-rules&gt; 
  
  &lt;!-- ---- Database data ---- 
       The following data are isnerted in database when plugin is installed
       They are used by Rest to give the UI the informations they needs to display technology, features, etc
       
       To get mroe info about all foolowing data, please read http://wiki.domogik.org/DevelopersDatabase for &quot;0.1.0 model&quot;
  --&gt;
  &lt;device_technology&gt;
    &lt;id&gt;&lt;!-- technology id. Available caracters : &quot;[a-z][0-9]&quot;. Example : relayboard --&gt;&lt;/id&gt;
    &lt;name&gt;&lt;!-- Displayed name of technology. Example : Relay board --&gt;&lt;/name&gt;
    &lt;description&gt;&lt;!-- Description of technology. Example : Relay boards monitoring and controlling --&gt;&lt;/description&gt;
  &lt;/device_technology&gt;
  &lt;device_types&gt;
    &lt;device_type&gt;
      &lt;id&gt;&lt;!-- device type id. Available caracters : &quot;[a-z][0-9]&quot;. Should be formatted like this : &lt;technology&gt;.&lt;type&gt;. Example : relayboard.relay --&gt;&lt;/id&gt;
      &lt;device_technology_id&gt;&lt;!-- technology id. Example : relayboard --&gt;&lt;/device_technology_id&gt;
      &lt;name&gt;&lt;!-- Displayed name of device type. Example : Relay --&gt;&lt;/name&gt;
      &lt;description&gt;&lt;!-- Description of device type. Example : Relay --&gt;&lt;/description&gt;
    &lt;/device_type&gt;
    &lt;device_type&gt;
      &lt;!-- another device type --&gt;
    &lt;/device_type&gt;
  &lt;/device_types&gt;
  &lt;device_feature_models&gt;
    &lt;device_feature_model&gt;
      &lt;id&gt;&lt;!-- device feature model id. Available caracters : &quot;[a-z][0-9]&quot;. Should be formatted like this : &lt;technology&gt;.&lt;type&gt;. Example : relayboard.relay.switch --&gt;&lt;/id&gt;
      &lt;name&gt;&lt;!-- Displayed name of device feature model. Example : Switch --&gt;&lt;/name&gt;
      &lt;feature_type&gt;&lt;!-- feature type : actuator, sensor. Example : actuator--&gt;&lt;/feature_type&gt;
      &lt;device_type_id&gt;&lt;!-- device type id. Example : relayboard.relay --&gt;&lt;/device_type_id&gt;
      &lt;parameters&gt;
          &lt;!-- parameters for web UI. Example : {&amp;quot;output&amp;quot;:&amp;quot;&amp;quot;,&amp;quot;value0&amp;quot;:&amp;quot;low&amp;quot;, &amp;quot;value1&amp;quot;:&amp;quot;high&amp;quot;}--&gt;
      &lt;/parameters&gt;
      &lt;value_type&gt;&lt;!-- type of value returned by xpl messages : binary, number, string, etc (depanding on feature type : see online documentation) --&gt;&lt;/value_type&gt;
      &lt;stat_key&gt;&lt;!-- stat key in database. Example : output --&gt;&lt;/stat_key&gt;
      &lt;return_confirmation&gt;&lt;!--For an actuator, will device return a confirmaton ? 1=yes, 0=no. Example : 1--&gt;&lt;/return_confirmation&gt;
    &lt;/device_feature_model&gt;
    &lt;device_feature_model&gt;
      &lt;!-- another device feature model --&gt;
    &lt;/device_feature_model&gt;
  &lt;/device_feature_models&gt;  
&lt;/package&gt;   
{CODE}

__Notice :__ for __database part__ of the xml files, it is not very simple to fill it. With the next data model, we will make it differently, so it will be less difficult ;)

Feel free to come on irc to ask for our help or to use the mailing list.

!!Template : specific elements for &quot;hardware&quot; type
Set type = hardware
{CODE()}
&lt;package type=&quot;hardware&quot;&gt; 
{CODE}

Set no configuration element :
{CODE()}
&lt;configuration-keys/&gt;
{CODE}

Add vendor id and device id :
{CODE()}
&lt;vendor-id&gt;&lt;!--hardware vendor id--&gt;&lt;/vendor-id&gt;
&lt;device-id&gt;&lt;!--hardware device id--&gt;&lt;/device-id&gt;
{CODE}

If external files are provided (for example sketch files for an arduino, etc), list them :
{CODE()}
&lt;external_files&gt;                                                              
  &lt;file path=&quot;src/external/hardware/&lt;name for related 'hardware' plugin&gt;/&lt;file 1&gt;&quot;/&gt;                       
  &lt;file path=&quot;src/external/hardware/&lt;name for related 'hardware' plugin&gt;/&lt;file 2&gt;&quot;/&gt;                       
  ...
&lt;/external_files&gt; 
{CODE}

!!Load new data in database
If you update any __&lt;device*&gt;__ part of the xml, you will have to reload this file in database. This could be done like this :
{CODE()}
cd src/tools/packages
./insert_data.py ../../share/domogik/plugins/&lt;your plugin name&gt;.xml
{CODE}