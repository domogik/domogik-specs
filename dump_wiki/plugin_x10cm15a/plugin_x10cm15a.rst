{maketoc}

!Purpose
X10 is an automation technology which allows to switch and dim lights, control appliances, etc. This plugin allows to control X10 devices if you got a __CM15A__ / __CM15PRO__ adaptator. If you want to use another adaptator, check if there are available plugins for these adaptators.

!How to plug
/!\change cm15 pic
{img fileId=&quot;185&quot; thumb=&quot;y&quot; alt=&quot;&quot; rel=&quot;box[g]&quot;} {img fileId=&quot;184&quot; thumb=&quot;y&quot; alt=&quot;&quot; rel=&quot;box[g]&quot;}

On the left the CM15A module which is used to send commands to all x10 plugged in modules.
On the right a LM12 module used to control a lamp.
!cm15a
This plugin uses the linux driver to use CM15 adaptator. So, you will first need to install the driver.

!!Installation
More information can be find [http://www.linuxha.com/USB/cm15a.html|here]
If already plugged, deplug cm15 module, and get [http://www.linuxha.com/common/iplcd/iplc-driver.tgz|iplc-driver.tgz]
{CODE()}
tar zxvf iplc-driver.tgz

ln -s /usr/src/linux-headers-$(uname -r)/include/generated/autoconf.h /usr/src/linux-headers-$(uname -r)/include/linux/autoconf.h

cd iplc/driver/linux-2.6/cm15a.d # or Linux 2.4 if you need support for 2.4
make
sudo insmod cm15a.ko # You need to be root
ls -l /dev/cm15a*
{CODE}

If you want to give the rights to the domogik user, you can create /etc/udev/rules.d/98-cm15a.rules, and add : 
{CODE()}
KERNEL==&quot;cm15a0&quot;, BUS==&quot;usb&quot;, SYSFS{idVendor}==&quot;0bc7&quot;, SYSFS{idProduct}==&quot;0001&quot;, NAME=&quot;cm15a0&quot;, OWNER=&quot;domogik&quot;
{CODE}

Then, deplug/plug in your CM15 device. You should have a /dev/cm15 link created :
{CODE()}
# ls -l /dev/cm15a0
lrw------- 1 domogik domogik 7 2010-07-19 09:50 /dev/cm15a0
{CODE}

Note that &quot;cm15a0&quot; may change on your installation.



!!!Try using an appliance
Plug in an appliance device (using A1 code for example) and run :
{CODE()}
echo sur /dev/cm15a0 ?
{CODE}
The appliance should switch on. Now run :
{CODE()}
echo sur /dev/cm15a0 ?
{CODE}
The appliance should switch off.

!!!Try using a lamp 
Plug in a lamp device (using A2 code for example) and run :
{CODE()}
echo sur /dev/cm15a0 ?
{CODE}
The lamp should switch on. Now, run (one or more times) :
{CODE()}
echo sur /dev/cm15a0 ?
{CODE}
This command lowers brightness of 10 units each time you call it. So, your lamp intensity should decrease. Now, run : 
{CODE()}
echo sur /dev/cm15a0 ?
{CODE}
This command increases brightness of 10 units each time you call it. So, your lamp intensity should increase.

!Plugin configuration
!!Enabling plugin
You can enable plugin by using (from your domogik directory) :
{CODE()}
dmgenplug x10cm15a
{CODE}

You just have to reload administration page to see the plugin in the list.

!!Configuration
In Domogik administration, go to x10_cm15a configuration page.

!!!cm15a-cfg-path
Path to cm15a config file
Default : /dev/cm15a0
The default value (/dev/cm15a0) should be fine. When set don't forget to save it!

!!Start plugin
You can now start the plugin (start button).

!Creating x10 devices
!!Creating a lamp device
In administration, go to __Organization &gt; Devices__ page. Create a new device like this :
* Name : Short name, like &quot;Hall&quot;
* Description : Device details, like &quot;Hall light&quot;
* Address : X10 address, like &quot;A4&quot;
* Reference : X10 module's model, only for information, like &quot;LM12&quot;
* Type : 
** X10.switch (provides only on/off)
** X10.dimmer (provides on/off and dim/bright)
* Usage : Light

Example : 

{IMG(attId=&quot;194&quot;)}{IMG}   {IMG(attId=&quot;195&quot;)}{IMG}

((Setup_your_devices|Attribute the features to a place and you can now control your lamp)).

!!Creating an appliance device
In administration, go to __Organization &gt; Devices__ page. Create a new device like this :
* Name : Short name, like &quot;Coffee machine&quot;
* Description : Describe your coffee machine if you want!
* Address : X10 address, like &quot;A3&quot;
* Reference : X10 module's model, only for information, like &quot;AM12&quot;
* Type : X10.switch
* Usage : Appliance

((Setup_your_devices|Attribute the features to a place and you can now control your appliance)).

!Developper Notes

!!xPL schema
The [http://xplproject.org.uk/wiki/index.php?title=Schema_-_X10.BASIC|x10.basic] schema is used.

!!/command
{CODE()}
/command/x10/&lt;address&gt;/on # switch on the lamp / appliance
/command/x10/&lt;address&gt;/off # switch off the lamp / appliance
{CODE}
''Only for lamps'' 
{CODE()}
/command/x10/&lt;address&gt;/dim/&lt;value&gt; # dim units by &lt;level&gt; (1-22) (decrease brightness)
/command/x10/&lt;address&gt;/bright/&lt;value&gt; # brighten units by &lt;level&gt; (1-22) (increase brightness)
{CODE}
Note that these values are relative.