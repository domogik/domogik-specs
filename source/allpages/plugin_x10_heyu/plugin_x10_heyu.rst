***********
X10 plugin
***********


This plugin documentation is now available on [http://docs.domogik.org/plugin/x10\_heyu/dev/en/]


Developper Notes
=================


xPL schema
***********

The `x10.basic <http://xplproject.org.uk/wiki/index.php?title=Schema\_-\_X10.BASIC>`_ schema is used.

/command
*********

.. code-block:: json


    
    /command/x10/<address>/on # switch on the lamp / appliance
    /command/x10/<address>/off # switch off the lamp / appliance
    

''Only for lamps'' 
.. code-block:: json


    
    /command/x10/<address>/dim/<value> # dim units by <level> (1-22) (decrease brightness)
    /command/x10/<address>/bright/<value> # brighten units by <level> (1-22) (increase brightness)
    

Note that these values are relative.