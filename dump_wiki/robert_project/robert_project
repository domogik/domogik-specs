************************************
Uses Cases for General Interactions
************************************

This document purpose is for listing simple to more complex interaction with Domogik system, and start to clarify the general notions that are going to be needed to move to a more interactive, intuitive, intelligent system.

Nothing in this document will target a specific hardware or technology.
A 'command' could be a simple button, a vocal sentence, ...
A 'notification' could be a text message on a screen, a TTS sentence, ...
An 'event', can be a sensor event, a date/time, ...


#Mail
======
Description
************
The mailman just dropped an envelop in the mailbox, outside the house.
And the system will notify the user(s)
Notions
********
The event simply update the a general state.
__state__: mail(s) in the mailbox (on/off, or 0...999 if possible)

This change of state, will result into notification actions, but it depends of general context
__state__: does notifications are allowed for this particular time (night?)
__state__: does notification are not in conflict with any other general __state__ (do not disturb, holiday, ...)

It depends also on users specific context
So for each user, that (generally) want to be notified for this event:
__location__: does the user is at home? outside? at work connected with his phone?
__state__: does the user available? (doing home work, at the phone, ...)
__preference__: Does the user want to be notified on real time? when he comes back?
__preference__: what is the preferred way for notification? TTS? via TXTmsg/email if not at home? Message on screen?

#General speech type command
=============================
Description
************
A user send a vocal command: "Please, turn on the light"
Notions
********
The first thing to identify is the __target__ of the command
Is the __target__ indicated in the vocal command? If not how to reduce the number of possible targets?
How many 'light' devices are available? (For unique devices like TV, the target will be more easy to find)
Where is the user located? How many 'light' in the same __location__?

If many __target__ are possible, the system can ask for more details about the target.

When the __target__ is found, the next step is to identify the __user__ that request the action.
Does the user use a specific terminal, with __authentication__?
If it is not possible to identify the __user__, then the user is considered as Guest.

Does the user has the right for this command?
Does the target action can be regulated by general __state__? (light at 50% if during the night)

If so does the user have __preferences__ for this command? (the user may have set the light at 70% the last time at the same time period)


#Shopping list (speech command)
================================
Description
************
A user initiate a vocal command: "Please, add to the shopping list"
Then, he can add some items :
"water"
"milk"
..
And to finish the list :
"thats is all" / "end" / ...

Later, the user can retrieve the shopping list : "Please give me the shopping list"

Notions
********
The system must be able to start to listen for a list of vocal items and append them in a list in memory.
The system must be able to detect the end of the list
The system must be able to store permanently the list and complete it when requested
The system must be able to give back the list when needed. It could be on various format : voice, texte, email ("send the shopping list to my wife"), ...

Can we have as many shopping lists (some notes finally) as we want ?
"Please, add to XXXXXXXXXX"

# Speech, photo and glasses/screens interactions
=================================================
Description
************
The user plug a usb key with some photo/schematics in a "electric plan" folder
He wears his glasses and ask "Please, display the pictures from the folder electric plan of the usb key on my glasses"
The system loads the picture and display them on the glasses
Then the user can do some actions : "next", "previous", "end"

Notions
********
This is a quite advanced usage : get some data, send them to a component (which will make a copy or act as a proxy) and display them on a device. The device can be glasses, screens, tablets

The command may also be done with a drag and drop on a user interface instead of a voice control
