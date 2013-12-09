^La traduction de cette page n'est pas terminée.^

.. toctree::



Ce plugin permet de communiquer avec des dispositifs 1-Wire.

Pour fonctionner, ce plugin à besoins de OWFS `OWFS <http://www.owfs.org>`_.

Liste des dispositifs pris en charge :
||__Composant__|__Fiche technique__|__Version Domogik__
DS18B20        | http://pdfserv.maxim-ic.com/en/ds/DS18B20.pdf | 0.1.0
DS18S20        | http://pdfserv.maxim-ic.com/en/ds/DS18S20.pdf | 0.1.0
DS2401         | http://datasheets.maxim-ic.com/en/ds/DS2401.pdf | 0.1.0
DS2438         | http://datasheets.maxim-ic.com/en/ds/DS2438.pdf | dev release||

Dans les prochaines versions, d'autres composants seront inclus.

*************************
Caractéristiques connues
*************************
Owfs 2.8p2 et owfs 2.8p3 ne fonctionnent pas très bien avec python.
====================================================================
Veuillez s'il vous plait, utiliser Owfs __2.7p38__ or __2.8p4__ (recommender).

Owfs ne semble pas fonctionner avec python 2.7
===============================================
Il fait l'erreur suivante:
.. code-block::
    
    Traceback (most recent call last):
      File "/home/cedric/sources/src/domogik/xpl/bin/onewire.py", line 42, in <module>
        from domogik.xpl.lib.onewire import OneWireException
      File "/home/cedric/sources/src/domogik/xpl/lib/onewire.py", line 42, in <module>
        import ow
      File "/usr/lib/python2.7/site-packages/ow/__init__.py", line 33, in <module>
        from ow import _OW
    ImportError: dynamic module does not define init function (init_OW)
    


******************************
Prerequis : installation OWFS
******************************
Ubuntu/Debian installation
===========================
Sur Ubuntu ou Debian, il existe des paquets OWFS (www.owfs.org) mais sont trop vieux. Donc, nous allons obtenir la dernière version des sources et les compiler.

Outils nécessaires pour compiler OWFS
**************************************
Pour commencer, nous avons besoin d'un compilateur __C compiler__ pour installer OWFS. Nous utiliserons __gcc__. Pour verifier si gcc est présent et sa version :
.. code-block::
    
    $ gcc --version
    

Si gcc est présent c'est Ok, sinon : 
.. code-block::
    
    # apt-get install gcc
    


Nous avons aussi besoin de make et ed :
.. code-block::
    
    # apt-get install make ed
    


Ensuite, nous aurons besoin dans __Autoconf__ version 2.57 ou supérieure. Pour voir si elle est disponible:
.. code-block::
    
    $ autoconf --version
    

Sinon installé-la : 
.. code-block::
    
    # apt-get install autoconf
    $ autoconf --version 
    version 2.65 
    


Nous aurons aussi besoin des librairies de développement USB : 
.. code-block::
    
    # apt-get install libusb-dev
    


Puis, installer swig :
.. code-block::
    
    # apt-get install swig
    


Owfs
=====
Telecharger OWFS (adapter les lignes à votre version) et extraire le paquet :
.. code-block::
    
    # cd /usr/src
    #  wget http://downloads.sourceforge.net/project/owfs/owfs/2.8p4/owfs-2.8p4.tar.gz
    # tar xvzf owfs-2.8p4.tar.gz
    # cd owfs-2.8p4
    


Configurer OWFS avec python :
.. code-block::
    
    # ./configure --with-python 
    # make
    As root / with sudo :
    # make install
    


OWFS est maintenant installé pour python

Test OWFS
**********
Pour tester vous devez faire ceci :
.. code-block::
    
    $ python
    >>> import ow
    >>> print ow.__version__                                                        
    2.8p4-1.18                
    



*****************
Wiring standards
*****************
See [http://owfs.org/index.php?page=wiring-standards]

********
DS9490R
********
{img attId="258"}
Permissions
============

By default, you need to be root to access onewire network. To give access to everybody on your computer to onewire device, follow these instructions.

First, get vendor and product ids :
.. code-block::
    
    $ lsusb  | grep DS1490
    Bus 006 Device 013: ID 04fa:2490 Dallas Semiconductor DS1490F 2-in-1 Fob, 1-Wire adapter
    


Here, vendor id is 04fa and product id is 2490 (they will be the same for all DS1490).

Create an udev rule for onewire in file __/etc/udev/rules.d/onewire.rules__ :
.. code-block::
    
    SUBSYSTEMS=="usb", ATTRS{idVendor}=="04fa", ATTRS{idProduct}=="2490", SYMLINK+="onewire", MODE="0666"
    

If you don't have a DS9490, you should adapt vendor and product id.

You just have to unplug and plug back your DS9490 to have permissions on it as a non root user.

Connection
===========
{img attId="283"}

*********************
Plugin configuration
*********************
Enabling plugin
================
You can enable plugin by using :
.. code-block::
    
    $ dmgenplug onewire
    


You just have to reload administration page to see the plugin in the list.

Configuration
==============
In Domogik administration, go to 1wire configuration page.

device
*******
This is the 1 wire device. Here are possible values : 
* u (default) : USB controller.
* /dev/ttyS0 : serial port (adapt the number to your situation)
* remote_system:3003 : address of owserver

cache
******
Tells if you want to use the OWFS cache or not.
* True (default) : use the cache 
* False: don't use the cache
Reading data on 1 wire netowrk is a slow operation, so if you read lot of data, it could be usefull to use cache.
More informations on http://owfs.sourceforge.net/caching.html

others...
**********
There are others configuration items which depends on components. You will find them in components chapters of this page



Start plugin
=============
You can now start the plugin (start button).

Check plugin works
===================

In Helper tool, launch this command : __onewire all u__

This should return all components on your onewire network

.. code-block::
    
    onewire all u
    | Family | Component id | Type    |
    -----------------------------------
    | 28     | C57B2E020000 | DS18B20 |
    | 01     | 4507B2130000 | DS2401  |
    | 81     | 93702C000000 | DS1420  |
    


********
DS18B20
********
How to plug 
=============
Parasit mode
*************
{img attId="46"}

Configuration items
====================
ds18b20-en
***********
Enabling (or not) DS18B20 components support.
* True : enable support
* False (default) : disable support

ds18b20-int
************
Interval between each DS18B20 component reading. If you want to monitor your house temperature, 60 or 120s is a good value. If you want to monitor something where temperature can change quickly, you can put a small value (5s for example) but you will have to set __cache__ to False to get instant values.
Default : 60s

ds18b20-res
************
Resolution of temperature read on onewire network. Possible values are : 
* 9 : 9 bits resolution
* 10 : 10 bits resolution
* 11 : 11 bits resolution
* 12 : 12 bits resolution
If you set another value, first component read will fail and next read will use 12 bits resolution.

Default : 12

Note that the resolution has an impact on time for reading temperature on device. On ((Maxim site|http://www.maxim-ic.com/app-notes/index.mvp/id/4377)) you will find this table which indicate time taken for each resolution : 

||Resolution  |9 bit  |10 bit  |11 bit  |12 bit
Conversion Time (ms) |93.75 |187.5 |375 |750
LSB (Â°C) |0.5 |0.25 |0.125 |0.0625||
Configuration examples
=======================
For all these examples, set __ds18b20-en = True__

Monitoring my house temperatures
*********************************
You sould set __ds18b20-int__ between 60 seconds and 300 seconds (5 minutes) depending on the precison you want to have. Less than 60 seconds is useless, more than 300 seconds could be not sufficient for managing temperature.

Creating a device for a DS18B20
================================
In administration, go to __Organization > Devices__ page. Create a new device like this :
* Name : a name ("Temperature", "Kitchen temp", ... as you wish) 
* Description : a short description (DS18b20 placement, etc)
* Address : the DS18b20 id (you can get it with this helper command : __onewire ds18b20__ which will give you all your DS18B20 detected)
* Reference : "DS18B20" (you can also put everything else)
* Usage : "Temperature"
* Type : "1Wire.Thermometer"

Example : 
{img attId="179"}

((Setup_your_devices|Attribute the feature to a place and you can now see your temperature)):)


********
DS18S20
********
Difference with DS18B20
========================
The DS18__B__20 component offers 4 resolutions for temperature : 9 ~ 12 bits. The DS18__S__20 offers only a 9bits resolution.

How to plug 
=============
Parasit mode
*************
{IMG(attId="69")}{IMG}

Normal mode
************
{IMG(attId="70")}{IMG}

Configuration items
====================
ds18sS0-en
***********
Enabling (or not) DS18S20 components support.
* True : enable support
* False (default) : disable support

ds18s20-int
************
Interval between each DS18S20 component reading. If you want to monitor your house temperature, 60 or 120s is a good value. If you want to monitor something where temperature can change quickly, you can put a small value (5s for example) but you will have to set __cache__ to False to get instant values.
Default : 60s


Configuration examples
=======================
See DS18B20 component for examples.

Creating a device for a DS18S20
================================
See DS18B20 component for indications.
*******
DS2401
*******
How to plug 
=============
Parasit mode
*************
{IMG(attId="63")}{IMG}

Configuration items
====================
ds2401-en
**********
Enabling (or not) DS2401 components support.
* True : enable support
* False (default) : disable support

ds2401-int
***********
Interval between each DS2401 component reading. Interval to set depends on the usage you will have for DS2401 comopnents.
Default : 5s

Configuration examples
=======================
For all these examples, set __ds2401-en = True__

Opening sensor for a garage door
*********************************
A garage door is somethong that take time to close/open, especially when it has a motor. Opening or closing such a door can take 15 seconds, so there is no risk that someone open and close your door without DS2401 seeing it with a 5 seconds value.

Creating a device for a DS2401
===============================
In administration, go to __Organization > Devices__ page. Create a new device like this :
* Name : a name ("Kitchen window", ... as you wish) 
* Description : a short description (DS2401placement, etc)
* Address : the DS2401 id (you can get it with this helper command : __onewire ds2401__ which will give you all your DS2401 detected)
* Reference : "DS2401" (you can also put everything else)
* Usage : "Shutter" (for example)
* Type : "1Wire.Serial Number"

Example : 
{img attId="180"}

((Setup_your_devices|Attribute the feature to a place and you can now see the status of your DS2401 (present or not)))

******************************************************
DS2438 in MS-T module (not in 0.1.0 : in dev release)
******************************************************
__Notice : as MS-T is only supported actually, only temperature feature is fully supported.__
{img attId="284"}

How to plug 
=============
{IMG(attId="290")}{IMG}

Configuration items
====================
ds2438-en
**********
Enabling (or not) DS2438 components support.
* True : enable support
* False (default) : disable support

ds2438-int
***********
Interval between each DS2438 component reading. Interval to set depends on the usage you will have for DS2438 comopnents.
Default : 60s

Configuration examples
=======================
TODO

Creating a device for a DS2438Z
================================
TODO


********
Helpers
********
''To get an introduction to helpers, you can read the ((Plugins_helpers|Helper documentation)). To use a helper, the plugin must be stopped.''

__Warning :__ for some reasons, it is not a good idea to use both onewire helper and onewire plugin : you could obtain permissions issues... These issues could even force you to reboot your computer or wait a long time before using back plugin or helper. So, you should only use helper when plugin is stopped and don't start plugin when using helper. It is a sad thing and we will look how to correct these bug (which is linked to ow library). If you got a solution about this, feel free to report it :)

__Notice about <device> parameter :__ <device> parameter has the same possible values as defined in "configuration > device". For the following examples we will use the "u" device which is Usb adaptor.

onewire all <device>
===========================
__onewire all__ will list all onewire components found on your 1 wire network.

Example : 
.. code-block::
    
    onewire all u
    | Family | Component id | Type    |
    -----------------------------------
    | 28     | C57B2E020000 | DS18B20 |
    | 01     | 4507B2130000 | DS2401  |
    | 81     | 93702C000000 | DS1420  |
    


onewire detail <device> <component id> 
====================================================
__onewire detail__ will display all attributes of <component id> component.

Example : 
.. code-block::
    
    onewire detail u C57B2E020000
    C57B2E020000 attributes :
    * address : 28C57B2E0200005D
    * crc8 : 5D
    * die : C2
    * family : 28
    * fasttemp : 25
    * id : C57B2E020000
    * locator : FFFFFFFFFFFFFFFF
    * power : 0
    * present : 1
    * r_address : 5D0000022E7BC528
    * r_id : 0000022E7BC5
    * r_locator : FFFFFFFFFFFFFFFF
    * temperature : 25.1875
    * temperature10 : 25.25
    * temperature11 : 25.25
    * temperature12 : 25.1875
    * temperature9 : 25
    * temphigh : 75
    * templow : 70
    * trim : 56247
    * trimblanket : 0
    * trimvalid : 0
    * type : DS18B20
    


onewire ds18b20 <device>
===============================
__onewire ds18b20__ will display important data about all DS18B20 components found.

Example : 
.. code-block::
    
    onewire ds18b20 u
    DS18B20 : id=C57B2E020000
    * Temperature : 25.125
    * Powered (1) / parasit (0) : 0	
    


onewire ds18s20 <device>
===============================
__onewire ds18s20__ will display important data about all DS18S20 components found.

Example : 
.. code-block::
    
    onewire ds18s20 u
    DS18S20 : id=F1F0DB010800
    * Temperature : 28.75
    * Powered (1) / parasit (0) : 0
    


onewire ds2401 <device>
==============================
__onewire ds2401__ will display important data about all DS2401 components found.

Example : 
.. code-block::
    
    onewire ds2401 u
    DS2401 : id=4507B2130000
    * Present : 1
    




*****************
Developper notes
*****************
How to add a new component support ?
=====================================
||TODO all following points||
* add options,
* create class,
* call class with options if good option enabled
* update description xml file for options
* update stats xml file
* xpl-stat/xpl-trig
* rules to choose xpl schema

xpl-stat or xpl-trig 
======================
When a value is read and sent by 1 wire plugin, here is the rule which must be followed :
.. code-block::
    
    IF <previous value> DIFFERENT FROM <new value> 
    THEN use xpl-trig
    ELSE use xpl-stat
    



DS18B20 and DS18S20
====================
xPL messages
*************
When temperature change for a DS18B20 (or DS18S20) component : 
.. code-block::
    
    xpl-stat                                                                    
    {                                                                               
    ...
    }                                                                               
    sensor.basic                                                                    
    {                                                                               
    device=<component id>
    current=<temperature value in degree (celcius)>
    type=temp                                                                       
    }      
    


When temperature doesn't change : 
.. code-block::
    
    xpl-trig                                                                    
    {                                                                               
    ...
    }                                                                               
    sensor.basic                                                                    
    {                                                                               
    device=<component id>
    current=<temperature value in degree (celcius)>
    type=temp                                                                       
    }      
    



    
**************
Related links
**************
http://owfs.sourceforge.net/install.html
http://tomasz.korwel.net/2006/07/02/owfs-instalation-on-ubuntu-606/
