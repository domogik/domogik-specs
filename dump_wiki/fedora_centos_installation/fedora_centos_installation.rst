!Installing Domogik on Fedora / Centos / Redhat 6

We are working hard to include domogik on Fedora and EPEL official repository. If you want to try rpm release package you first need to add Cquad repository.

!! Add Cquad repository

For fedora 16 : 
{CODE()}yum install http://cquad.dyndns.org/repo/fedora/16/i386/cquad-repo-fedora-1.0-0.2.fc16.noarch.rpm --nogpgcheck{CODE}

For fedora 15 : 
{CODE()}yum install http://cquad.dyndns.org/repo/fedora/15/i386/cquad-repo-fedora-1.0-0.2.fc16.noarch.rpm --nogpgcheck{CODE}

For Centos/RHEL 6 :
{CODE()}yum install http://cquad.dyndns.org/repo/epel/6/i386/cquad-repo-el6-1.0-0.2.el6.noarch.rpm --nogpgcheck{CODE}

!! Install domogik

On Fedora 15/16 and Centos 6 :
{CODE()}yum install domogik{CODE}

When it's done follow documentation instruction :
{CODE()}cat /usr/share/doc/domogik-0.20/README.Fedora{CODE}
{CODE()}
New installs
============

1. Unless you are already using the MySQL server or you are running it
   remotely you will need to ensure that the server is installed:

     yum install mysql-server

2. You will need to create the domogik database. You can create it using 
   these commands (as mysql admin user) :&quot;
   &gt; CREATE DATABASE domogik;&quot;
   &gt; GRANT ALL PRIVILEGES ON domogik.* to domogik@127.0.0.1 IDENTIFIED BY 'randompassword';&quot;

3. The database configuration is not set by default, you will need to edit
   this file to set it:

     /etc/domogik/domogik.cfg

4. Calling Application Installer
     
     su -c &quot;python /usr/share/domogik/install/installer.py&quot; domogik

5. You can now start domogik
     
     service domogik start{CODE}

!! Install domoweb

On Fedora 15/16 and Centos 6 :
{CODE()}yum install domoweb{CODE}

When it's done follow documentation instruction :
{CODE()}cat /usr/share/doc/domoweb-0.20/README.Fedora{CODE}
{CODE()}
New installs
============

1. Calling Application Installer
     
     su -c &quot;python /usr/lib/python2.*/site-packages/domoweb/manage.py syncdb --noinput&quot; domogik

2. You can now start domogik
     
     service domoweb start{CODE}


