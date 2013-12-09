**************
Plugin ipx800
**************


This plugin documentation is now available on [http://docs.domogik.org/plugin/ipx800/dev/en/]

*****************
Developper notes
*****************


.. toctree::



Finding an IPX relay board
***************************

TO discover all IPX relay boards on local network, you can send the following message on UDP (port 30303) : 
.. code-block:: json


    
    Discovery: Who is out there?
    


All IPX relay boards will answser 
.. code-block:: json


    
    <name of relay board>
    <mac address of relay board>
    


Get actual card status
***********************

You can get the actual status of the card with this url : http://ip:port/status.xml

This will give this xml data :

.. code-block:: json


    
    <response>
    <led0>0</led0>
    <led1>1</led1>
    <led2>1</led2>
    <led3>0</led3>
    <led4>1</led4>
    <led5>0</led5>
    <led6>0</led6>
    <led7>0</led7>
    <btn0>up</btn0>
    <btn1>up</btn1>
    <btn2>up</btn2>
    <btn3>up</btn3>
    <an1>81</an1>
    <an2>0</an2>
    <time0>07:40:19</time0>
    <count1>0</count1>            # beta feature on IPX
    <count2>0</count2>            #
    <count3>0</count3>            #
    <count4>0</count4>            #
    </response>
    

* ledX : status of each relay (0 => OFF, 1 => ON)
* btnX : status of each digital input (up => ON, down => OFF)
* anX : value of each analog input (0 for 0V, 1024 for 3.3V)
* countX : value of each counter (0...)
 
API
****

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
Here are the url to use for each feature of IPX800 board. "address" is <boardname>-<element type (led, btn...)><number of element>

Switch : 
* /command/relayboard/<address>/high
* /command/relayboard/<address>/low
Trigger : 
* /command/relayboard/<address>/pulse

||TODO : reset counter when implemented||

xPL Schema
***********

!!!!xpl-cmnd
The COMMAND.BASIC xPL schema is used in this module : http://xplproject.org.uk/wiki/index.php?title=Schema_-_CONTROL.BASIC

.. code-block:: json


    
    CONTROL.BASIC
    {
    DEVICE=<device name>
    TYPE=<device type>
    CURRENT=<value sent to the device>
    }
    
 
* device : <relay board name in plugin config>-<element : btn0, btn1...>
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

.. code-block:: json


    
    SENSOR.BASIC
    {
    DEVICE=<device name>
    TYPE=<device type>
    CURRENT=<current value>
    }
    

* device : <relay board name in plugin config>-<element : btn0, btn1...>
* type : 
** output for a relay
** input for the digital input
** voltage for the analog input
** count for the counter
* current : 
** HIGH, LOW for a relay (there is no PULSE value here)
** 0 to reset counter

A xpl-trig message is sent at each status change for board's elements.

