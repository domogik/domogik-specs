Sometimes (yes, it can happen), your Domogik installation does not work as expected.

Here are a few tips to check what's wrong, and maybe find the problem by yourself, or at least let you come with all the data we will need to debug your installation.

********************
During installation
********************

Permission
===========


* Problem
.. code-block:: json

colors='bash'
    
    user@domogik:~/domogik$ sudo ./install.sh
        sudo: ./install.sh: command not found
    


* Solution
.. code-block:: json

colors='bash'
    
    user@domogik:~/domogik$ chmod +x install.sh
    


Config test
============

* Problem
test_config.py (started at the end of install.sh or by hand) find errors.

* Solution
Most of the errors are explained by the script itself. Maybe a few things can be precised :

xPL_Hub not found
******************

.. code-block:: json


    
     ==> xPL_Hub can't be found, please double check CUSTOM_PATH is correctly defined if you are in development mode. In install mode, check your architecture is supported or check src/domogik/xpl/tools/COMPILE.txt, then restart test_config.py  
    


It can happen if you are using some version of arm which are not correctly detected. Try to take xPL_Hub from src/domogik/xpl/tools/arm/.

****************
Domogik Startup
****************


Django
=======

* Problem 
You don't have any website when you try to connect to http://the.ip.you.set:40404/domogik 

* Diagnostic
# Is your Django running ? 
.. code-block:: json

colors='bash'
    
    user@domogik:~/domogik$ ps aux|grep django
    


* If nothing is running:
** looks at /tmp/django.log
** try to run it by hand : 
.. code-block:: json

colors='bash'
    
    /usr/bin/python /usr/local/bin/dmg_django runserver 127.0.0.1:40404
    


* If something is running :
** Are you looking at the good url ? 
** Any firewall ? 
** Anything in /tmp/django.log ?

Rest
=====

* Problem
When you connect on the web interface (http://the.ip.you.set:40404/domogik) you get a :
.. code-block:: json

ishtml="1"
    
    <b>Interface Server not responding</b>
    
    Check if the server is running
    


* Diagnostic :
** Is rest running ? 
.. code-block:: json

colors='bash'
    
    user@domogik:~/domogik$ ps aux|grep rest
    


** Yes
*** Look at /var/log/domogik/rest.log

**** Problem:

You find something like :
.. code-block:: json

colors='python'
    
      [Errno 13] Permission denied: '/home/domogik/.python-eggs/somepackage.egg'
    
    The Python egg cache directory is currently set to:
    
      /home/domogik/.python-eggs
    


**** 