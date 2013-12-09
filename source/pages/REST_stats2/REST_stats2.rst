.. toctree::


<br />
********************
Purpose<br />
********************

__/stats__ entry allows to get statistics stored in database (table device_stats).<br />
<br />
*************************************
Getting data with /stats<br />
*************************************

Parameters description<br />
===================================

* device id : a device id. Could be '*' to return all keys.<br />
* key : key name for data in table __device_stats__. Could be '*' to return all keys. <br />
* start time (optionnal)<br />
* end time (optionnal : none = now)<br />
<br />
/stats/<device id>/<key>/all<br />
=====================================================

Get all values. You may avoid to use this entry : there could be several thousands values in database!<br />
some exemples<br />
.. code-block:: json


    <br />
    /stat/*/*/all<br />
    /stat/5/*/all<br />
    /stat/5/command/all<br />
    
<br />
<br />
Result:<br />
.. code-block:: json


    <br />
    {<br />
        "status" : "OK",<br />
        "code" : 0,<br />
        "description" : "None",<br />
        "stats" : [<br />
            {<br />
                "timestamp" : 1286226868,<br />
                "value" : "HIGH",<br />
                "key" : "ping",<br />
                "date" : "2010-07-21 16:02:14",<br />
                "device_id" : 3<br />
            },<br />
            ...<br />
        ]<br />
    }<br />
    
<br />
<br />
/stats/<device id>/<key>/latest<br />
========================================================

Get latest value<br />
<br />
.. code-block:: json


    <br />
    /stat/*/*/latest<br />
    /stat/5/*/latest<br />
    /stat/5/command/latest<br />
    
<br />
<br />
<br />
Result : same than /all but with only one value<br />
<br />
/stats/<device id>/<key>/last/<number of item to get><br />
====================================================================================

Get the N last values<br />
<br />
.. code-block:: json


    <br />
    /stat/*/*/last/10<br />
    /stat/5/*/last/10<br />
    /stat/5/command/last/10<br />
    
<br />
<br />
<br />
Result : same than /all but with only N values<br />
<br />

/stats/<device id>/<key>/from/<start time> {/to/<end time>}<br />
================================================================================================

~~#C00:CSV export allowed~~<br />
<br />
Get values from <start time> to ...<br />
<start time> and <end time> need to be timestamps<br />
<br />
Result : same than /all but with values between start and end time<br />
<br />
Example<br />
********************

__/stats/4/temperature/from/1286226613/to/1286500000__<br />
<br />
.. code-block:: json


    <br />
    {<br />
        "status" : "OK",<br />
        "code" : 0,<br />
        "description" : "None",<br />
        "stats" : [<br />
            {<br />
                "device_stats" : [<br />
                    {<br />
                        "timestamp" : 1286226868,<br />
                        "value" : "22.6875",<br />
                        "key" : "temperature",<br />
                        "date" : "2010-10-04 23:14:28",<br />
                        "device_id" : 4<br />
                    },<br />
                    {<br />
                        "timestamp" : 1286226884,<br />
                        "value" : "22.6875",<br />
                        "key" : "temperature",<br />
                        "date" : "2010-10-04 23:14:44",<br />
                        "device_id" : 4<br />
                    },<br />
                    {<br />
                        "timestamp" : 1286226899,<br />
                        "value" : "22.6875",<br />
                        "key" : "temperature",<br />
                        "date" : "2010-10-04 23:14:59",<br />
                        "device_id" : 4<br />
                    },<br />
                    ...<br />
                ],<br />
                "key" : "temperature",<br />
                "device_id" : "4"<br />
            }<br />
        ]<br />
    }<br />
    
<br />
<br />
/stats/<device id>/<key>/from/<start time> {/to/<end time>}/interval/<year, month, week, day, hour, minute, second>/selector/<min(number only), max(number only), avg(number only), first, last, x><br />
====================================================================================================================================================================================================================================================

~~#C00:CSV export allowed~~<br />
<br />
Result : for performance issue, the return format is different from /all. Following data are returned :<br />
* key<br />
* device_id<br />
* values : a list of tuples<br />
Tuples format<br />
**************************

.. code-block:: json


    <br />
    # Minutes<br />
    # Format : (year, month, week, day, hour, min, value)<br />
    [(2010, 2, 7, 21, 15, 57, 56.5), (2010, 2, 7, 21, 15, 58, 62.5), (2010, 2, 7, 21, 15, 59, 68.5),<br />
    (2010, 2, 7, 21, 16, 0, 74.5), (2010, 2, 7, 21, 16, 1, 80.5), (2010, 2, 7, 21, 16, 2, 86.5)]<br />
    <br />
    # Hours<br />
    # Format : (year, month, week, day, hour, value)<br />
    [(2010, 6, 25, 22, 19, 38.5), (2010, 6, 25, 22, 20, 40.0), (2010, 6, 25, 22, 21, 41.5),<br />
     (2010, 6, 25, 22, 22, 43.0), (2010, 6, 25, 22, 23, 44.0), (2010, 6, 25, 23, 0, 45.5),<br />
     (2010, 6, 25, 23, 1, 47.0), (2010, 6, 25, 23, 2, 48.0)]<br />
    <br />
    # Days<br />
    # Format : (year, month, week, day, value)<br />
    [(2010, 6, 25, 22, 4.0), (2010, 6, 25, 23, 6.0), (2010, 6, 25, 24, 9.0), (2010, 6, 25, 25, 12.0),<br />
     (2010, 6, 25, 26, 15.0), (2010, 6, 25, 27, 18.0), (2010, 6, 26, 28, 21.0)]<br />
    <br />
    # Weeks<br />
    # Format : (year, month, week, value)<br />
    [(2010, 7, 29, 25.0), (2010, 7, 30, 35.5), (2010, 8, 31, 49.5), (2010, 8, 32, 63.5),<br />
     (2010, 8, 33, 77.5), (2010, 8, 34, 88.0)]<br />
    
<br />
<br />
Example <br />
*********************

<br />
__/stats/4/temperature/from/1286226613/to/1286500000/interval/hour/selector/avg  __<br />
<br />
.. code-block:: json


    <br />
    {<br />
        "status" : "OK",<br />
        "code" : 0,<br />
        "description" : "None",<br />
        "stats" : [<br />
            {<br />
                "values" : [<br />
                    [<br />
                        2010,<br />
                        10,<br />
                        40,<br />
                        4,<br />
                        23,<br />
                        22.753251445086704<br />
                    ],<br />
                    [<br />
                        2010,<br />
                        10,<br />
                        40,<br />
                        5,<br />
                        0,<br />
                        22.559444444444445<br />
                    ],<br />
                    [<br />
                        2010,<br />
                        10,<br />
                        40,<br />
                        5,<br />
                        1,<br />
                        22.12887168141593<br />
                    ],<br />
                    ...<br />
                ],<br />
                "key" : "temperature",<br />
                "device_id" : "4"<br />
            }<br />
        ]<br />
    }<br />
    
<br />
<br />
/stats/multi/<id1>/<key1>/<id2>/<key2><br />
===========================================================================

Get last values for multiple id/keys in one request<br />
<br />
Example json response : <br />
.. code-block:: json


    <br />
    {<br />
        "status" : "OK",<br />
        "code" : 0,<br />
        "description" : "None",<br />
        "stats" : [<br />
            {<br />
                "timestamp" : 1286226868,<br />
                "value" : "HIGH",<br />
                "key" : "ping",<br />
                "date" : "2010-07-21 16:02:14",<br />
                "device_id" : 3<br />
            },        {<br />
                "timestamp" : 1286566868,<br />
                "value" : "LOG",<br />
                "key" : "command",<br />
                "date" : "2010-07-22 16:02:14",<br />
                "device_id" : 5<br />
            },<br />
            ...<br />
        ]<br />
    }
