This page explain how to create an ubuntu repository for the packages of domogik/domoweb.

Add a user to manage repository
================================

We need a user to run the repository scritpts. It need a GPG key to sign the index files.
.. code-block:: json


    #sudo adduser --home /home/repository --shell /bin/bash --group repository{CODE}
    Assign a password to the user
.. code-block:: json


    #sudo passwd repository{CODE}
Genereate a key
.. code-block:: json


    #su repository
    #gpg --genkey 
    


Install reprepro
=================

.. code-block:: json


    #sudo apt-get install reprepro{CODE}
    Create a conf directory in the repository. You need to put the reprepro configuration file in it.
.. code-block:: json


    
    #mkdir /home/repository/conf
    

We also need to create some directories and fix security attributes.
Keep in mind that we are sharing some of these directories with apache.
.. code-block:: json


    
    #mkdir db dists logs scripts pool keys
    

.. code-block:: json


    
    #chmod o+rx dists logs pool keys
    #chmod o-rx db scripts
    

Add a "distributions" file in the conf directory with the following content :
.. code-block:: json


    Origin: packages.domogik.org
    Label: Domogik repository
    Codename: oneiric
    Architectures: amd64 i386 armel source
    Components: universe
    Description: Ubuntu repository for Domogik and dependances
    Uploaders: uploaders
    SignWith: repository4domogik@gmail.com
    Contents: .bz2
    
    Origin: packages.domogik.org
    Label: Domogik repository
    Codename: precise
    Architectures: amd64 i386 armel source
    Components: universe
    Description: Ubuntu repository for Domogik and dependances
    Uploaders: uploaders
    SignWith: repository4domogik@gmail.com
    Contents: .bz2
    
Origin : the address of the repository
Label : a short description
Description : a long description
Codename : must be the name of a real distribution
Components : universe or main
Architecture : all the architectures holded by the repository
Contents : will be compresses using bz2
Uploaders : the list of developpers authorizes to upload packages.
SignWith : the key generated previously. Use gpg --list-keys to retrieve it.

Create a file conf/incoming
.. code-block:: json


    Name: oneiric
    IncomingDir: /home/ftp/incoming/oneiric
    TempDir: tmp/oneiric
    Allow: oneiric
    Cleanup: on_deny on_error
    
    Name: precise
    IncomingDir: /home/ftp/incoming/precise
    TempDir: tmp/precise
    Allow: precise
    Cleanup: on_deny on_error
    
We defined 2 incomings directory, one for oneiric and another for precise.

Create a file scripts/import-new-packages.sh. We can use it to maually add packages... code-block:: json


    #!/bin/bash
    BASEDIR=/home/repository
    
    # Import package to distribution.
    reprepro -V -b $BASEDIR processincoming oneiric
reprepro -V -b $BASEDIR processincoming precise{CODE}And create a /etc/cron.d/repository to call it every 5 mins with cron... code-block:: json


    # /etc/cron.d/repository
SHELL=/bin/sh
PATH=/home/repository/scripts:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

*/5 * * * *   repository import-new-packages.sh
{CODE}You can also add /etc/logrotate.d/repository
.. code-block:: json


    /home/repository/logs/*.log {
            weekly
            missingok
            rotate 7
            copytruncate
            compress
            notifempty
            create 644 repository repository
    }
    


Ftp and Http
=============

Now, you should create an anonymous user (ftp in this tutorial) with no password for your ftp server. dupload will use it to upload packages. It's also possible to use a scp connection to do it.
Every body can write to it, but reprepro will check the packages keys before adding them. If the uploader is not allowed, reprepro will delete the files.
Create the incoming directories :
.. code-block:: json


    #mkdir  /home/ftp/incoming/oneric
    #mkdir  /home/ftp/incoming/precise
    


At last, we need a http server. Create a directory and link some directories from /home/repository.
Apache uses www-data user to read files from the filesystem. So keep in ming that this user must have access to some /home/repository directories.
.. code-block:: json


    #mkdir /var/www/ubuntu
    #sudo ln -s /home/repository/pool /var/www/ubuntu/pool
    #sudo ln -s /home/repository/dists /var/www/ubuntu/dists
    #sudo ln -s /home/repository/logs /var/www/ubuntu/logs
    #sudo ln -s /home/repository/maintainers.keys /var/www/ubuntu/maintainers.keys
    #sudo chown -Rf www-data:www-data /var/www/ubuntu
    

And now, add this section to your apache configuration
.. code-block:: json


        Alias /ubuntu/ "/var/www/ubuntu/"
        <Directory "/var/www/ubuntu/">
            Options Indexes MultiViews FollowSymLinks
            AllowOverride None
            Order allow,deny
            Allow from all
        </Directory>
    

And restart it
.. code-block:: json


    #/etc/init.d/apache2 restart{CODE}
    
    Add an uploader
    ================
    
    Import the key of the uploader
.. code-block:: json


    #su repository
    #gpg --import uploader_key_file.key

Retrieve the key id
.. code-block:: json


    #su repository
    #gpg --list-keys

And add it to conf/uploaders :
.. code-block:: json


    
    allow * by key keyid
    


Upload packages to the repository
==================================

Install dupload on the compiler computer. It will push new packages to the domogik repository.
.. code-block:: json


    sudo apt-get install dupload{CODE}
    Now edit /etc/dupload.conf or create a .dupload.conf in your home directory.
.. code-block:: json


    $default_host = "domogik";
    $cfg{'domogik'} = {
            fqdn => "192.168.14.66",
            incoming => "/incoming/oneiric/",
            dinstall_runs => 1,
    };


You can use the following command to upload a new package to the repository
.. code-block:: json


    #dupload package.changes{CODE}
    Links
    ======
    
    `http://blog.mycrot.ch/2011/04/26/creating-your-own-signed-apt-repository-and-debian-packages/ <http://blog.mycrot.ch/2011/04/26/creating-your-own-signed-apt-repository-and-debian-packages/>`_
    `http://mirrorer.alioth.debian.org/ <http://mirrorer.alioth.debian.org/>`_
    `http://www.debian-administration.org/articles/286 <http://www.debian-administration.org/articles/286>`_