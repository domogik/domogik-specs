{maketoc}

!Purpose

TODO: ZiBase description

!Protocol list
* VISONIC433 : Protocol VISIONIC with frequency 433 MHz
* VISONIC868 : Protocol VISIONIC with frequency 868 MHz
* CHACON : Protocol CHACON for CHACON V2 + DIO series
* DOMIA : Protocol DOMIA for CHACON V1 + low cost devices  
* X10 : Protocol RF X10
* ZWAVE : Protocol ZWAVE
* RFS10 : Protocol RFS10/TS10
* XDD433AL : Protocol X2D alarme with frequency 433 MHz
* XDD868AL : Protocol X2D alarme with frequency 868 MHz
* XDD868INSH : Protocol X2D inter/shutter
* XDD868PILOT : Protocol X2D Pilot Wire 
* XDD868BOAC : Protocol X2D Boiler/AC

!Plugin configuration
!!Enabling plugin
You can enable plugin by using:
{CODE()}
dmgenplug zibase
{CODE}
You just have to reload administration page to see the plugin in the list.

!!Configuration
In Domogik administration, go to zibase configuration page.

!!!ip
IP of the ZiBase.


!!!interface
Network interface to connect your PC to your local network.

!!!port
Listening port for the reception of messages from the ZiBase.

!!!envar
Enable reading internal variable

!!!interv
Interval between each reading of the internal variables (in secondes)

!!Start plugin
You can now start the plugin (start button).

!Creating devices for ZiBase
In administration, go to Organization &gt; Devices page to create tour devices.

!!Actuators

!!!lamp device
Create a new device like this:

* Name : &quot;Living room&quot; (or whatever you want)
* Description : a short description (Placement, usage ,etc)
* Address : &lt;__Address device__&gt;:&lt;__protocol__&gt;. you should put : __G1:CHACON__ or __G2:X10__ or __G3:DOMIA__
* Reference : &quot;Zibase&quot; (or whatever you want)
* Usage : &quot;Light&quot; (for example)
* Feature :
** ZiBase.Switch provides only on/off
** ZiBase.Dimmer provides on/off and dim/bright

Examples :
{IMG(fileId=&quot;268|267&quot;)}{IMG}


((Setup_your_devices|Attribute the features to a place and you will be able to control your lamp.))

!!!appliance device
Create a new device like this:

* Name : &quot;Swimming pump&quot; (or whatever you want)
* Description : a short description (Placement, usage ,etc)
* Address : &lt;__Address device__&gt;:&lt;__protocol__&gt;. you should put : __G1:CHACON__ or __G2:X10__ or __G3:DOMIA__
* Reference : &quot;Zibase&quot; (or whatever you want)
* Usage : &quot;Appliance&quot; (for example)
* Feature : ZiBase.Switch

((Setup_your_devices|Attribute the features to a place and you can now control your appliance.))

!!Sensors

!!!Sensors list
* Oregon rain
* Oregon U.V (*)
* Oregon Anemometer
* Oregon Thermometer 
* Oregon Thermometer / Hygrometer
* OWL CM119 / CM130
* Digimax TS10 (*)
* ON/OFF Sensor (*)

(*) Sensor not tested

!!!Add a new sensor
Create a new sensor like this:

* Name : &quot;Swimming temp&quot; (or whatever you want)
* Description : a short description (Placement, usage ,etc)
* Address : &lt;__Address device__&gt; (Sensor ID in zibase configurator)
{IMG(fileId=&quot;274&quot;)}{IMG}
* Reference : &quot;Zibase&quot; (or whatever you want)
* Usage : &quot;Temperature&quot; (for example)
* Feature : ZiBase.Oregon Temperature

!!Internal variable

!!!Add an internal variable reading
* Name : &quot;Internal var&quot; (or whatever you want)
* Description : a short description (Usage ,etc)
* Address : &quot;VAR&quot; &amp; &lt;__number of the internal variable__&gt; ( for example : VAR1 for the internal variable number 1)
* Reference : &quot;Zibase&quot; (or whatever you want)
* Usage : whatever you want
* Feature : ZiBase.Internal VARs

!Helpers
''To get an introduction to helpers, you can read the ((Plugins_helpers|Helper documentation)). To use a helper, the plugin must be stopped.''

!Developper Notes
TODO:xpl schema
