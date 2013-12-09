!Plugin wol_ping

This plugin documentation is now available on [http://docs.domogik.org/plugin/wol_ping/dev/en/]

!Plugin wol_ping - developer information

{maketoc}

!!WOL part
xPL client listens to the xPL network in order to get command messages ''control.basic'' with ''device="computer"'' and ''type="wakeonlan"''. When one is detected, it sends a magic packet to the mac address defined in ''mac'' option on port defined in ''wol-port'' for computer name defined in ''name''.

!!!xPL schema
* [http://xplproject.org.uk/wiki/index.php/Schema_-_CONTROL.BASIC|Control.basic]
* [http://xplproject.org.uk/wiki/index.php/Schema_-_SENSOR.BASIC|Sensor.basic]

When the plugin gets a ''control.basic message'', it sends a magic packet to the mac address specified in the xPL command.

!!!!Message to send to plugin for asking to start a computer
To ask a plugin to send a magic packet, you should send this __xpl-cmnd__ message :
{CODE()}
CONTROL.BASIC
{
DEVICE=
TYPE=wakeonlan
CURRENT=HIGH
}
{CODE}

!!!!Message sent by plugin when it successfully send a magic packet
It is a __xpl-trig__ message :
{CODE()}
SENSOR.BASIC
{
DEVICE=
TYPE=wakeonlan
CURRENT=HIGH
}
{CODE}

!!!/command
Here is the url to use by UI to wake up a computer with ''dyonisos'' as computer name: __http://ip:port/command/computer/dyonisos/wol__

!!Ping part
Each ''ping-interval'' seconds, plugin will ping all computers defined in configuration options. When getting a status for a computer, a xPl message is sent.

!!!xPL schema
* [http://xplproject.org.uk/wiki/index.php?title=Schema_-_SENSOR.BASIC|Sensor.basic]

It is a __xpl-trig__ message if status evolved and __xpl-stat__ message if status doesn't evolved :
{CODE()}
SENSOR.BASIC
{
DEVICE=
TYPE=ping
CURRENT=
}
{CODE}
