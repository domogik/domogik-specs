Devices
========

.. code-block:: json


    /base/device/list 
    /base/device/add/name/<name>/description/<description>/reference/<reference>/usage_id/<usage id>/technology_id/<technology id>/type/<type>
    /base/device/update/<id>/name/<name>/description/<description>/reference/<reference>/usage_id/<usage id>
    /base/device/del/<id>

{REMARKSBOX(type=>note)}
device technology and device type can not be updated after creation
{REMARKSBOX}

Device parameters
==================

~~#C00:__To update with database model__~~

Features
=========

.. code-block:: json


    /base/feature/list/by-id/<id>
    /base/feature/list/by-device_id/<id> 
    /base/feature/add/device_id/<device_id>/name/<name>/command_type/<DMG type>/command_address/<command address>/command_reference/<command reference>/state_type/<DMG type>/state_address/<state address>/state_reference/<state reference>
    /base/feature/update/<id>/name/<name>/command_type/<DMG type>/command_address/<command address>/command_reference/<command reference>/state_type/<DMG type>/state_address/<state address>/state_reference/<state reference>
    /base/feature/del/by-id/<id>
    /base/feature/del/by-device_id/<id> 
    

{REMARKSBOX(type=>note)}
device_id can not be updated
{REMARKSBOX}

Feature parameters
===================

~~#C00:__To update with database model__~~
.. code-block:: json


    /base/feature_config/set/feature_id/<feature id>/key/<key>/value/<value>
    /base/feature_config/del/by-feature_id/<feature id>
    /base/feature_config/del/by-key/<feature id>/<key>
    


Device templates
=================

.. code-block:: json


    /base/device_template/list/by-id/<device type>{CODE}
    {REMARKSBOX(type=>note
    
    There is no need for writing REST urls as they are updated using the xml process
    {REMARKSBOX}
    
    Feature templates
    ==================
    
.. code-block:: json


    /base/feature_template/list/by-device_id/<device type>{CODE}
{REMARKSBOX(type=>note)}
There is no need for writing REST urls as they are updated using the xml process
{REMARKSBOX}

Features states
================

.. code-block:: json


    /states/<feature id>/all
    /states/<feature id>/latest
    /states/<feature id>/last/<number of item to get>
    /states/<feature id>/from/<start time> {/to/<end time>}
    /states/<feature id>/from/<start time> {/to/<end time>}/interval/<year, month, week, day, hour, minute, second>/selector/<min(number only), max(number only), avg(number only), first, last, x>


Plugin config
==============

~~#C00:__To update with database model__~~
.. code-block:: json


    
    /plugin/config/set/name/<plugin name>/hostname/<hostname>/key/<key>/value/<value> {/interface/<interface number : 0..n>}
    


Pages
======

.. code-block:: json


    /base/page/list
    /base/page/add/name/<name>/description/<description>/parent/<parent id>
    /base/page/update/<id>/name/<name>/description/<description>/parent/<parent id>
    /base/page/del/<id>
    /base/page/view/<id>
    /base/page/tree/<id>
    /base/page/path/<id>
    
