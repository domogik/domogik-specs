!RINOR / REST

The RINOR/REST server is a gateway between all User Interfaces (UI), the xPL network and the database. 

The stable API of Rest can be found for each version in the official documentation : http://docs.domogik.org/domogik/dev/en/ chapter RINOR. 

__All the below pages are only specifications of draft. Use them with caution. __

!!Log viewing (candidate for Domogik 0.2.0)
||__Part__                                |__Description__                                               |__Rest API number__|__Progress__
((REST_log|REST : /log))                  |View log files from REST                                      |0.4                |{GAUGE(value=&gt;70, max=&gt;100, label=&gt;''dev'', perc=&gt;true, labelsize=&gt;50, height=&gt;20, color=&gt;green, bgcolor=&gt;#EEEEEE)}{GAUGE}||

!!Scenario
||__Part__                                |__Description__                                               |__Rest API number__|__Progress__
((REST_scenario|REST : /scenario))        |Scenario                                                      |                   |{GAUGE(value=&gt;10, max=&gt;100, label=&gt;''specification'', perc=&gt;true, labelsize=&gt;50, height=&gt;20, color=&gt;green, bgcolor=&gt;#EEEEEE)}{GAUGE} {GAUGE(value=&gt;0, max=&gt;100, label=&gt;''dev'', perc=&gt;true, labelsize=&gt;50, height=&gt;20, color=&gt;green, bgcolor=&gt;#EEEEEE)}{GAUGE}||

!!Next data model
!!! Data service (REST)
||__Part__                                |__Description__                                               |__Data API number__|__Progress__
((RINOR_base2|/base))               |Get data from the database (pages, features, devices, etc)    |                   |{GAUGE(value=&gt;30, max=&gt;100, label=&gt;''draft'', perc=&gt;true, labelsize=&gt;50, height=&gt;20, color=&gt;green, bgcolor=&gt;#EEEEEE)}{GAUGE}
((REST_stats2|/stats))              |/stats : get stats from the database                         |                   |{GAUGE(value=&gt;0, max=&gt;100, label=&gt;''draft'', perc=&gt;true, labelsize=&gt;50, height=&gt;20, color=&gt;green, bgcolor=&gt;#EEEEEE)}{GAUGE}||

!!! Events service (Server Sent Event ?)
||__Part__                                |__Description__                                               |__Events API number__|__Progress__
((RINOR_xpl_msgs|xpl_msgs))        |Get filtered xPL messages                                     |                   |{GAUGE(value=&gt;20, max=&gt;100, label=&gt;''specification'', perc=&gt;true, labelsize=&gt;50, height=&gt;20, color=&gt;green, bgcolor=&gt;#EEEEEE)}{GAUGE}
((RINOR_events2|events))           |/events: get events                                           |                   |{GAUGE(value=&gt;10, max=&gt;100, label=&gt;''draft'', perc=&gt;true, labelsize=&gt;50, height=&gt;20, color=&gt;green, bgcolor=&gt;#EEEEEE)}{GAUGE}||
!!! Commands service (JSON-RPC)