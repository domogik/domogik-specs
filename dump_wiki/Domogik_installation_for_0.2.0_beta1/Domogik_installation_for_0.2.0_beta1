!Standard installation for Domogik 0.2.0-beta1
{maketoc}

!!Installation
!!!Notes
* These examples assume Debian or another apt-based distribution (Ubuntu, etc).  Adjust accordingly (eg, use yum instead if using RedHat-based distribution).
* Domogik includes its own xPL hub.  If you are running another xPL hub on your target machine (xpl-perl, etc), you will have to stop it before installation.

!!!Dependencies
Check your Python version with : 
{CODE()}
python -V
{CODE}
__Please note:__ Right now Domogik __requires Python 2.6/2.7__. Python 3 is not (yet) supported.

If you don't already have Python 2.6/2.7 or above (you have it if you are running a recent Linux system), then you can run for example: 
{CODE()}
# apt-get install python2.7
# ln -sf /usr/bin/python2.7 /usr/bin/python
{CODE}

Even if you have python2.6 or higher installed, check that the development package is also installed, or install them :
{CODE()}                                          
# apt-get install python2.7-dev gcc
{CODE}

Install SSL librairies
{CODE()}
# apt-get install libssl-dev 
{CODE}

Install librairies for mysql access and command line client :
{CODE()}
# apt-get install libmysqlclient-dev mysql-client
{CODE}

!!!Mysql server
''If you have already a Mysql server installed, you will only have to create the Domogik database.''

Install packages for mysql server :
{CODE()}
# apt-get install mysql-server-5.0
{CODE}
Or if mysql 5.1 is available on your Linux system :
{CODE()}
# apt-get install mysql-server-5.1
{CODE}

Log on the mysql database as root user :
{CODE()}
$ mysql -u root -p
Enter password: 
{CODE}

Create a database called &quot;domogik&quot; :
{CODE()}
mysql&gt; CREATE DATABASE domogik;
Query OK, 1 row affected (0.00 sec)
{CODE}

Create the user &quot;domogik&quot; to use the new database :
{CODE()}
mysql&gt; GRANT ALL PRIVILEGES ON domogik.* to domogik@localhost IDENTIFIED BY 'domopass';
Query OK, 0 rows affected (0.00 sec)

mysql&gt;exit
{CODE}

!!!Download Domogik
Go on the ((Download|download page)) to get Domogik.
You will get a file named __domogik-&lt;release&gt;.tgz__. Download it and extract it :
{CODE()}
$ wget http://repo.domogik.org/...
$ tar xvzf domogik-&lt;release&gt;.tgz
$ cd domogik-&lt;release&gt;
{CODE}

!!!Install Domogik 
From __domogik-&lt;release&gt;__ folder, run the install :
''Note : during installation, a new user will be created if necessary.''
{CODE()}
$ sudo ./install.sh
{CODE}

You will be asked for the following questions :

{CODE()}
If you want to use a proxy, please set it now. It will only be used during the installation. (ex: http://1.2.3.4:8080)
{CODE}
During the installation, some python librairies could be downloaded. If you use a proxy, you must set it here.

{CODE()}
Which user will run domogik, it will be created if it does not exist yet? (default : domogik)
{CODE}
System user that will launch Domogik. You should keep the default choice.

If the choosen user doesn't exists, you will have to answser following questions : 
{CODE()}
Enter new UNIX password: 
...
Retype new UNIX password: 
...
Changing the user information for domogik
Enter the new value, or press ENTER for the default
	Full Name []: 
	Room Number []: 
	Work Phone []: 
	Home Phone []: 
	Other []: 
Is the information correct? [Y/n] 
...
{CODE}
Enter twice a password for the user and eventually, fill values about the new user.

{CODE()}
You already have Domogik configuration files. Do you want to keep them ? [Y/n]
{CODE}
If you already have Domogik configuration files, you will be asked for keeping them or not.

{CODE()}
Which interface do you want to bind to? (default : lo) :
{CODE}
To use Domogik only on a local computer, choose __lo__. To access it from another computer or use multi host features, choose the appropriate network interface (e.g. : __eth0__).

{CODE()}
If you need to access Domogik from outside, you can specify an IP now :
{CODE}
Used to access to Domogik over the internet. You can set your public IP here (depending on your configuration, you could need to create a port redirection on your router.
Domogik is not yet secure, use this with caution!

{CODE()}
You need to have a working Mysql server with a domogik user and database.       
You can create it using these commands (as mysql admin user) :                  
 &gt; CREATE DATABASE domogik;                                                     
 &gt; GRANT ALL PRIVILEGES ON domogik.* to domogik@localhost IDENTIFIED BY 'randompassword';                                                                       
Press Enter to continue the installation when your setup is ok.
{CODE}
If you have installed Mysql server and create the Domogik database, just press Enter.

{CODE()}
Please set your mysql parameters.                                               
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
The installation is finished and seems to be OK.

!!!Optional : postgresql (instead of mysql)
If you wish to use postgresql instead of mysql
* Create your database
* Edit your ''.domogik.cfg'' file and put database information : db_type (postgresql), db_user, db_password...

!!!Make Domogik start with your computer
For Debian or Ubuntu systems:
{CODE()}
# update-rc.d domogik defaults
{CODE}

For Archlinux:
Add ''@domogik'' at the very end of the line starting with ''DAEMON''.

!!!Start domogik
{CODE()}
sudo /etc/init.d/domogik start
* Starting XPL... Done.
* Starting Manager (with -d -r -p -E)... Done
* Updating packages cache... Done
{CODE}

It will start : 
* The xpl hub
* The Domogik manager on this host
* The database manager and the REST interface module and will take in account your config.

Domogik is mutli-thread, so it could take some times before you can connect to it.

!!!Logs
A file named __domogik__ is installed in __/etc/logrotate.d/__. You can update it to change the logrotate configuration.

!!!It doesn't work?
* ((Errors_and_solutions|See errors and solutions))

!!Next step ?
* ((Domoweb_installation_for_developpers|Domoweb installation)) 

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