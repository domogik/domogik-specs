**********************************************
Use Case 1 - Address split in 2 sub addresses
**********************************************

Example 
=========

In rfxcom plugin, there is an __ac.basic__ schema : 
.. code-block::


    
    ac.basic
    {
    address=<0x1..0x3ffffffff>
    unit=<1..16>
    command=...
    ...
    }
    

To address the device, you must specify address AND unit. So /command must be able to use 2 addresses (address and unit) to create the xPL
What has been done
===================

solved in 0.x.x-deviceparams
the address is removed from a device config, now this can be configured by multiple values


**************************************
Use Case 2 - Multi technology plugins
**************************************

Example
========

Rfxcom handle several technologies : homeeasy, x10, ...
Several technologies can need the same order (on, off, ...).

What has been done
===================

solved in 0.x.x-deviceparams
a plugin doens't define a technology anymore, it only defines device_types

*******************************************************************
Use case 3 - Give access to list and ressources of usages by RINOR
*******************************************************************

Example 
=========

All UIs may use new usages by getting then from RINOR (/usage/list, /usage/...) and also get the different icons with RINOR

What has to be done
====================


************************************************
Use case 4 - Group of features/ Virtual devices
************************************************


*******************************************************
Use case 5 - Can send extra attributes, with a command
*******************************************************

Example
========

For relay box (ipx800) the box has a unique address, so the command needs to send the action, AND the relay id
For KNX the KNX datatype is required for conversion before sending to the bus

What has been done
===================

solved in 0.x.x-deviceparams
the address is removed from a device config, now this can be configured by multiple values

*******************************
Use case 6 - Calculated values
*******************************

How to have calculated values based on features values, constants, formulas
See forum topic for full details:
http://forum.domogik.org/viewtopic.php?f=3&amp;t=88&amp;p=669#p669

*****************************
Use case 7 - Specific Target
*****************************

Some xpl equipment, like an arduino, could have multiple instance on the network.  The XPL protocol allows to target a specific instance of a device like:
.. code-block::


    target=arduino-rgb.parentsbedroom
    target=arduino-rgb.kitchen

But for the moment, Domogik permits only  broadcast target.

**************************************
Use case 8 - Multiples states command
**************************************

For group command (like OFF ALL), multiple responses can be received, with no direct link to the original command.
Need to find a way to catch them all, and display a summary on UI.

What has been done
===================

solved in 0.x.x-deviceparams
a device_type can have multiple sensors to catch all those states, or it can even have multiple xpl_stats linked to one sensor

************************************
Use case 9 - The Up, Down and Stop 
************************************

Shutters are managed using the 3 commands : up, down and stop. Need to have 3 commands in a feature to do it.

What has been done
===================

solved in 0.x.x-deviceparams
a device_type can have multiple commands