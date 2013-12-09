*********
 Status 
*********
First version ok

*****************
 Goal of module 
*****************
This module allows to get events from a google calendar.

*************
 ShÃ©ma xPL 
*************
* ((xPL_calendar_schema|Proposition of calendar.basic schema))

Note : only ''startdate'' and ''object'' are used for this version.

***************
 Prerequisite 
***************

 Google account 
=================
You need a valid gmail account.

 Installation 
===============
You need to install python package for google data. 

 Debian/Ubuntu 
****************
 # apt-get install python-gdata

***************
 How it works 
***************
The xPL client listens to ''calendar.request'' messages. When it gets one, it asks google calendar for the given date. These three dates parameters are allowed :  
* TODAY : get today's events after current time
* TOMORROW : get tomorrow's events
* 2010-08-12 : get 8 october 2010 events

A ''calendar.basic'' message will be sent back for each event found.

****************
 Configuration 
****************
You need following entries : 

* email : email of gmail account
* password : password of gmail account
* calendarname : calendar name to use in gmail account. Default : email value
