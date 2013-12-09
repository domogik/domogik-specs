.. toctree::



This page is a draft about reflexions for integrating ZoneMinder with Domogik

********
Install
********
Download and expand zmxap in /usr/local/zmxap

making the /var/run/zm dir manually, and making it mode 777 (755 ?), and start zm

copy  zmxap.conf.sample to zmxap.conf and tune it

lanch zmxap in /usr/local/zmxap :  sudo perl zmxap.pl

check des logs :  tail -f /tmp/zmxap.log


******************
Xpl specification
******************

Alarms
=======
Sent on alarm :
****************
xpl-trig
{
...
}
zm.alarm 
{
alarm_id=503     #id
cause=motion     #other values ?
state=on         # start of alarm
zone_data=all    # what the fuck is it ?
}

Sent during alarm :
********************
xpl-trig
{
...
}
zm.alarm 
{
}

TODO : 

xap-header
{
v=12
hop=1
uid=FFEA0901
class=Message.Display
source=zm.zoneminder.house:Portail
pid=16468
}
Display.Text
{
duration=ARRAY(0x9310d48)
line1=CCTV - Portail
line2=ARRAY(0x928f6a8)
priority=ARRAY(0x9310d68)
}
Display.Web
{
link=http://***MON IP***/zm//index.php?view=event&amp;eid=503
pic=http://***MON IP***/cgi-bin/nph-zms?mode=single&amp;monitor=1&amp;scale=100&amp;rand=1303025131
refresh=0.1
}

Sent at the end of alarm : 
****************************
xpl-trig
{
...
}
zm.alarm 
{
alarm-id=503     # id
cause=motion     # other values ?
state=off        # end of alarm
zone-data=all    # what the fuck is it ?

frames=179
alarm-frames=159
total-score=4879
max-score=46
avg-score=30
duration=30
}

external ressources :

XPL en perl : https://github.com/beanz/xpl-perl/

Demarage du plugin :


chris@ubuntu1004:~/domogik/src/domogik/xpl/bin$ python ./dump_xpl.py -f
2011-08-16 20:49:14.383518 - xpl-stat
{
hop=1
source=zm-zonemind.house
target=*
}
hbeat.app
{
interval=1
port=49152
remote-ip=192.168.1.30
pid=3238
}

2011-08-16 20:49:14.384779 - xpl-stat
{
hop=1
source=zm-zonemind.house
target=*
}
hbeat.app
{
interval=1
port=49152
remote-ip=192.168.1.30
pid=3238
}


Heartbeat

2011-08-16 20:50:14.513198 - xpl-stat
{
hop=1
source=zm-zonemind.house
target=*
}
hbeat.app
{
interval=1
port=49152
remote-ip=192.168.1.30
pid=3238
}
