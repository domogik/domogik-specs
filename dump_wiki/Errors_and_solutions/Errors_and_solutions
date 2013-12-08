!Errors and solutions
{maketoc}

!!Domogik doesn't work, how to debug it ?

First, check the log files for ERROR messages.

If you don't find any, check if your xpl hub is working. You can use the tool __send.py__ to send a test message and __dump_xpl.py__ to check if you received it.

If all is OK at this point, you may try so start the plugin (or manager/rest/dbgmr) which has an issue in a shell with the -f option (example : ./onewire.py -f) and check if there are uncaught errors on stdout.

!!Installation issues
!!!libmysqlclient issue on Ubuntu 12.04
!!!!Error
{CODE()}
ImportError: libmysqlclient_r.so.16: cannot open shared object file: No such file or directory
{CODE}

!!!!Solution
Ubuntu install the libmysqlclient in release 18. Just create a symlink : 
{CODE()}
ln -v /usr/lib/i386-linux-gnu/libmysqlclient_r.so.18 /usr/lib/i386-linux-gnu/libmysqlclient_r.so.16
{CODE}




!!Browser
!!!My browser never ends loading the page
!!!!Error
The loading indicator of your browser never stops loading

!!!!Cause
This is not an error. Domogik always listen for events on the REST server so in fact loading never stops :)

!!xPL Hub
!!!xPL Hub doesn't start (C version) 
!!!!Error
When manualy launching the xPL Hub, you get :
{CODE()}
$ ./xPL_Hub                                                                       
bash: ./xPL_Hub: Aucun fichier ou dossier de ce type
{CODE}

!!!!Cause
You may be on a 64bits system with no 32bits glibc library

!!!!Solution
Install the 32bits glibc. Example for Archlinux :

{CODE()}
pacman -S lib32-glibc
{CODE}

!!Manager
!!!ConfigParser.NoSectionError: No section: 'domogik'  (v0.1)
!!!!Error
{CODE()}
...
ConfigParser.NoSectionError: No section: 'domogik'                              
Exception AttributeError: &quot;__Singl_BasePlugin instance has no attribute '_log'&quot; 
in &lt;bound method __Singl_BasePlugin.__del__ of &lt;domogik.xpl.common.baseplugin.__
Singl_BasePlugin instance at 0xc4ccb0&gt;&gt; ignored                                 
Exception AttributeError: &quot;'NoneType' object has no attribute 'debug'&quot; in &lt;bound
 method __Singl_xPLPlugin.__del__ of None&gt; ignored            
{CODE}

!!!!Cause
There is no ~/.domogik/domogik.cfg file or it has a bad format

!!!!Solution
Create or fix the problem in this file.

!!REST/RINOR
!!!REST doesn't start
!!!!Error
In rest.log you only get :
{CODE()}
2010-05-21 16:16:41,150 domogik-rest INFO Daemonize plugin rest
2010-05-21 16:16:41,151 domogik-rest DEBUG watcher fork
2010-05-21 16:16:41,151 domogik-rest DEBUG New system manager instance for rest
2010-05-21 16:16:41,152 domogik-rest DEBUG xPL plugin rest socket bound to 127.0.0.1, port 58975
2010-05-21 16:16:41,153 domogik-rest DEBUG New timer registered : &lt;domogik.xpl.lib.xplconnector.xPLTimer&gt; name : internal-timer
2010-05-21 16:16:41,154 domogik-rest DEBUG New listener, filter : {'xpltype': 'xpl-stat', 'schema': 'hbeat.app'}
2010-05-21 16:16:41,155 domogik-rest DEBUG xPL thread started for rest 
2010-05-21 16:16:41,155 domogik-rest DEBUG New listener, filter : {'xpltype': 'xpl-cmnd', 'schema': 'domogik.system'}
2010-05-21 16:16:41,155 domogik-rest DEBUG end single xpl plugin
2010-05-21 16:16:41,155 domogik-rest DEBUG after watcher
{CODE}

If you launch REST manually (./rest.py -f), you get :
{CODE()}
create Base plugin instance
new query
{CODE}

!!!!Cause
There are two possibilities : 
* The xPL Hub is not launched
* The Database Manager wasn't able to give REST his configuration

!!!!Solution
!!!!!The xPL Hub is not launched
Launch it. To check if it is started, run this command:
{CODE()}netstat -lun{CODE}
If you see a line displaying the port 3865 then it is running.

!!!!!The Database Manager wasn't able to give REST his configuration
Launch it manually (./dbmgr.py -f). Launch REST and see which error happens (see Database Manager section to see errors)

!!!REST doesn't start
!!!!Error
In stdout you get : 
{CODE()}
Traceback (most recent call last):
  File &quot;/root/configure-hgrc/domogik/src/domogik/xpl/bin/rest.py&quot;, line 3839, in &lt;module&gt;
    rest_server.start_http()
  File &quot;/root/configure-hgrc/domogik/src/domogik/xpl/bin/rest.py&quot;, line 444, in start_http
    handler_params = [self])
  File &quot;/root/configure-hgrc/domogik/src/domogik/xpl/bin/rest.py&quot;, line 496, in __init__
    bind_and_activate)
TypeError: __init__() takes exactly 3 arguments (4 given)
{CODE}

!!!!Cause
REST is not compatible with python 2.5

!!!!Solution
Install python 2.6

!!!Rest /plugin/detail/&lt;plugin name&gt; makes xpl_hub (c version) crashes
!!!!Error
A /plugin/detail/cidmodem (for example) REST request makes xpl_hub crash in a __segmentation fault__

!!!!Cause
It happens only with the -xpldebug option for xpl_hub

!!!!Solution
Use the hub without -xpldebug option

!!!REST is slow
!!!!Error
For example, the config page of plugins takes more than 5 seconds to be displayed

!!!!Cause
Definitely due to DNS issue. Check rest.log times, especially the time between :
* domogik-rest DEBUG Send HTTP header for OK, and 
* domogik-rest DEBUG Send HTTP data : {...}
If the difference is something like 5s, your DNS setup may be bad.

!!!!Solution
If you have ''avahi'' running (at least on a Ubuntu Desktop install), it could be stopped unless you know that you need it. That should solve your problem.
If you don't have such software, check your DNS setup, one quick way to check (without using domogik) is to run the command :
&lt;pre&gt;
time getent hosts the.ip.of.client
&lt;/pre&gt;
If it takes long time without any answer, your setup is wrong.

!!!!Solution with a karotz on the LAN
You must assign a host name to your Karotz on your local network.

!!Plugins
!!!Plugin don't start automatically
!!!!Error
After rebooting the server, plugins marked as &quot;Automatically start plugin at Domogik startup&quot; don't start.
Plugins start correctly after doing ''/etc/init.d/domogik restart''.
!!!!Cause
Domogik starts before mysql and doesn't load plugins.
!!!!Solution (Debian)
After the installation process, if you did:
{CODE()}update-rc.d -f domogik defaults{CODE}
It generates the following symlinks:
{CODE()}
/etc/rc1.d/K02domogik
/etc/rc2.d/S01domogik
/etc/rc3.d/S01domogik
/etc/rc4.d/S01domogik
/etc/rc5.d/S01domogik
{CODE}
Add ''mysql'' to the ''/etc/init.d/domogik'' :
{CODE()}# Required-Start: $local_fs $network *mysql*{CODE}
Now, these symlinks are generated :
{CODE()}
/etc/rc1.d/K02domogik
/etc/rc2.d/S20domogik
/etc/rc3.d/S20domogik
/etc/rc4.d/S20domogik
/etc/rc5.d/S20domogik
{CODE}
Mysql starts before domogik (S19) and all is OK.

!!!Plugin onewire and hardware usb issue
!!!!Error
All was working with 6 DS18B20 in parasite mode, i add 4 new one on the onewire bus (still in parasite mode) and starting having problems.
The plugin start correctly but stop working after few minutes or hours it depends.
Plugin is still working and still send xpl-stat command but no answer from the hardware (you could see that in the onewire.log file).

!!!!Cause
I use a simple usb hub without power supply, Teleinfo hardware, DS9490R Usb adaptor and a Mir:ror are powered on.
!!!!Solution
If you see some ttyusb error in dmesg don't look around it's a usb power problem. Removing the Mir:ror or adding a power supply on the Usb Hub remove the problem.

Now you can enjoy long time tracking without any hole.
