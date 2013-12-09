!Plugin onewire

This plugin documentation is now available on [http://docs.domogik.org/plugin/onewire/dev/en/]



!Plugin onewire - developer information
{maketoc}

!!How to add a new component support ?
||TODO all following points||
* add options,
* create class,
* call class with options if correct option enabled
* update description xml file for options
* update stats xml file
* xpl-stat/xpl-trig
* rules to choose xpl schema

!!xpl-stat or xpl-trig 
When a value is read and sent by 1 wire plugin, here is the rule which must be followed :
{CODE()}
IF  DIFFERENT FROM  
THEN use xpl-trig
ELSE use xpl-stat
{CODE}


!!DS18B20, DS18S20, DS2438
!!!xPL messages
When temperature changes for a DS18B20 (or DS18S20) component : 
{CODE()}
xpl-stat                                                                    
{                                                                               
...
}                                                                               
sensor.basic                                                                    
{                                                                               
device=
current=
type=temp                                                                       
}      
{CODE}

When temperature doesn't change : 
{CODE()}
xpl-trig                                                                    
{                                                                               
...
}                                                                               
sensor.basic                                                                    
{                                                                               
device=
current=
type=temp                                                                       
}      
{CODE}

For DS2438, for the humidity the same messages will be used with __type=humidity__
    
!!Related links
http://owfs.sourceforge.net/install.html
http://tomasz.korwel.net/2006/07/02/owfs-instalation-on-ubuntu-606/
