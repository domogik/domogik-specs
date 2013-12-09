.. toctree::



****************
Plugin cidmodem
****************

This plugin documentation is now available on [http://docs.domogik.org/plugin/cidmodem/dev/en/]



*****************
Developper notes
*****************
xPL Schema 
============
The `CID.BASIC <http://xplproject.org.uk/wiki/index.php?title=Schema\_-\_CID.BASIC>`_ schema is used by this plugin.

Here is xPL schema send when an inbound calls occurs : 
.. code-block::
    
    xpl-trig
    {
    ...
    }
    cid.basic
    {
    calltype=INBOUND
    phone=0102030405
    }
    


 How it works 
===============
The xPL client listens to the modem. When it detects an incoming call, it sends a XPL-TRIG over the network.

Example of what the modem sees for an incoming call : 
.. code-block::
    
    RING
    
    NMBR = 0688xxxxxx
    
    DATE = 1021
    
    TIME = 2149
    
    RING
    

When a line containing NMBR is detected, the client gets the number and sends it over the network. We don't get date and time because this information will be added by the stats manager.

