***************
Plugin wol_ping
***************

This plugin documentation is now available on [http://docs.domogik.org/plugin/wol\_ping/dev/en/]

***************************************
Plugin wol_ping - developer information
***************************************

.. toctree::



WOL part
========
xPL client listens to the xPL network in order to get command messages ''control.basic'' with ''device="computer"'' and ''type="wakeonlan"''. When one is detected, it sends a magic packet to the mac address defined in ''mac'' option on port defined in ''wol-port'' for computer name defined in ''name''.

xPL schema
**********
* `Control.basic <http://xplproject.org.uk/wiki/index.php/Schema\_-\_CONTROL.BASIC>`_
* `Sensor.basic <http://xplproject.org.uk/wiki/index.php/Schema\_-\_SENSOR.BASIC>`_

When the plugin gets a ''control.basic message'', it sends a magic packet to the mac address specified in the xPL command.

!!!!Message to send to plugin for asking to start a computer
To ask a plugin to send a magic packet, you should send this __xpl-cmnd__ message :
.. code-block::
    
    CONTROL.BASIC
    {
    DEVICE=
    TYPE=wakeonlan
    CURRENT=HIGH
    }
    


!!!!Message sent by plugin when it successfully send a magic packet
It is a __xpl-trig__ message :
.. code-block::
    
    SENSOR.BASIC
    {
    DEVICE=
    TYPE=wakeonlan
    CURRENT=HIGH
    }
    


/command
********
Here is the url to use by UI to wake up a computer with ''dyonisos'' as computer name: __http://ip:port/command/computer/dyonisos/wol__

Ping part
=========
Each ''ping-interval'' seconds, plugin will ping all computers defined in configuration options. When getting a status for a computer, a xPl message is sent.

xPL schema
**********
* `Sensor.basic <http://xplproject.org.uk/wiki/index.php?title=Schema\_-\_SENSOR.BASIC>`_

It is a __xpl-trig__ message if status evolved and __xpl-stat__ message if status doesn't evolved :
.. code-block::
    
    SENSOR.BASIC
    {
    DEVICE=
    TYPE=ping
    CURRENT=
    }
    

