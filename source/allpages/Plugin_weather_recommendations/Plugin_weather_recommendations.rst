*******************************
Weather plugin recommendations
*******************************

.. toctree::


Rules for all weather plugins
==============================

All weather plugins (online services or local station/sensors) should respect the following rules :

Getting current data and previsionnal data must be separated features and could be disabled
********************************************************************************************

The idea is to allow the possibility for a user with a local weather station (or local sensors) to use with a plugin his local station (instead of online service data) and to use previsionnal data from an online service.

For each location, plugins should have 2 options to set the location
*********************************************************************

* the first is related to the hardware or online service (ex : The city code is in Yahoo Weather API is different from the Google one)
* the second is related to the device address : this is the one the user chooses (ex : "my_home") and allow to use data from different plugins in the same widget

Current data use sensor.basic schema
*************************************

For current data, ''__sensor.basic__'' xPL schema should be used :

.. code-block:: json


    
    xpl-stat
    {
    ...
    }
    sensor.basic
    {
    device = ...
    type = ...
    current = ...
    [ units = ... ]
    }
    


!!!!Device
''Device'' will be the address of the device the user set in the plugin configuration.

!!!!Type
Here are the possible values for the type :
||__Data__                      |__Type in sensor.basic__   |__Key name in database__ (cf stats xml file)
temperature                     |temp                       |temperature                   
atmosphere pressure (barometer) |pressure                   |pressure
atmosphere humidity             |humidity                   |humidity
atmosphere visibility           |visibility *               |visibility 
atmosphere rising               |rising *                   |rising 
wind chill                      |chill *                    |chill  
wind direction                  |direction                  |direction
wind speed                      |speed                      |speed
uv index                        |uv                         |uv
rainfall                        |rainfall *                 |rainfall 
drew point                      |drewpoint *                |drewpoint 
condition code                  |condition-code *           |condition-code 
condition text                  |condition-text *           |condition-text       ||

''*'' these type are not indicated on the official xPL website for ''sensor.basic''.

!!!!Current
Current value for device / type

!!!!Units (optionnal)
If available, unit of the data

Previsionnal data use weather.basic schema
*******************************************

For previsionnal data, ''__weather.basic__'' xPL schema should be used.

.. code-block:: json


    
    xpl-stat
    {
    ...
    }
    weather.basic
    {
    device = <address of the device set in the plugin config page>
    day = <YYYYMMDD>
    day-part* = <morning, afternoon, evening, night>
    city = <city ; ex : Paris>
    country* = <country ; ex : France>
    region* = <region if available (US)>
    unit-temperature = <c (celcius), f (farenheit)>
    unit-distance = <km, miles>
    unit-pressure = <mb, ...>
    unit-speed = <km/h, ...>
    wind-chill* = <number>
    wind-direction* = <number>
    wind-speed* = <number>
    atmosphere-humidity* = <number>
    atmosphere-visibility* = <number>
    atmosphere-pressure* = <number>
    atmosphere-rising* = <number>
    picture-url* = <url of current condition picture>
    condition-code = <number>
    condition-text = <ex : "Party cloud", etc>
    temperature* = <number>
    temperature-high* = <number>
    temperature-low* = <number>
    uv* = <number>
    barometer*= <number>
    rainfall* = <number>
    drew-point* = <number>
    }
    

''*'' are optionnal keys

Depending on the weather service used, some data will be used or not. It is possible that some data is missing in this schema. Please, fell free to tell us or to complete this schema.