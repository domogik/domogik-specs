!Domogik installation for developers
__*** Please note that this document may often change as the project is under development.***__
{maketoc}

!!Difference between this page and the [http://docs.domogik.org/domogik/dev/en/|official installation method page]
This page is about development version installation. Moreover, some tricks could be given here to customize Domogik for development purpose.
The official installation method page give the way to install a released version of Domogik.

!!Prerequisites

* Python 2.6/2.7
* Python 2.6/2.7 development package (for ssl support compile with setup.py). You can also directly install python-openssl.
* mysql-server-5.0 and libmysqlclient-dev for MySQL support. MySQL 5.1 is also supported. 
* libssl-dev (you can also directly install python-openssl)

There may be additional dependencies based upon your selection of plugins.  We recommend that you take care of these after you have installed Domogik, before you activate new plugins.

!!Installation
''Notice : if you want to install Domogik on several hosts, see the chapter __Installation on secondary hosts__ for the secondary hosts''

!!!Notes
* These examples assume Debian or another apt-based distribution (Ubuntu, etc). Adjust accordingly (eg, use yum instead if using RedHat-based distribution).
* Domogik includes its own xPL hub. If you are running another xPL hub on your target machine (xpl-perl, etc), you will want to stop it before installation. 

(TODO: Mac installation)

!!!In a nutshell
!!!!Dependencies
Python 2.6 or above is required; note that Python version 3.x is not supported.  

{CODE()}
# apt-get install python2.7
# ln -sf /usr/bin/python2.7 /usr/bin/python
{CODE}

Even if you have python2.6 or higher installed, check development package is also installed, or do :
{CODE()}                                          
# apt-get install python2.7-dev gcc
{CODE}

Install SSL librairies
{CODE()}
# apt-get install libssl-dev 
{CODE}

Install librairies for MySQL access and command line client :
{CODE()}
# apt-get install libmysqlclient-dev mysql-client
{CODE}

!!!!MySQL server
''If you have already installed MySQL server, you will only have to create the Domogik database.''

Install packages for MySQL server :
{CODE()}
# apt-get install mysql-server-5.0 libmysqlclient-dev
{CODE}
Or if MySQL 5.1 is available on your Linux system :
{CODE()}
# apt-get install mysql-server-5.1
{CODE}

Log on MySQL database as root user :
{CODE()}
$ mysql -u root -p
Enter password: 
{CODE}

Create a database &quot;domogik&quot; :
{CODE()}
mysql&gt; CREATE DATABASE domogik;
Query OK, 1 row affected (0.00 sec)
{CODE}

Create user &quot;domogik&quot; to use the new database :
{CODE()}
mysql&gt; GRANT ALL PRIVILEGES ON domogik.* to domogik@localhost IDENTIFIED BY 'domopass';
Query OK, 0 rows affected (0.00 sec)

mysql&gt;exit
{CODE}

!!!!Install the Domogik development release
Install mercurial package :
{CODE()}
# apt-get install mercurial
{CODE}

Grab the sources (with mercurial, see ((Use_mercurial|here for more information))) :
{CODE()}
git clone --recursive https://github.com/domogik/domogik.git
{CODE}

Go on the appropriate branch (example : 0.3) : 

{CODE()}
git checkout 0.3
{CODE}

Run the installation script :
''Note : during installation, a new user will be created if necessary.''
{CODE()}
$ cd domogik
$ sudo ./install.sh
{CODE}

You will be asked for the following questions :

{CODE()}
Which install mode do you want (choose develop if you don't know)? [install/develop] :
{CODE}
For development purpose, you should answer develop.

{CODE()}
If you want to use a proxy, please set it now. It will only be used during the installation. (ex: http://1.2.3.4:8080)
{CODE}
During the installation, some python librairies could be downloaded. If you use a proxy, you must set it here.

{CODE()}
Which user will run domogik, it will be created if it does not exist yet? (default : domogik)
{CODE}
System user that will launch Domogik. This user should have read and write permissions to sources. Ideally, choose the user with which you grab the sources.

{CODE()}
You already have Domogik configuration files. Do you want to keep them ? [Y/n]
{CODE}
If you already have Domogik configuration files, you will be asked for keeping them or not.

{CODE()}
Which interface do you want to bind to? (default : lo) :
{CODE}
To use Domogik only on a local computer, choose __lo__. To access it from another computer or use multi host features, choose appropriate network interface (e.g. : __eth0__).

{CODE()}
If you need to reach Domogik from outside, you can specify an IP now :
{CODE}
To use to access to Domogik from internet. You can set your public IP here (depending on your configuration, you could need to create a port redirection on your router.
Domogik is not yet secure, use this with caution!

{CODE()}
You need to have a working MySQL server with a domogik user and database.       
You can create it using these commands (as MySQL admin user) :                  
 &gt; CREATE DATABASE domogik;                                                     
 &gt; GRANT ALL PRIVILEGES ON domogik.* to domogik@localhost IDENTIFIED BY 'randompassword';                                                                       
Press Enter to continue the installation when your setup is ok.
{CODE}
If you have installed MySQL server and create the Domogik database, just press Enter.

{CODE()}
Please set your MySQL parameters.                                               
Username : domogik                                                              
Password : domopass                                                             
Port [3306] :                                                                   
Host [localhost] :                                                              
Database name [domogik]:
{CODE}
Set connection informations for the database.

{CODE()}
Your database already contains some tables, do you want to drop them. If you choose No, new items will *NOT* be installed ? [Y/n]
{CODE}
In case the Domogik database is not empty (it is not the first installation), you will get this warning. Depending on your needs choose the appropriate option. Y choice will delete all existing data.

{CODE()}
Everything seems to be good, Domogik should be installed correctly.             
I will start the test_config.py script to check it.                             
Please press Enter when ready.
{CODE}
Just press enter to start the check script.

{CODE()}
 ==&gt; ================================================== &lt;==                     
 ==&gt;  Everything seems ok, you should be able to start  &lt;==                     
 ==&gt;       Domogik with /etc/init.d/domogik start       &lt;==                     
 ==&gt;             or /etc/rc.d/domogik start             &lt;==                     
 ==&gt; ================================================== &lt;==
{CODE}
Installation is finished and seems to be OK.

!!!!Optional : postgresql (instead of MySQL)
If you wish to use postgresql instead of MySQL
* Create your database
* Edit your ''.domogik.cfg'' file and put database information : db_type (mysql or postgresql), db_user, db_password...

!!!!Make Domogik start with your computer
For Debian or Ubuntu systems:
{CODE()}
# update-rc.d domogik defaults
{CODE}

For Archlinux:
Add ''@domogik'' at the very end of the line starting with ''DAEMON''.

!!!!Start domogik
Then start Domogik!
{CODE()}
sudo /etc/init.d/domogik start
{CODE}

It will start : 
* The xpl hub
* The Domogik manager on this host
* The database manager and the REST interface module and will take in account your config.

Domogik is mutli-thread, so it could take some times before you can connect to it.

You can use the following command to manage domogik :
{CODE()}
sudo /etc/init.d/domogik start|stop|restart|status
{CODE}

Developpers can use the extended command (they are more verbose) to start/stop domogik and utilities:
{CODE()}
sudo /etc/init.d/domogik start|stop|restart|status xpl
sudo /etc/init.d/domogik start|stop|restart|status manager
{CODE}

!!!Logs
A file named __domogik__ is installed in __/etc/logrotate.d/__. You can update it to change the logrotate configuration.


!!Next step ?
* [http://docs.domogik.org/domoweb/dev/en/installation/index.html|Domoweb installation] !


!!!There is an error!!!
Please, feel free to consult ((Errors_and_solutions)) page : there may be a solution :)

!!Installation on secondary hosts
Domogik is multihost, but the installation will be different between the main host (which will have the database manager and rinor activated) and the others hosts (which will have only the manager activated).

!!!Dependencies
Just do the same actions you did for the main host

!!!!Install the Domogik development release
Do the same actions you did for the main host, except for the __install.sh__ shell script : to launch install for a secondary host, run the installation script with the __--secondary__ option :
{CODE()}
$ cd domogik
$ sudo ./install.sh --secondary
{CODE}