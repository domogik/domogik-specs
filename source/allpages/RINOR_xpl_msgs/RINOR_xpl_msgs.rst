*********************************************
Create a new request to get all xpl messages
*********************************************

/xpl_msgs/request/new
======================

Return :
.. code-block::


    
    {
        "status" : "OK",
        "code" : 0,
        "description" : "None",
        "ticket_id" : 1,
        "xpl_message" : [
            {
                "datetime" : "2011-05-23 20:23:33.486954",
                "type" : "xpl-stat",
                "source" : "xpl-onewire.shyrkadmg",
                "destination" : "*",
                "schema" : "sensor.basic",
                "data" : [
                       "device" : "03EDB7010000",
                       "current" : "22.5",
                       "type" : "temp",
                ]
            },
    		...
        ]
    }
    


**************************************************
Create a new request to get filtered xpl messages
**************************************************

Each filter can be used independently with each other.
/xpl_msgs/request/new/type/<stat|trig|cmnd>/source/<source address>/destination/<destination address>/schema/<schema name>
===================================================================================================================================================

Return :
.. code-block::


    
    Same as above, but only with messages that matches the filters.
    


*****************************************
Get next results for an existing request
*****************************************

/xpl_msgs/request/get/<ticket id>
========================================


*************************************
Explicitly close an existing request
*************************************

/xpl_msgs/request/free/<ticket id>
=========================================

