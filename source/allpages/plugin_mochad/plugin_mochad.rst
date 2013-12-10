********
Purpose
********

Use this plugin to manage X10 devices through mochad with a cm15 or cm19

*************
Installation
*************

Please install mochad 
on your device by following the installation instructions on `the mochad wiki page <http://sourceforge.net/apps/mediawiki/mochad/index.php?title=Main\_Page>`_

Then enable the plugin :
.. code-block:: json


    dmgenplug mochad{CODE}
    
    **************
    Configuration
    **************
    
    In the administration panel, you can configure the following options :
    mochad-host : should be 127.0.0.1 (the same host runs mochad and domogik)
    mochad-port : 1099 is default
    cm15 : have it checked if you use a cm15 device
    cm19 : have it checked if you use a cm19 device, (:exclaim:)__be sure cm15 is unchecked__(:exclaim:)
    
    
    *************
    Add a device
    *************
    
    In the administration panel, go to the Organization > Devices page. Create a new device like this :
    Name : Short name
    Description : Describe your device!
    Address : Module address, like "A1"
    Reference : only for information string
    Type : x10.switch
    Usage : Appliance
