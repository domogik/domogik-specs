**************************
 List of available mocks 
**************************


||__Mock name__|__Description__
x10evt|Send an event for a X10 cpl network||

*************************
 How to launch a mock ? 
*************************

''Note : __-f__ parameters must be given. Else, mock will be launch in background''

Generic example :
.. code-block:: json


    
    cd xpl/mock/
    ./mymock.py -f --param1=foo --param2=fuu
    


Example for X10 event : device A3 passed to status ON :
.. code-block:: json


    
    cd xpl/mock/
    ./x10evt -f --command=STATUS_ON --device=A3
    


***************
 Mocks Detail 
***************

 x10evt 
=========

 Purpose 
**********

This mock is made to send an event instead of sending a real order to an X10 device.
 Parameters 
*************

* --command!<command>: X10 command (cf http://xplproject.org.uk/wiki/index.php?title!Schema_-_X10.BASIC for available X10 commands)
* --device!<device> : device reference : A1...A16...P16
* --house!<house> : house reference : A...P
* --level!<level> : level value : 0...100