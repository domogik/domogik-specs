.. toctree::


********
Purpose
********
This hardware plugin aims to control one RGB leds strip with an arduino and xPL.

{IMG(attId="301")}{IMG}

**************
Prerequisites
**************
You will need :
* 1 Arduino Uno
* 1 Arduino's ethernet shiled based on wizenet
{IMG(attId="277")}{IMG}

* 1 12V DC power supply
* 1 RGB Led strip
* 1 10kOhm resistor
* 1 push button
* 1 100kOhm round potentiometer (potentiometer value can be different)
* 1 ULN2003 component

Schematics
===========
__Notice__ : on following schematics, we don't see ethernet shield. As ethernet shield is plugged on arduino, they use the same pins, so there is no nood to show it.

''All schematics are made with `Fritzing <http://fritzing.org/>`_''

Complete schematic source for 500mA/color max (please read chapter __Power analysis__):


{ATTACH(name="ar_rgb-complete.fz",file="ar_rgb-complete.fz",id="309",dls="1",icon="1")}{ATTACH}

All schematic sources and pictures are also available :
* on Domogik repository : src/external/hardwares/ar_rgb/schematics-and-pictures/.
* in plugin's package : __TODO : path in package__.


For breadboard testing
***********************
Here, RGB led strip is shown as a single RGB led. You just have to connect the led strip where the led is placed.
{IMG(attId="296")}{IMG}

Schematic
**********
{IMG(attId="295")}{IMG}

PCB
****
''\_\_Notice :\_\_ I didn't make a PCB as I used a test circuit. With `Fritzing <http://fritzing.org/>`_ and schematic sources, you can easily generate a PCB. Feel free to send it us in order to share with others :)''


***************
Power analysis
***************
Known data
===========
The led strip
**************
We will take as example a RGB led strip of 5m which needs 12V to work and consume 30W for displaying white light (all three colors are at full intensity).

ULN2003 component
******************
This component contains several `Darlingtons <http://en.wikipedia.org/wiki/Darlington\_transistor>`_. Each output can deliver up to 500mA. With the following schematic, we can deliver up to 500mA to each color of the led strip :
{IMG(attId="310")}{IMG}

To deliver up to 1A to a color, you can group inputs and outputs like this :
{IMG(attId="311")}{IMG}

Max intensity needed for a color
=================================
The led strip consume 30W (maximum) for three colors, so one color will consume 10W (maximum).
.. code-block::
    
    I = P/V = 10W / 12V = 833mA
    

For this full led strip we need to be able to deliver 833mA per color. __We will need to adapt the ULN2003 connection (see ''Power analysis > ULN2003 component chapter'') to use the full led strip!!__.

Which maximum length can I use with the basic schematic (up to 500mA per color) ?
==================================================================================
.. code-block::
    
    Pfull=833mA
    Lfull=5m
    Pwanted=500mA
    Lwanted=?
    
    Lwanted = (Pwanted * Lfull) / Pfull = (500 * 5) / 833 = 3m
    

We can use 3meters of RGB led strip with the simple schematic (up to 500mA/color)

Choosing a power supply
========================
Here, we need a 12V power supply which could support the 30W of the led strip and the arduino. I don't exactly know how much an arduino consume. I suppose (if you got informations, please send them to me) it won't exceed 500mA.
Example for 5 meters of the example led strip : 
*************************************************
.. code-block::
    
    I = P/V = 30/12 = 2.5A
    or  
    I = Ired + Igreen + Iblue = 833mA + 833mA + 833mA = 2.5A
    

We add the 500mA of the arduino and we got a __12V / 3A__ power supply.

Example for 3 meters of the example led strip : 
*************************************************
.. code-block::
    
    I = Ired + Igreen + Iblue = 500mA + 500mA + 500mA = 1.5A
    

We add the 500mA of the arduino and we got a __12V / 2A__ power supply.

************************
Load program on arduino
************************
Arduino's files are available :
* on Domogik repository : src/external/hardwares/ar_rgb/*.pde
* in plugin's package : __TODO : path in package__.

Install arduino IDE
====================
See `the official website tutorial <http://www.arduino.cc/playground/Learning/Linux>`_

Configure sketch
=================
First, modify __ar_rgb.pde__ like this :

.. code-block::
    
    ...
    
    /***************** Network configuration ********************/
    
    // Mac address : a mac address must be unique
    byte mac[] = {0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED};
    // IP address : the value will depend on your network
    byte ip[] = {192, 168, 1, 160};
    // Broadcat address's first three elements should be the same than ip. The last should be 255.
    byte broadCastIp[] = {192, 168, 1, 255};
    // Udp local port used (any value you want between 1024 and 65536)
    unsigned int localPort = 3865;  
    // xPL protocol port (keep default value unless you know what you are doing)
    unsigned int xplPort = 3865;  
    

In this block, change only __ip__ and __broadCastIp__ to adapt them to your local network.

.. code-block::
    
    /***************** xPL configuration part *******************/
    
    // Source. Format is <vendor id>-<device id>.<instance>
    
    // Vendor id and device id should not be changed
    // Instance should be the location of your arduino and RGB led strip : living, bedroom, etc
    // Instance should only use letters or numbers! (no underscore, ...)
    #define MY_SOURCE "arduino-rgb.parentsbedroom"
    
    // Name of device in body of xpl message
    // This should be the same as previously defined instance
    #define MY_DEVICE "parentsbedroom"
    
    // Maximal size of xPL messages that could be processed
    // This size should not be reduce unless you are sure of what you are doing
    #define MAX_XPL_MESSAGE_SIZE 165
    
    // Heartbeat interval : time in minutes between 2 sends of a xpl hbeat message
    #define HBEAT_INTERVAL 1
    

Here, you should only change __MY_SOURCE__ and __MY_DEVICE__ by replacing "parentsbedroom" to the place where you will place the led strip (16 caracters max, only letters or numbers, no spaces, underscore, ...). Be careful : device and the end of source should be the same (I used 2 variables for eventual futur evolutions)!

Examples :
* MY_SOURCE "arduino-rgb.kitchen"
* MY_DEVICE "kitchen"

* MY_SOURCE "arduino-rgb.livingroom"
* MY_DEVICE "livingroom"


.. code-block::
    
    /******************** RGB configuration**********************/
    
    // Define which PWM pins to use
    #define RED_PIN 3
    #define GREEN_PIN 5
    #define BLUE_PIN 6
    
    // define potentiometer pin
    #define ANALOG_CONTROL A0
    
    // define button pin
    #define BUTTON_CONTROL 8
    
    /******************* END OF CONFIGURATION *******************/
    
    ...
    

Here, adapt eventually the pins if you change the connections (be careful, ethernet shiel uses several pins : see its documentation in order to not use them).

Upload sketch on arduino
=========================
Pour ce projet, j'ai utilisé la version 22 de l'environnement de développement arduino. La dernière version de la librairie Udp étant plus complète, j'ai ajouté cette version dans l'environnement de développement. Il vous suffit de télécharger les fichiers Udp.cpp et Udp.h depuis cette url : https://github.com/arduino/Arduino/tree/master/libraries/Ethernet.
Puis remplacez les fichiers de même nom dans le dossier librairies/Ethernet/ de l'environnement de développement.
Cette version permet notamment de gérer plusieurs sockets simultanément. Elle devrait être incluse dans la prochaine version de l'environnement de développement (23).
I used the version 22 of the IDE for this project. But I updated the UDP library with the latest available on https://github.com/arduino/Arduino/tree/master/libraries/Ethernet. It allowed to handle multiple sockets in the same time. It should be available in the version 23 of the IDE.

See `the official website tutorial <http://arduino.cc/en/Guide/Environment>`_

Test it manually :)
====================
First, check il manual control is OK. If not, you got a problem!

*********************************
Install ar_rgb plugin on Domogik
*********************************
''Actually, Domogik doesn't support yet packages, so to test the Domogik support of this arduino project, you need to test it from Domogik sources and default branch''.

Check arduino is seen by Domogik
=================================
When going in administration page, you should the __ar_rgb__ hardware plugin in the plugins list :
{IMG(attId="312")}{IMG}
 
If not, there is a problem : check network configuration of arduino.

Create device
==============
Create a device like this :
{IMG(attId="313")}{IMG}

Address must correspond to what you defined in __MY_DEVICE__ in ar_rgb.pde. It will also correspond to the instance name (which you can see in plugins list).

Place widget
=============
Go in visualisation mode and place __Color > RGB Color Picker__ widget.

Use widget
===========
Bug in actual widget on first use with no stats for device
***********************************************************
When you first create the device, and arduino is off or don't raise events (color changes), the widget has a bug : it will be displayed like this until first stat got in database. This bug will be corrected of course ;)
{IMG(attId="314")}{IMG}

State off
**********
When leds are off, widget is like this. To switch leds on, just clic on top left icon.

{IMG(attId="315")}{IMG}

State on
*********
When leds are on, chromatic wheel is activated. You just have to choose a color. To turn leds off, just click on top left icon.

{IMG(attId="302")}{IMG}



***************
Specifications
***************

Generating RGB color codes with only one input
===============================================
The idea is to make a conversion from HSL (hue, saturation, lightness) format to RGB (red, green, blue) format.
* HSL (en) : http://en.wikipedia.org/wiki/HSL_and_HSV
* HSL (fr) : http://fr.wikipedia.org/wiki/Teinte_saturation_lumi%C3%A8re
* RGB (en) : http://en.wikipedia.org/wiki/RGB_color_model
* RGB (fr) : http://fr.wikipedia.org/wiki/Rouge_vert_bleu
* Different color conversion formulas : http://www.easyrgb.com/index.php?X=MATH#text21

I create the following script to generate this result (screenshot from a html page) : 

{IMG(attId="279")}{IMG}

.. code-block::
    
    <?
    $S = 1;
    $L = 0.6;
    for ($i=0;$i<=1;$i+=0.005) {
        echo "<div style='background-color:" . get_rgb_code($i, $S, $L) . ";";
        echo "            height: 1px;";
        echo "           '></div>";
    }
    
    function get_rgb_code($H, $S, $L) {
        // HSL : 0..1
        // RGB : 0..255
        if ( $S == 0 ) {
           $R = $L * 255; 
           $G = $L * 255;
           $B = $L * 255;
        }
        else {
           if ( $L < 0.5 ) 
               $var_2 = $L * ( 1 + $S );
           else      
               $var_2 = ( $L + $S ) - ( $S * $L );
    
           $var_1 = 2 * $L - $var_2;
    
           $R = 255 * Hue_2_RGB( $var_1, $var_2, $H + ( 1 / 3 ) );
           $G = 255 * Hue_2_RGB( $var_1, $var_2, $H );
           $B = 255 * Hue_2_RGB( $var_1, $var_2, $H - ( 1 / 3 ) );
        }
        return "#" . dechex($R) . dechex($G) . dechex($B);
    }
    
    function Hue_2_RGB( $v1, $v2, $vH ) {
       if ( $vH < 0 ) $vH += 1;
       if ( $vH > 1 ) $vH -= 1;
       if ( ( 6 * $vH ) < 1 ) return ( $v1 + ( $v2 - $v1 ) * 6 * $vH );
       if ( ( 2 * $vH ) < 1 ) return ( $v2 );
       if ( ( 3 * $vH ) < 2 ) return ( $v1 + ( $v2 - $v1 ) * ( ( 2 / 3 ) - $vH ) * 6
     );
       return ( $v1 );
    }
    ?>
    


The same thing is to do for the arduino.

Xpl protocol
=============
* Port used : 3865

.. code-block::
    
    2011-05-17 23:08:23.838808 - xpl-cmnd
    {
    hop=1
    source=xpl-rest.domogik
    target=*
    }
    arduino.rgb
    {
    device=parentsbedroom
    command=setcolor
    color=off
    }
    
    2011-05-17 23:08:23.905372 - xpl-trig
    {
    hop=1
    source=arduino-rgb.parentsbedroom
    target=*
    }
    arduino.rgb
    {
    command=setcolor
    device=parentsbedroom
    color=#000000
    }
    
    2011-05-17 23:08:29.769817 - xpl-stat
    {
    hop=1
    source=arduino-rgb.parentsbedroom
    target=*
    }
    hbeat.app
    {
    interval=1
    port=3865
    remote-ip=192.168.1.160
    mac=de:ad:be:ef:fe:ed
    color=#cbb401
    }
    
    
    
    
    
    
    2011-05-17 23:08:59.766750 - xpl-cmnd
    {
    hop=1
    source=xpl-rest.domogik
    target=*
    }
    arduino.rgb
    {
    device=parentsbedroom
    command=setcolor
    color=on
    }
    
    2011-05-17 23:08:59.834177 - xpl-trig
    {
    hop=1
    source=arduino-rgb.parentsbedroom
    target=*
    }
    arduino.rgb
    {
    command=setcolor
    device=parentsbedroom
    color=#cbb401
    }
    
    
    
    
    
    
    
    2011-05-17 23:09:16.597749 - xpl-cmnd
    {
    hop=1
    source=xpl-rest.domogik
    target=*
    }
    arduino.rgb
    {
    device=parentsbedroom
    command=setcolor
    color=#cb0101
    }
    
    2011-05-17 23:09:16.667910 - xpl-trig
    {
    hop=1
    source=arduino-rgb.parentsbedroom
    target=*
    }
    arduino.rgb
    {
    command=setcolor
    device=parentsbedroom
    color=#cb0101
    }
    






