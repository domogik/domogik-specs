**************
Plugin mirror
**************


This plugin documentation is now available on [http://docs.domogik.org/plugin/mirror/dev/en/]

**************************************
Plugin mirror - developer information
**************************************

.. toctree::


xPL Schema 
============

The `sensor.basic <http://xplproject.org.uk/wiki/index.php?title=Schema\_-\_SENSOR.BASIC>`_ schema is used by this plugin.

Here are the events for which a xPL message is sent :

Mir:ror faced up
*****************

.. code-block:: json


    
    xpl-trig
    {
    ...
    }
    sensor.basic
    {
    device=mirror
    type=activated
    current=HIGH
    }
    


Mir:ror faced down
*******************

.. code-block:: json


    
    xpl-trig
    {
    ...
    }
    sensor.basic
    {
    device=mirror
    type=activated
    current=LOW
    }
    


A RFID element is detected
***************************

.. code-block:: json


    
    xpl-trig
    {
    ...
    }
    sensor.basic
    {
    device=
    type=present
    current=HIGH
    }
    


A RFID element is no more detected
***********************************

.. code-block:: json


    
    xpl-trig
    {
    ...
    }
    sensor.basic
    {
    device=
    type=present
    current=LOW
    }
    
