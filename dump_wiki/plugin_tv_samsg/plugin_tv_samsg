{maketoc}

!Purpose

This plugin's goal is to control a Samsung television with EX-link port (sort of a serial port).

::{IMG(attId=&quot;203&quot;)}{IMG}::

!EX Link wire
!!Schematic
{IMG(attId=&quot;149&quot;)}{IMG}

!!Make your own wire 
!!!Materials needed
You need a simple stereo wire with a 3.5mm jack plug and a female DB9 :

{IMG(attId=&quot;196&quot;)}{IMG}

{IMG(attId=&quot;197&quot;)}{IMG} {IMG(attId=&quot;198&quot;)}{IMG}

Brase wire on DB9 like told in schematic :

{IMG(attId=&quot;199&quot;)}{IMG}

And finally, protect your new EX Link wire :

{IMG(attId=&quot;200&quot;)}{IMG}

!How to plug
Just plug EX Link's jack side on television like this : 

{IMG(attId=&quot;202&quot;)}{IMG}

If your computer doesn't have any serial port, you may need a serial&lt;=&gt;usb adaptator.

{IMG(attId=&quot;201&quot;)}{IMG}

!Developper notes
!!xPL Schema
No xPL schema exists for television control. We choose to use [http://xplproject.org.uk/wiki/index.php?title=Schema_-_CONTROL.BASIC|CONTROL.BASIC schema] to send commands. Acknowledgments will be made by a [http://xplproject.org.uk/wiki/index.php?title=Schema_-_SENSOR.BASIC|SENSOR.BASIC schema]

!!!xpl-cmnd

{CODE()}
xpl-cmnd
{
...
}
control.basic
{
device=&lt;television name&gt;
type=television
current=&lt;alias for command : power_on, channel_up, etc&gt;
[data1=&lt;optionnal value : current='channel', data1=1 to set channel 1&gt;]
}
{CODE}

!!!xpl-stat
||TODO : if we can get television power status, return this data||

!!!xpl-trig
Acknowloedgment for successfull xpl-cmnd :
{CODE()}
xpl-cmnd
{
...
}
sensor.basic
{
device=&lt;television name&gt;
type=television
current=&lt;alias for command : power_on, channel_up, etc&gt;
[data1=&lt;optionnal value : current='channel', data1=1 to set channel 1&gt;]
}
{CODE}

!!Widgets reflexion
{IMG(attId=&quot;148&quot;)}{IMG}

!!Protocol
!!!Commands
See Proof of concept for the moment

Set volume to a level :
{CODE()}
&quot;\x08\x22\x01\x00\x00\x05\xFF&quot; ;      // Cmd: &quot;Volume at 5/100&quot;
octet 6=volume. 
{CODE}

!!!Return
* &quot;0x03 0x0C 0xFF&quot; if error
* &quot;0x03 0x0C 0xF1&quot; if OK. 

!!Proof of concept
!!!samsung_led.py : list of action/code
{CODE()}
COMMANDS = {
&quot;power_standby&quot; : &quot;00000001&quot;, # Power Standby    ### OK
&quot;power_on&quot; : &quot;00000002&quot;, # Power On              ### OK
&quot;get_power_status&quot; : &quot;00000000&quot;, # Get power status   ### ?????
&quot;mute_toggle&quot; : &quot;02000000&quot;, # Mute toggle        ### OK
&quot;volume_up&quot; : &quot;01000100&quot;, # Master Volume Up     ### OK
&quot;volume_down&quot; : &quot;01000200&quot;, # Master Volume Down     ### OK
&quot;channel_up&quot; : &quot;03000100&quot;, # Channel Up    ### OK
&quot;channel_down&quot; : &quot;03000200&quot;, # Channel Down  ### ERR
&quot;tv&quot; : &quot;0a000000&quot;, # TV       ### OK
&quot;av1&quot; : &quot;0a000100&quot;, # AV 1       ### OK
&quot;av2&quot; : &quot;0a000101&quot;, # AV 2       ### OK
&quot;av3&quot; : &quot;0a000102&quot;, # AV 3       ### OK
&quot;svideo1&quot; : &quot;0a000200&quot;, # S-Video 1     ### OK
&quot;svideo2&quot; : &quot;0a000201&quot;, # S-Video 2     ### OK
&quot;component1&quot; : &quot;0a000300&quot;, # Component 1    ### OK
&quot;component3&quot; : &quot;0a000302&quot;, # Component 3    ### OK
&quot;pc1&quot; : &quot;0a000400&quot;, # PC 1     ### OK
&quot;pc2&quot; : &quot;0a000401&quot;, # PC 2     ### OK
&quot;hdmi1&quot; : &quot;0a000500&quot;, # HDMI 1   ### OK
&quot;hdmi2&quot; : &quot;0a000501&quot;, # HDMI 2   ### OK
&quot;hdmi3&quot; : &quot;0a000502&quot;, # HDMI 3   ### OK
&quot;hdmi4&quot; : &quot;0a000503&quot;, # HDMI 4   ### OK
&quot;dvi1&quot; : &quot;0a000600&quot;, # DVI 1   ### OK
&quot;dvi2&quot; : &quot;0a000601&quot;, # DVI 2   ### OK
&quot;dvi3&quot; : &quot;0a000602&quot;, # DVI 3   ### OK
&quot;dynamic&quot; : &quot;0b000000&quot;, # Dynamic
&quot;standard&quot; : &quot;0c000000&quot;, # Standard
&quot;wide&quot; : &quot;0b000002&quot;, # Wide
&quot;black_adjust_off&quot; : &quot;0b090000&quot;, # Black Adjust Off
&quot;black_adjust_medium&quot; : &quot;0b090002&quot;, # Black Adjust Medium
&quot;black_adjust_low&quot; : &quot;0b090001&quot;, # Black Adjust Low
&quot;black_adjust_high&quot; : &quot;0b090003&quot;, # Black Adjust High
&quot;dynamic_contrast_off&quot; : &quot;0b090100&quot;, # Dynamic Contrast Off
&quot;dynamic_contrast_low&quot; : &quot;0b090101&quot;, # Dynamic Contrast Low
&quot;dynamic_contrast_medium&quot; : &quot;0b090102&quot;, # Dynamic Contrast Medium
&quot;dynamic_contrast_high&quot; : &quot;0b090103&quot;, # Dynamic Contrast High
&quot;color_space_auto&quot; : &quot;0b090300&quot;, # Color Space Auto
&quot;color_space_wide&quot; : &quot;0b090301&quot;, # Color Space Wide

# Others
&quot;aspect_16_9&quot; : &quot;0b0a0100&quot;, # 16/9 aspect
&quot;aspect_zoom_1&quot; : &quot;0b0a0101&quot;, # Zoom 1 aspect
&quot;aspect_zoom_2&quot; : &quot;0b0a0102&quot;, # Zoom 2 aspect
&quot;aspect_wide_fit&quot; : &quot;0b0a0103&quot;, # Wide Fit aspect
&quot;aspect_4_3&quot; : &quot;0b0a0104&quot;, # 4/3 aspect
&quot;speaker_off&quot; : &quot;0c060000&quot;, # Speaker Off
&quot;speaker_on&quot; : &quot;0c060001&quot;, # Speaker On

# Sound commands
&quot;sound_standard&quot; : &quot;0c000000&quot;, # Standard
&quot;sound_music&quot; : &quot;0c000001&quot;, # Music
&quot;sound_movie&quot; : &quot;0c000002&quot;, # Movie
&quot;sound_custom&quot; : &quot;0c000004&quot;, # Custom
&quot;sound_eq_standard&quot; : &quot;0c010000&quot;, # EQ Standard
&quot;sound_eq_music&quot; : &quot;0c010001&quot;, # EQ Music
&quot;sound_eq_video&quot; : &quot;0c010002&quot;, # EQ Movie
&quot;sound_eq_speech&quot; : &quot;0c010003&quot;, # EQ Speech
&quot;sound_eq_custom&quot; : &quot;0c010004&quot;, # EQ Custom
&quot;sound_srs_tru_surround_on&quot; : &quot;0c020000&quot;, # SRS Tru Surround On
&quot;sound_srs_tru_surround_off&quot; : &quot;0c020001&quot;, # SRS Tru Surround Off
&quot;sound_multi_track_mono&quot; : &quot;0c040000&quot;, # Multi-Track Mono
&quot;sound_multi_track_stereo&quot; : &quot;0c040001&quot;, # Multi-Track Stereo
&quot;sound_multi_track_sap&quot; : &quot;0c040002&quot;, # Multi-Track SAP

# Tests
&quot;test&quot; : &quot;04010002&quot;, # Channel 2 on TNT
&quot;test&quot; : &quot;04000002&quot;, # Channel 2 on Classical TV
}

{CODE}
!!!tv_test.py : pof
{CODE()}
#!/usr/bin/python
# -*- coding: utf-8 -*-

import binascii
import serial
from samsung_led import COMMANDS
import sys


class SamsungTVException(Exception):  
    &quot;&quot;&quot;                                                                         
    Samsung television control exception                                                           
    &quot;&quot;&quot;                                                                         
                                                                                
    def __init__(self, value):                                                  
        Exception.__init__(self)
        self.value = value                                                      
                                                                                
    def __str__(self):                                                          
        return repr(self.value)           


class SamsungTV:
    &quot;&quot;&quot; Control samsung television
    &quot;&quot;&quot;

    def __init__(self, log = None, callback = None):
        &quot;&quot;&quot; Init samsung TV controller
        &quot;&quot;&quot;
        self._log = log
        self._callback = callback
        self._samsung = None


    def open(self, device):
        &quot;&quot;&quot; Open EX Link
            @param device : serial port connected to EX Link
        &quot;&quot;&quot;
        try:
            print(&quot;Try to open Samsung EX Link device : %s&quot; % device)
            self._samsung = serial.Serial(device, 9600, 
                                parity=serial.PARITY_NONE,
                                stopbits=serial.STOPBITS_ONE,
                                xonxoff=serial.XOFF)
            print(&quot;EX Link device opened&quot;)
        except:
            error = &quot;Error while opening EX Link device : %s. Check if it is the good device or if you have the good permissions on it.&quot; % device
            raise SamsungTVException(error)


    def send(self, cmd_alias):
        &quot;&quot;&quot; Send command code associated to alias to EX Link
            @param cmd_alias : alias 
        &quot;&quot;&quot;
        print cmd_alias
        if not cmd_alias in COMMANDS:
            print &quot;Command not known : '%s'&quot; % cmd_alias
            return
        cmd = self.generate_command(COMMANDS[cmd_alias])
        print cmd
        data = binascii.unhexlify(cmd)
        self._samsung.write(&quot;%s&quot; % data)
        #res = ser.read(16)
        #print &quot;res=%s&quot; % res

    def generate_command(self, value):
        &quot;&quot;&quot; Generate command with header and checksum
        &quot;&quot;&quot;
        # TODO : review quality
        HEADER=&quot;0822&quot;
        data = value.decode(&quot;hex&quot;)
        sum = 0
        for byte in data:
            sum += ord(byte)
        sum+=42
        CS=generatechecksum(HEADER+value)
        return HEADER+value+CS


    def close(self):
        &quot;&quot;&quot; Close EX Link
        &quot;&quot;&quot;
        self._samsung.close()



#### for test purpose : taken from http://www.avsforum.com/avs-vb/showthread.php?t=703453
def generatechecksum(value):
    data = value.decode(&quot;hex&quot;)

    sum = 0
    for byte in data:
        sum += ord(byte)
    print &quot;Two's complement:&quot;, hex((~sum + 1) &amp; 0xFF)
    data = hex((~sum + 1) &amp; 0xFF)
    data = str(data)[2:]
    if ( len(data) &lt; 2 ):    

       data = '0' + data
    print &quot;checksum &quot; + data
    return data


#print generatechecksum(&quot;01000100&quot;)
my_tv = SamsungTV(None, None)
my_tv.open(0)
my_tv.send(sys.argv[1])
my_tv.close()
{CODE}
