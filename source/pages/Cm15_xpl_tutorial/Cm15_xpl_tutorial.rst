*********************************
Use a CM15a/CM15pro with domogik
*********************************

What you need
==============

*The driver for the cm15 under linux, which can be found `here <http://www.linuxha.com/common/iplcd/iplc-driver.tgz>`_
*xPL-Perl installed on the system, see `here <http://www.xpl-perl.org.uk/wiki/DownloadPage>`_ if you don't have it.
*The xpl CM15 module, which can be found `here <http://www.poulpy.com/wp-content/plugins/download-monitor/download.php?id=3>`_

Important : you don't need neither heyu, nor the x10_heyu plugin to have this to work.

How to install the hardware driver part
========================================

First of all, compile and install the cm15a driver, in short it is :
.. code-block:: json

caption=""
    tar xzf iplc-driver.tgz
    cd iplc/driver/linux-2.6
    #tip found on poulpy.com, if you have a recent linux kernel -> sed -i s/\\Winfo\\W*\(/\ pr_info\(/ *.c
    cd cm15a.d
    make
    insmod ./cm15a.ko

Then you should be able to see the driver installed (check with dmesg and lsmod).

Next thing is to install the xpl-cm15a utility from www.poulpy.com
again tar, make, make install (see the `reference article <http://www.poulpy.com/2010/02/cm15a-et-cm15pro-sous-linux-et-xpl/comment-page-1/#comment-4136>`_ for more information)

So, now, you should be able to launch the xpl listener that will translate your xpl commands to x10 with this command :
.. code-block:: json

caption=""
    xpl-cm15a --cm15a-verbose --cm15a-device /dev/cm15a0 --interface eth0{CODE}
    
    You can verify it with the xpl-sender command :
.. code-block:: json

caption=""
    /usr/bin/xpl-sender -m xpl-cmnd -c x10.basic device=a1 command=on{CODE}
Go on with domogik
===================

If you are using a __version < 0.6__, there's a missing feature in the xpl-cm15a command to have it work with domogik, you must apply this patch to the sources :
.. code-block:: json

caption=""
    --- xpl-cm15a-0.5/lib/xPL/Dock/CM15A.pm 2010-04-22 10:54:09.000000000 +0200
    +++ ../xpl-cm15a-0.5/lib/xPL/Dock/CM15A.pm      2011-02-20 23:28:20.293341332 +0100
    @@ -409,6 +409,8 @@
           $self->{_io}->write($msg2);
         }
         print("X10 to PLC - ".$p{'house'}.$p{'unit'}." ".$p{'command'}."\n") if ($self->{_verbose});
    +    send_xpl_message($self,$p{'house'},$p{'unit'},$p{'command'});
    +
       }
     }
    

Now, everything should be ok and all you have to do is :
*configure your x10 devices
*add them to your rooms (with widgets)
*Enjoy !

Sources
========

`xpl -> CM15 driver <http://www.poulpy.com/2010/02/cm15a-et-cm15pro-sous-linux-et-xpl>`_
