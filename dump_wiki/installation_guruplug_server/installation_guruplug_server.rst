!Installation of Domogik on a Guruplug

!!Introduction
My first wish was to intall Domogik on my NAS (a netgear Readynas Nv) but the sparc processor is not enough powerfull.
So I will use a [http://www.globalscaletechnologies.com/p-31-guruplug-server-standard.aspx|Guruplug Server] to install Domogik, mysql will be hosted on the NAS,

!!Open the box
What is a guruplug server ? : an ARM processor with Debian Lenny :)
It seems that there is a problem connecting the guruplug to a gigabit switch ([http://stevemilner.org/blog/2010/05/17/hello-guruplug-you-jerk/|here]). So you can use the wifi.
Tha guruplug automatically create an open wifi network named Plug2-uAP-xxxx.
Remember it is totally open.
The default ip address is 192.168.1.1. There is a smal wen interface [http://192.168.1.1/|here]
Connect with ssh :{CODE()}# ssh root@xxx.xxx.xxx.xxx{CODE}The password is &quot;nosoup4u&quot;

Update the apt sources :
{CODE()}deb http://ftp.us.debian.org/debian/ lenny main contrib non-free
deb http://http.us.debian.org/debian stable main contrib non-free
deb http://security.debian.org lenny/updates main contrib non-free
deb http://debian.advalem.net/debian-backports/ lenny-backports main contrib non-free
#deb http://www.backports.org/debian lenny-backports main contrib non-free
#deb http://10.82.108.51/kedars/sheevaplug_wifi/builds/packages/ binary/
{CODE}I change the backports mirror with the french one. Update it to your needs. The last line is a private repository used by the guruplug developpers. It's a bad news, no wifi updates are available using apt.

Update the package list :
{CODE()}#apt-get update{CODE}
And finish the previous installation :
{CODE()}#dpkg --configure -a{CODE}

Links :
[http://plugcomputer.org/plugwiki/index.php/GuruPlug]

!!!Build python
Only python 2.5 is available in Lenny. We need python 2.6/2.7 to run domogik.
Add the sources of wheezy to apt
{CODE()}deb-src http://ftp.fr.debian.org/debian/ wheezy main contrib non-free
{CODE}
Install the buid tools :
debhelper cdbs lintian build-essential fakeroot devscripts pbuilder dh-make debootstrap


Build ncurses
Get the sources :
{CODE()}apt-get source ncurses
{CODE}
Resolve the build dependencies :
 ncurses-5.9/debian/control
change debhelper dependency from 8.1.3 to 8.1

!!!Installing a cross compiler for armel
{CODE()}sudo apt-get install linux-libc-dev-armel-cross libc6-armel-cross libc6-dev-armel-cross binutils-arm-linux-gnueabi gcc-4.4-arm-linux-gnueabi g++-4.4-arm-linux-gnueabi
sudo apt-get install apt-cross dpkg-cross{CODE}


Links :
[http://wiki.debian.org/EmdebianToolchain]