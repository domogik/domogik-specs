!Plugin ipx800

This plugin documentation is now available on [http://docs.domogik.org/plugin/ipx800/dev/en/]

!Developper notes

{maketoc}

!!!Finding an IPX relay board
TO discover all IPX relay boards on local network, you can send the following message on UDP (port 30303) : 
{CODE()}
Discovery: Who is out there?
{CODE}

All IPX relay boards will answser 
{CODE()}
&lt;name of relay board&gt;
&lt;mac address of relay board&gt;
{CODE}

!!!Get actual card status
You can get the actual status of the card with this url : http://ip:port/status.xml

This will give this xml data :

{CODE()}
&lt;response&gt;
&lt;led0&gt;0&lt;/led0&gt;
&lt;led1&gt;1&lt;/led1&gt;
&lt;led2&gt;1&lt;/led2&gt;
&lt;led3&gt;0&lt;/led3&gt;
&lt;led4&gt;1&lt;/led4&gt;
&lt;led5&gt;0&lt;/led5&gt;
&lt;led6&gt;0&lt;/led6&gt;
&lt;led7&gt;0&lt;/led7&gt;
&lt;btn0&gt;up&lt;/btn0&gt;
&lt;btn1&gt;up&lt;/btn1&gt;
&lt;btn2&gt;up&lt;/btn2&gt;
&lt;btn3&gt;up&lt;/btn3&gt;
&lt;an1&gt;81&lt;/an1&gt;
&lt;an2&gt;0&lt;/an2&gt;
&lt;time0&gt;07:40:19&lt;/time0&gt;
&lt;count1&gt;0&lt;/count1&gt;            # beta feature on IPX
&lt;count2&gt;0&lt;/count2&gt;            #
&lt;count3&gt;0&lt;/count3&gt;            #
&lt;count4&gt;0&lt;/count4&gt;            #
&lt;/response&gt;
{CODE}
* ledX : status of each relay (0 =&gt; OFF, 1 =&gt; ON)
* btnX : status of each digital input (up =&gt; ON, down =&gt; OFF)
* anX : value of each analog input (0 for 0V, 1024 for 3.3V)
* countX : value of each counter (0...)
 
!!!API
!!!!Change the relay state
Calling this url will change a relay state 
http://ip:port/leds.cgi?led=N  (N=0..7)

Example : 
* change relay 0 state : http://ip:port/leds.cgi?led=0
* change relay 2 state : http://ip:port/leds.cgi?led=2
 
!!!!Send a pulse to the relay
Calling this url will send a pulse to the relay
http://ip:port/rlyfs.cgi?rlyf=N  (N=0..7)

Example : 
* send a pulse to  relay 0 : http://ip:port/rlyfs.cgi?rlyf=0
* send a pulse to  relay 2 : http://ip:port/rlyfs.cgi?rlyf=2
 
Note : sending a pulse to a relay that is already in state 1, will only put it to state 0 after pulse duration

!!!!Reset counter  -- beta feature on IPX
Calling this url will reset a counter :
http://ip:port/counter.cgi?count=N (N=0..3)

Example : 
* Reset counter 0 : http://ip:port/counter.cgi?count=0
* Reset counter 2 : http://ip:port/counter.cgi?count=2

!!!!/command
Here are the url to use for each feature of IPX800 board. &quot;address&quot; is &lt;boardname&gt;-&lt;element type (led, btn...)&gt;&lt;number of element&gt;

Switch : 
* /command/relayboard/&lt;address&gt;/high
* /command/relayboard/&lt;address&gt;/low
Trigger : 
* /command/relayboard/&lt;address&gt;/pulse

||TODO : reset counter when implemented||

!!!xPL Schema
!!!!xpl-cmnd
The COMMAND.BASIC xPL schema is used in this module : http://xplproject.org.uk/wiki/index.php?title=Schema_-_CONTROL.BASIC

{CODE()}
CONTROL.BASIC
{
DEVICE=&lt;device name&gt;
TYPE=&lt;device type&gt;
CURRENT=&lt;value sent to the device&gt;
}
{CODE} 
* device : &lt;relay board name in plugin config&gt;-&lt;element : btn0, btn1...&gt;
* type : 
** output for a relay
** count for the counter
* current : 
** HIGH, LOW, PULSE for a relay
** 0 to reset counter

!!!!xpl-stat
There is no usage of xpl-stat with this plugin

!!!!xpl-trig
The SENSOR.BASIC xPL schema is used in this module : http://xplproject.org.uk/wiki/index.php?title=Schema_-_SENSOR.BASIC

{CODE()}
SENSOR.BASIC
{
DEVICE=&lt;device name&gt;
TYPE=&lt;device type&gt;
CURRENT=&lt;current value&gt;
}
{CODE}
* device : &lt;relay board name in plugin config&gt;-&lt;element : btn0, btn1...&gt;
* type : 
** output for a relay
** input for the digital input
** voltage for the analog input
** count for the counter
* current : 
** HIGH, LOW for a relay (there is no PULSE value here)
** 0 to reset counter

A xpl-trig message is sent at each status change for board's elements.

