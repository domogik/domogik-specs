******************************
Web UI : creating new devices
******************************

.. toctree::



Ideas
======

* For actuators, add a field for the device for the max power consumed by the appliance plugged on the actuator

Administration view
====================

When creating a new device, the user will have 2 choices:

* Unique address, for physical device of software service where the features can be reached by a unique address. (X10, plcBus, ...)
* Multi addresses, for physical or virtual devices where the features are identified by their own individual addresses. (KNX, ...) 

The user will have to choose a techno, or a specific device type for pre-populated feature list.

It will be possible to add, remove or disable any feature.
And Configure the Domogik Type for each feature.

As actually the features will be separated in 2 categories:
* Actuator: with reference for command and reference for state
* Sensor: only with state reference 

Unique address device
**********************

* Will ask for a global address
* For each feature it will require, the command name (for command) or key name (for state) as references 
Multi address device
=====================

* For each feature it will require, the addresses (for command and for state) as references 

Points to see :
* auto discovery (modify below pic)
* make pictures examples for techno/type
* make pictures examples for address

.. image:: ../../_static/images/269

Auto discovery process
=======================

Plugin side
************

At startup, the plugin create one or more listeners for :
* type = xpl-cmnd
* schema = domogik.helpers
* command = autodiscovery
* techno = <plugin technology>
If a plugin/technology can make the difference between features : the lsitener is also on :
* feature/type = <feature/type (same than UI value)
 
A listener makes reference to a callback function that will :
* refresh devices list
* send a list as xpl-trig domogik.helpers. "plugin = <plugin name>" is added in xpl message

xPL
****

Request : 
.. code-block:: json


    
    xpl-cmnd
    {
    ...
    }
    domogik.helper
    {
    command = autodiscovery
    technology = <technology asking for discovery>
    [ type = <filter on type : switch, light, temperature, etc> ]
    }
    


Answer : 
.. code-block:: json


    
    xpl-trig
    {
    ...
    }
    domogik.helper
    {
    command = autodiscovery
    technology = <technology asking for discovery>
    [ type = <filter on type : switch, light, temperature, etc> ]
    plugin = <plugin providing device>
    host = <host on which is plugin>
    dev0-address = <address>
    dev0-reference = <reference>
    dev1-address = ...
    dev1-reference = ...
    ...
    }
    


UI/REST side
*************

When clicking in the address field, a box appears. On box opening, REST is called : 
* /autodiscovery/technology/<techno> [ /type/<type> ]
This makes REST send a ''xpl-cmnd domogik.helpers'' "command=autodiscovery" message. Then REST waits for several replies.