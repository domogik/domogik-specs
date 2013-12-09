**************************************
xPL to Domogik data types transcoding
**************************************

The current model stores the values directly from the xPL to the database.
The interpretation (On/Off, Up/Down) is deducted from the usage associated to the device.

Current model problems:

* Without minimal control, the values format in the database can be anything. And the UI needs to know and handle all possible formats.
* The usage (so the interpretation) is associated to a device, but some devices have multiples outputs, and each output can be dedicated to a specific usage.
* When adding an usage, each widget should be modified to take the new usage in account (new interpretations).

New Model
==========
The new model will consist of 3 main modifications:

* Extending feature types to Domogik data types
* Create transcoding functions to convert techno values to unified values based on Domogik data types
* Update the RINOR to process the transcoding

Domogik data types
*******************
The Domogik data types are going to be based on a simplified version of the KNX Data Point Types.
(list to do)
!!!!Values transcoding functions
As in KNX value will require some more complex processing, the conversion table is not enough.
We will need 2 Python functions per techno+type :

* A function from the techno value to the unified value (typically when an event is received)
* A function from the unified value to the techno value (typically when a command is sent from the UI) 

The functions will be stored to the XML file:

.. code-block::
    <transcode from='techno' type='DT_Switch'>
    def transcode(value):
        ...
        return trancoded_value
    </transcode>


~~#F00:Fritz : I don't agree with that. Storing functions in xml is a bad idea : it would be best to have python functions that deduce what to do from xml file~~

RINOR transcoding process
**************************
The transcoding process will require 4 steps:

# Use the XML to identify keys and values
# Retrieve the feature id and type
# Transcode the value using the transcoding function
# Store the transcoded value into the database 