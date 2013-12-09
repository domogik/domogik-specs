{maketoc}

!Purpose
This plugin allows sending message by TTS (Text To Speech).  

!Package Installation
!! TTS festival
For use TTS with festival for english language:

{CODE()}
# apt-get install festival
{CODE}

!! TTS espeak

!! TTS SVOX pico
{CODE()}
# apt-get install libttspico-utils
{CODE}


!Plugin configuration
!!Enabling plugin
You can enable plugin by using :
{CODE()}
dmgenplug tts
{CODE}

You just have to reload administration page to see the plugin in the list.

!!Configuration
!!Start plugin
You can now start the plugin (start button).

!!!software : Command line for use TTS software
* for french language with SVOX pico:
** pico2wave -l fr-FR -w tts.wav \&quot;%s\&quot; | paplay tts.wav 

* for french language with espeak:
** espeak -v fr \&quot;%s\&quot;

* for english language :
** echo \&quot;%s\&quot; | festival --tts




!Developper Notes

!!How the online plugin to test of order? 
In a final one, since the catalog xpl/bin it is necessary to launch the order. 
{CODE()}
./tts.py -f
{CODE}

In a final other, since the catalog xpl/bin it is necessary to launch the order. 
{CODE()}
./send.py xpl-cmnd tts.basic “speech=your_text&quot;
{CODE}



!!!xPL schema
* [http://xplproject.org.uk/wiki/index.php?title=Schema_-_TTS.BASIC|tts.basic]


!!!!Message to send to plugin for send message to TTS software
To ask a plugin to send a message, you should send this __xpl-cmnd__ message :
{CODE()}
TTS.BASIC
{
SPEECH=&lt;text to announce&gt;
[VOLUME=&lt;0 to 100&gt;]
[SPEED=&lt;-10 to 10&gt;]
[VOICE=&lt;name of voice to use&gt;]
}
{CODE}

For this moment only field &quot;speech&quot; is use.
