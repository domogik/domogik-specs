****************************
Plugin xml description file
****************************

~~#F00:__IMPORTANT NOTICE : This page is only about Domogik 0.1.0__~~

~~#F00:For Domogik >= 0.2, see [Packages_info_json] ~~

.. toctree::


Xml description file
=====================
A description file (xml format) must be created for each plugin. It describes, plugin (name, technology, where is online documentation, etc) and configuration options (short description, more details are in plugin's online documentation).

Template
=========
.. code-block::
    
    <package type="plugin">                                                         
      <id><!--plugin id(same as python file name without .py)--></id>
      <description><!--The plugin description (could eb multiline)--></description>
      <changelog><!-- multiline changelog Ex : 
    0.2.0
    * feature A
    * feature B
    
    0.1.0
    * create plugin -->
      </changelog>
      <technology><!--technology--></technology>
      <version><!--plugin version : change it when publishing a new version--></version>
      <documentation><!--url for online documentation about plugin--></documentation>
      <domogik-min-version><!-- domogik minimum version requirement --></domogik-min-version>
      <author><!-- plugin's author --></author>                                                        
      <author-email><!-- plugin's author email --></author-email>                           
      <configuration-keys>
        <key>
          <!-- if you want to set several options for multi interfaces, add this entry to link them to an interface group :
          <interface>yes</interface>
          -->
          <!-- if the parameter is optionnal (example : login/password for a relayboard which can need or not auth) :
          <optionnal>yes</optionnal>
          -->      
          <order-id><!--id only used to order configuration keys (0...n)--></order-id>
          <name><!--key name : 14 caracters maximum. Available caracters : "[a-z][0-9]" and "-" --></name>
          <description><!--key description. Should length at most 80 caracters. If you want to make more, do it in the documentation. Don't use any ','.--></description>
          <type><!-- type of key data : boolean, number, string, enum. Only used by for a nicer display--></type>
          <!-- the following is only used in case of type enum -->
          <options>
               <option><!-- option to select --></option>
               <option><!-- option to select --></option>
          </options>
          <!-- end enum specific -->
          <default-value><!--defualt or recommended value for key configuration--></default-value>
        </key>
        <key>
          <!-- .... -->
        </key>
      </configuration-keys>
      <files>
        <file path="<!-- /path/to/first/file/needed/by/plugin -->"/>
        <file path="<!-- /path/to/second/file/needed/by/plugin -->"/>
        <!-- ... -->
      </files>
      <dependencies>                                                                
        <dep type="python=" id="pyserial (>=2.5)"/><!-- example for a python dependency (distutils2 format). Ex : 'pyserial (>=2.5)', 'foo (>1.0, <1.8)', ... -->
        <dep type="plugin" id="xpl_time"/><!-- example for a plugin dependency : another plugin must run in order this one could be functionnal -->
        <dep type="other" id="owfs"/><!-- example for another dependency (example : owfs for onewire, which need a manual installation -->
        <!-- ... -->
      </dependencies> 
      <udev-rules>  <!-- the list (optionnal) of possible udev rules for the plugin-->
        <rule model="the device model" description="long description of the model" filename="foo.rules">
    DEFINE HERE THE UDEV RULE TO WRITE IN foo.rules FILE
        </rule>
        <!-- ... -->
      </udev-rules> 
      
      <!-- ---- Database data ---- 
           The following data are isnerted in database when plugin is installed
           They are used by Rest to give the UI the informations they needs to display technology, features, etc
           
           To get mroe info about all foolowing data, please read http://wiki.domogik.org/DevelopersDatabase for "0.1.0 model"
      -->
      <device_technology>
        <id><!-- technology id. Available caracters : "[a-z][0-9]". Example : relayboard --></id>
        <name><!-- Displayed name of technology. Example : Relay board --></name>
        <description><!-- Description of technology. Example : Relay boards monitoring and controlling --></description>
      </device_technology>
      <device_types>
        <device_type>
          <id><!-- device type id. Available caracters : "[a-z][0-9]". Should be formatted like this : <technology>.<type>. Example : relayboard.relay --></id>
          <device_technology_id><!-- technology id. Example : relayboard --></device_technology_id>
          <name><!-- Displayed name of device type. Example : Relay --></name>
          <description><!-- Description of device type. Example : Relay --></description>
        </device_type>
        <device_type>
          <!-- another device type -->
        </device_type>
      </device_types>
      <device_feature_models>
        <device_feature_model>
          <id><!-- device feature model id. Available caracters : "[a-z][0-9]". Should be formatted like this : <technology>.<type>. Example : relayboard.relay.switch --></id>
          <name><!-- Displayed name of device feature model. Example : Switch --></name>
          <feature_type><!-- feature type : actuator, sensor. Example : actuator--></feature_type>
          <device_type_id><!-- device type id. Example : relayboard.relay --></device_type_id>
          <parameters>
              <!-- parameters for web UI. Example : {&amp;quot;output&amp;quot;:&amp;quot;&amp;quot;,&amp;quot;value0&amp;quot;:&amp;quot;low&amp;quot;, &amp;quot;value1&amp;quot;:&amp;quot;high&amp;quot;}-->
          </parameters>
          <value_type><!-- type of value returned by xpl messages : binary, number, string, etc (depanding on feature type : see online documentation) --></value_type>
          <stat_key><!-- stat key in database. Example : output --></stat_key>
          <return_confirmation><!--For an actuator, will device return a confirmaton ? 1=yes, 0=no. Example : 1--></return_confirmation>
        </device_feature_model>
        <device_feature_model>
          <!-- another device feature model -->
        </device_feature_model>
      </device_feature_models>  
    </package>   
    


__Notice :__ for __database part__ of the xml files, it is not very simple to fill it. With the next data model, we will make it differently, so it will be less difficult ;)

Feel free to come on irc to ask for our help or to use the mailing list.

Template : specific elements for "hardware" type
===========================================================
Set type = hardware
.. code-block::
    
    <package type="hardware"> 
    


Set no configuration element :
.. code-block::
    
    <configuration-keys/>
    


Add vendor id and device id :
.. code-block::
    
    <vendor-id><!--hardware vendor id--></vendor-id>
    <device-id><!--hardware device id--></device-id>
    


If external files are provided (for example sketch files for an arduino, etc), list them :
.. code-block::
    
    <external_files>                                                              
      <file path="src/external/hardware/<name for related 'hardware' plugin>/<file 1>"/>                       
      <file path="src/external/hardware/<name for related 'hardware' plugin>/<file 2>"/>                       
      ...
    </external_files> 
    


Load new data in database
==========================
If you update any __<device*>__ part of the xml, you will have to reload this file in database. This could be done like this :
.. code-block::
    
    cd src/tools/packages
    ./insert_data.py ../../share/domogik/plugins/<your plugin name>.xml
    
