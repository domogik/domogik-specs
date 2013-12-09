!Plugin mirror

This plugin documentation is now available on [http://docs.domogik.org/plugin/mirror/dev/en/]

!Plugin mirror - developer information
{maketoc}
!!xPL Schema 
The [http://xplproject.org.uk/wiki/index.php?title=Schema_-_SENSOR.BASIC|sensor.basic] schema is used by this plugin.

Here are the events for which a xPL message is sent :

!!!Mir:ror faced up
{CODE()}
xpl-trig
{
...
}
sensor.basic
{
device=mirror
type=activated
current=HIGH
}
{CODE}

!!!Mir:ror faced down
{CODE()}
xpl-trig
{
...
}
sensor.basic
{
device=mirror
type=activated
current=LOW
}
{CODE}

!!!A RFID element is detected
{CODE()}
xpl-trig
{
...
}
sensor.basic
{
device=
type=present
current=HIGH
}
{CODE}

!!!A RFID element is no more detected
{CODE()}
xpl-trig
{
...
}
sensor.basic
{
device=
type=present
current=LOW
}
{CODE}