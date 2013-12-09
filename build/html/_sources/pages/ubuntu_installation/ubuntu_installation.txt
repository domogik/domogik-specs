*************************************************
Installing Domogik on Ubuntu (Oneiric, Precise)
*************************************************


Full installation
===================

First of all, you must have mysql running on a host of your network. You also need the admin user and password.
Your mysql server must be running before starting installation of domogik, otherwise the installation will not finish properly.
If you don't have one, install mysql-server on your computer and verify it is running.
.. code-block:: json

    service mysql status

If not, start it

.. code-block:: json

    sudo service mysql start

Add the following sources to your apt configuration.
For Oneiric (i386,amd64 and armel) :

.. code-block:: json

    deb http://bibi21000.gallet.info/ubuntu oneiric universe

For Precise (i386 and amd64, armel will come soon) :

.. code-block:: json

    deb http://bibi21000.gallet.info/ubuntu precise universe

Get the gpg keys to authenticate packages.

.. code-block:: json

    wget -O - http://bibi21000.gallet.info/ubuntu/maintainers.keys | sudo apt-key add -

Open synaptic and reload indexes.

Look for domogik in the search engine and select domogik-full.

Apply updates

{IMG(fileId="322"
{IMG}
The interface to use with xplhub.
If your computer is connected to a wired network, you should use eth0.
With wifi, you should try wlan0. Otherwise use lo


{IMG(fileId="323"
{IMG}
Domogik need to create a database to finish its installation.
If you have a dedicated mysql server on your network, use it. If not, use localhost to connect to the previously installed mysql-server.
You also need the password of the admin user. It will be used to create the database.


{IMG(fileId="324"
{IMG}
Domogik use a special user to connect to the database. It's also possible to change the name of the database used by domogik.


{IMG(fileId="325"
{IMG}
The interface Domogik should bind to. It MUST be the same as xplhub.


Wait a litlle and that's all.

Open Firefox and connect the ip address associated with the interface previously defined on port 40404.
If you use lo, connect to `http://127.0.0.1:40404/|nocache <http://127.0.0.1:40404/>`_
If you choose etho or wlan0, yous should try something like http://192.168.X.Y:40404/

Remove domogik
================

    You can completely remove domogik using the purge command. It will erase all your configuration files and the database too. That's said.
    If you had a problem to your first installation, it's a good idea to purge domogik, and restart a clean one.
    In a terminal, the following command will purge domogik and all data :

.. code-block:: json

    #sudo apt-get purge xplhub domoweb domogik-full domogik-primary domogik-secondary domogik-mysql domogik-postgresql domogik-common

Packages available
====================

Classical installation
***********************

If you want to install domogik and domoweb on the same computer, you need to install this package :

.. code-block:: json

    #sudo apt-get install domogik-full

Primary server
***************

If you want to install a primary server, install this package :

.. code-block:: json

    #sudo apt-get install domogik-primary

Secondary server
*****************

If you want to install a secondary server, install this package :

.. code-block:: json

    #sudo apt-get install domogik-secondary

The configuration is sligthly different. You only need to set the ip address and the port of the main rest server of your network.
PS : Not tested. If you want to use it, contact-me on IRC, Forum or Developpers Mailing List (preferred)

Using postgresql
*****************

Domogik should work with postgresql
If you want to ude postgresql instead of mysql, add the package "domogik-postgresql":
For example, to install a primary server with postgresql

.. code-block:: json

    #sudo apt-get install domogik-primary domogik-postgresqlPS : Not tested. If you want to use it, contact-me on IRC, Forum or Developpers Mailing List (preferred)

Installing Domoweb
*******************

Warning : there is a missing dependence in domoweb.
The WebUi could be install on every computer on the network.

.. code-block:: json

    #apt-get install domoweb

Using apache with domoweb
**************************

.. code-block:: json

    #sudo apt-get install domoweb-apache2PS : Not tested. If you want to use it, contact-me on IRC, Forum or Developpers Mailing List (preferred)

Developpers
============

Installing a package repository for ubuntu : http://wiki.domogik.org/ubuntu\_repository
