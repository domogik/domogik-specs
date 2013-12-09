****************
Plugin h2ometer
****************

*****************
Developper notes
*****************

.. toctree::



Plugin Objective
*****************
This plugin is used to measure water consumption using a diy modified water counter. It may work with a water meter with a pulse output but has never been tested.
It is also platform dependant. It must be installed on domogik running on a raspberry pi.

Water meter modification
*************************
Different kind of modifications can be done. The objective of the modification is to get an impulse on a raspberry gpio for each liter consumed.
For my part, i use a photo sensor placed around the needle that indicate 1/10 liter. With that method i have no hardware modification to do on the water meter and i have 1 impulse / 1 liter.

Electrical schematic
*********************
If your water meter is just near your raspberry you could use a very simple schematic with the photo sensor.

{IMG(src="display345")}{IMG}

R1 is used to generate current through the IR led and must be around 330 ohms.
R2 is a pullup that maintain the GPIO of the raspberry pi at high level when there is no signal.
The value must be between 5k to 50k (electronic is very indulgent !!).

If your water meter is far away (some meters) this schematic could be not very efficient.
So, i use this schematic

{IMG(src="display346")}{IMG}

I use a shmitt trigger to re-arrange the signal into a proper square form. It will also invert the signal, but each impuls will generate a rising and a falling edge so there is no importance on the value of the signal.
R2 and C1 must be near the trigger.

Installing the plugin
**********************
You must install quick2Wire python api and quick2wire-gpio-admin in ordre to read gpio from the Raspberry pi.
`https://github.com/quick2wire/quick2wire-python-api/blob/master/doc/getting-started-with-gpio.md <https://github.com/quick2wire/quick2wire-python-api/blob/master/doc/getting-started-with-gpio.md>`_
This library as the opposite of others has the big advantage that there is no need of root rights to read a gpio event with interrupts.

So you must install quick2Wire python api to read GPIO

.. code-block::caption="quick2wire gpio api installation"
    git clone https://github.com/quick2wire/quick2wire-python-api.git
    cd quick2wire-python-api/
    sudo python setup.py install
    


And you must install also quick2wire-gpio-admin which permit to configure GPIO

.. code-block::caption="quick2wire-gpio-admin Installation"
    git clone git://github.com/quick2wire/quick2wire-gpio-admin.git
    cd quick2wire-gpio-admin/
    make
    sudo make install
    


The default user used by domogik must be added to gpio user group
.. code-block::caption="Adding user to gpio group"
    sudo adduser $USER gpio{CODE}
    
    Plugin configuration
    *********************
    
    There is many parameters in the configuration part of the plugin
    
    !!!!startup-plugin
    It will indicate if the plugin must be start at Domogik startup
    
    !!!!pin
    This parameter indicate the pin number of the raspberry pi where the impuls has to be read. the number used here is the real pin number not the GPIO.
    For example GPIO 4 is defined on pin 7 of the header. So you must enter 7 in the configuration.
    {IMG(src="http://elinux.org/images/2/2a/GPIOs.png"
    {IMG}
    
    !!!!interval
    This parameter indicate the interval in minute between to data logging in database
    
    !!!!current-val
    This parameter indicate the current consumption in liters. It can be adjusted if there is a gap between real value and computed value or it can be used to initialize the value with your water meter value.
    
    xPL Schema
    ***********
    !!!!xpl-cmnd
    There is no usage of xpl-cmnd with this plugin
    
    !!!!xpl-stat
    The SENSOR.BASIC xPL schema is used in this module : http://xplproject.org.uk/wiki/index.php?title=Schema_-_SENSOR.BASIC
    
.. code-block::
    
    CONTROL.BASIC
    {
    DEVICE=h2ometer
    TYPE=liters
    CURRENT=<Current value in liters>
    }
    
 

!!!!xpl-trig
There is no usage of xpl-trig with this plugin
