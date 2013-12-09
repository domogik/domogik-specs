.. toctree::



********
Purpose
********
Diskfree plugin send disk usage on xPL

*********************
Plugin configuration
*********************
Enabling plugin
================
You can enable plugin by using :
.. code-block::
    
    dmgenplug diskfree
    


You just have to reload administration page to see the plugin in the list.

Configuration
==============
In Domogik administration, go to diskfreeconfiguration page.

interval
*********
Interval (minutes) between each check of disk usage.

path-X
*******
Path on your filesystem where you want to check free, used, total space.

Start plugin
=============
You can now start the plugin (start button).

*******************************
Creating a device for Diskfree
*******************************
In administration, go to __Organization > Devices__ page. Create a new device like this :
* Name : Whatever you want to name a path on filesystem
* Description : Whatever you want to describe a path on filesystem
* Address : a path on your filesystem /, /home/user, /media/disk, etc
* Reference : anything you want
* Usage : Computer, Server
* Type : "Computer.Disk usage"

Example :

''TODO''

A device will give you several features :
* free space : free space for path
* used space : used space for path
* total space : total space for path
* percent used : percent of space used for path

((Setup_your_devices|Attribute the features to a place and you can now see the informations about your disk usage.



*****************
Developper notes
*****************
xPL Schema 
============
The `sensor.basic <http://xplproject.org.uk/wiki/index.php?title=Schema\_-\_SENSOR.BASIC>`_ schema is used by this plugin.

Four messages are sent for each path check. There is one message per type : 
* type=free_space
* type=used_space
* type=total_space
* type=percent_used

Values are in kbyte forfree, used and total space. Percent used is a percent.
On __xpl-stat__ is used by this plugin :
.. code-block::
    
    xpl-stat
    {
    ...
    }
    sensor.basic
    {
    device=<path>
    type=<free_space, used_space, total_space, percent_used>
    current=<value>
    }
    

