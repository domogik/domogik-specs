*********************
plugin_cron_interface
*********************
An interface to the cron plugin

List all cron jobs : stop, resume, delete.

Add a cron job : 
Actually 5 type of jobs with differents parameters. Some of them (like the HVAC one) may be created directly by a HVAC plugin.
Input fields :
day of the week : something like MoTueWeThFrSaSu, SaSu, We
Time : someting like 8:00, 23:35
Time interval : something like 8:00-11:00
Message fields : all the fields needed to send an xpl message.


All this actions are availables with xpl commands.
