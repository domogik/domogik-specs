{maketoc}
!REST /log
/log is used to view parts of log files from a host

__Warning__ : 
If host is the REST's host, it will read files from __/var/log/domogik/__ (or different depending on your configuration). Else, it will read files from __/var/log/domogik/hostname__.
So, you need to use __syslog-ng__ or another log service on various host to centralize all logs on REST's host.

!API
!!/log/tail/txt/&lt;hostname&gt;/&lt;filename without '.log'&gt;/&lt;number&gt;/&lt;offset&gt;
This will return as __text/plain__, the __number__ last end lines, with an __offset__.

!!/log/tail/html/&lt;hostname&gt;/&lt;filename without '.log'&gt;/&lt;number&gt;/&lt;offset&gt;
This will return as __text/html__, the __number__ last end lines, with an __offset__.
