*****************
python-openzwave
*****************

.. toctree::



Purpose
========

this not a plugin, but an external library for zwave plugin, is based on `python-openzwave|nocache <https://code.google.com/p/python-openzwave/>`_ software.

python-openzawe and `openzawe|nocache <http://code.google.com/p/open-zwave/>`_ are in hight development, by two different teams, so installing it can be sometimes not so easy. So we propose you different methods to install it
History
********

The original script `py-openzwave|nocache <https://github.com/maartendamen/py-openzwave>`_ was from maarten damen ~~#F03:and is no longer compatible with ozwave plugin~~

 Prerequisite
==============

if not installed, install the following packages:
* g++
* libudev-dev
* python-dev
* python-setuptools
* cython(at least 0.14.1)
* python-louie
* python-sphinx to make the documentation

You must install mercurial and subversion to get sources of python-openzwave and openzwave. Look at the documentation of your Linux distribution to do them.

Install python-openzwave, the official way
===========================================

* Get the sources, clone the hg repo:
 .. code-block:: json


    $hg clone https://code.google.com/p/python-openzwave/{CODE}
    
    Automatic installation
    ***********************
    
    * You can build python-openzwave with the install.sh script.
    Enter the python-openzwave directory
    
 .. code-block:: json


    $cd python-openzwave{CODE}
then use the provided scipt to compile
 .. code-block:: json


    $./update.sh{CODE}
 .. code-block:: json


    $./compile.sh{CODE}
* If the build process succeed, run the following command to install
 .. code-block:: json


    $sudo python setup.py install{CODE}
    That's all (:cool:)
    
     Manual installation
    *********************
    
    * Retrieve the sources of openzwave :
 .. code-block:: json


    $svn checkout http://open-zwave.googlecode.com/svn/trunk/ openzwave{CODE}
* Build openzwave
 .. code-block:: json


    $cd openzwave/cpp/build/linux
    $make
    $cd ../../../..

*Build python-openzwave
 .. code-block:: json


    $python setup.py build{CODE}
    *And install it if compilation succeed
 .. code-block:: json


    $sudo python setup.py install{CODE}
Installation on debian/ubuntu
******************************

You need to compile and install openzwave as a package to generate python-openzwave.
*After that, make the python-openzwave package
.. code-block:: json


    $dpkg-buildpackage -rfakeroot{CODE}
    You can now install the package with
.. code-block:: json


    $sudo dpkg -i python-openzwave*.deb{CODE}
API documentation is in /usr/share/doc/python-openzwave

 Static vs dynamic (or shared)
*******************************


The openzwave (c++) lib needs to run as a singleton : it means that it
MUST have only one instance of the manager running on your computer.

There is 2 ways of linking libraries with a program :
*static : includes a copy of the library in your binary program. This means
that your program has its own instance of the library. This the way the
install.sh runs. So you CAN'T have another program (like the control-panel)
running when using the python-openzwave library

*dynamic or shared : includes a link to the library in your binary program.
This means that your program share the library with other programs. In this
case, the instance is owned directly by the library. This the way the
debian package works. So you CAN have another program running when
using the python-openzwave library. Of course, this program MUST use
the shared library.


Generate some documentation
============================

using the command :
 .. code-block:: json


    $./make_doc.shcompil openzwave{CODE}
    
    There is a copy of the openzwave's directory in /usr/local/share/python-openzwave
    API documentation is in /usr/local/share/doc/python-openzwave
    
    How to check python-openzwave
    ==============================
    
.. code-block:: json


    ./examples/api_demo.py
    


 Creating the zwave device controller
======================================

We need to create an udev rule in order to create the device /dev/zwave
 check your device
*******************

I suppose your zwave controller is at /dev/ttyUSB0

.. code-block:: json


    $ udevadm info --name=/dev/ttyUSB0 --attribute-walk{CODE}
    locate your  idVendor and idProdroduct
    in /etc/udev/rules.d, create a file zwave.rules, and write the following rule
    
    ie, for aeon stick
    
.. code-block:: json


    SUBSYSTEMS=="usb", ATTRS{idVendor}=="10c4", ATTRS{idProduct}=="ea60", SYMLINK+="zwave", MODE="0666"{CODE}


 Install openzwave control-panel
=================================

In order to identify your network and collect the NodeID of your devices, we recommend to use the openzwave-control-panel

.. code-block:: json


    $ln -s open-zwave-read-only open-zwave {CODE}
    
    Compile libmicrohttpd, needed by openzwave-control-panel. Don’t use the libmicrohttpd provided by your distribution. The compilation of the openzwave-control-panel will fail otherwise!
    Respect carefully the folder location; ie openzwave, libmicrohttpd, and openzwave-control-panel must have the same parent directory.
    
.. code-block:: json


    $wget ftp://ftp.gnu.org/gnu/libmicrohttpd/libmicrohttpd-0.9.19.tar.gz
    $tar zxvf libmicrohttpd-0.9.19.tar.gz
    $mv libmicrohttpd-0.9.19 libmicrohttpd
    $cd libmicrohttpd
    $./configure
    $make
    $sudo make install
    $cd ~


Compile openzwave-control-panel

.. code-block:: json


    $svn checkout http://openzwave-control-panel.googlecode.com/svn/trunk/ openzwave-control-panel
    $cd openzwave-control-panel

.. code-block:: json


    $nano Makefile{CODE}
    
    Change the following lines to:
    for Linux uncomment out next two lines
.. code-block:: json


    LIBZWAVE := $(wildcard $(OPENZWAVE)/cpp/lib/linux/*.a)
    LIBUSB := -ludev


Compile:

.. code-block:: json


    $make{CODE}
    
    ozwcp require acces to the config dir of ozw
    
.. code-block:: json


    $ln -s ../open-zwave/config config
    $ chmod -R 777 config 


To start the openzwave-control-panel, type;
.. code-block:: json


    $./ozwcp -d -p 1234{CODE}
    
    Point your browser to http://openzwave-machinename:1234/
    
    source: http://www.strengholt-online.nl/howto-compile-open-zwave-and-openzwave-control-panel-on-ubuntu/
    
     Developer resources
    =====================
    
    
    For developing you can access to python-openzwave dev, instructions here :
    
    http://bibi21000.gallet.info/index.php/en/home-automation-uk/124-openzwave-vs-python-reloaded.html