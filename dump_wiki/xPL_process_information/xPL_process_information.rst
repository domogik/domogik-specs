!Get process information over the xPL network
{maketoc}
!!Purpose
Domogik plugins are able to send over the xPL network their cpu and memory usage. Each plugin that inherits from XplPlugin does it naturally. The goal is to display charts in Domogik administration (web ui) about each plugin for cpu and memory usage.

!!How it works
in __xpl/common/plugin.py__, an object ProcessInfo (from common/processinfo.py) is created. It will get process information and send them to a callback function which will send the data over xPL.

!!xPL Schema

!!!xpl-stat
{CODE()}
xpl-stat
{
...
}
domogik.usage
{
name = &lt;plugin name&gt;.&lt;host&gt;
pid = &lt;process id&gt;
cpu-percent = [0..100]
memory-percent = [0..100]
memory-rss = &lt;float&gt;
memory-vsz = &lt;float&gt;
[ futur additionnal values : thread number, etc]
}
{CODE}

Memory RSS and VSZ corresponds to :
* RSS : memory used by plugin and its data
* VSZ : memory used for cache and buffers

!!!xpl-cmnd
No xpl-cmnd usage

!!!xpl-trig
No xpl-cmnd usage