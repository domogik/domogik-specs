||__Created:__|22/06/2012
__Creator:__|jesuislibre
__Reviewers:__|
__Status:__|{GAUGE(value=>50, max=>100, label=>''dev'', perc=>true, labelsize=>50, height=>20, color=>green, bgcolor=>#EEEEEE)}{GAUGE}
__Target:__|0.x.0
__References:__|((Database_ui_terminal|Database Model))||

****************************
 Reduce DeviceStats storage
****************************

Some device can collect data every 10 seconds, in 24 hours, the device can collect 8640 data by item, in teleinfo device, they have 23 items, in one day the device colect (6*60*24*23) = 198720 items

By default, the reduce sytem, only reduce the same values (in the default mercurial branch), if you would like affine reduce stats, see flapping elimination (at bottom of this page)

******************
Actualy algorithm
******************


normal device stats
====================

{FANCYTABLE(head=>id~|~date~|~timestamp~|~skey~|~device_id~|~value_num~|~value_str)}
1~|~2012-06-24 05:27:01~|~1340508421~|~temp~|~1~|~10~|~10
2~|~2012-06-24 05:27:02~|~1340508422~|~temp~|~1~|~10~|~10
3~|~2012-06-24 05:27:03~|~1340508423~|~temp~|~1~|~10~|~10
4~|~2012-06-24 05:27:04~|~1340508424~|~temp~|~1~|~10~|~10
5~|~2012-06-24 05:27:05~|~1340508425~|~temp~|~1~|~11~|~11
6~|~2012-06-24 05:27:06~|~1340508426~|~temp~|~1~|~12~|~12
7~|~2012-06-24 05:27:07~|~1340508427~|~temp~|~1~|~11~|~11
8~|~2012-06-24 05:27:08~|~1340508428~|~temp~|~1~|~11~|~11
9~|~2012-06-24 05:27:09~|~1340508429~|~temp~|~1~|~11~|~11
10~|~2012-06-24 05:27:10~|~1340508430~|~temp~|~1~|~12~|~12
11~|~2012-06-24 05:27:11~|~1340508431~|~command~|~2~|~NULL~|~on
12~|~2012-06-24 05:27:12~|~1340508432~|~command~|~2~|~NULL~|~on
13~|~2012-06-24 05:27:13~|~1340508433~|~command~|~2~|~NULL~|~on
14~|~2012-06-24 05:27:14~|~1340508434~|~command~|~2~|~NULL~|~on
15~|~2012-06-24 05:27:15~|~1340508435~|~command~|~2~|~NULL~|~off
16~|~2012-06-24 05:27:16~|~1340508436~|~command~|~2~|~NULL~|~off
17~|~2012-06-24 05:27:17~|~1340508437~|~command~|~2~|~NULL~|~off
18~|~2012-06-24 05:27:18~|~1340508438~|~command~|~2~|~NULL~|~on
19~|~2012-06-24 05:27:19~|~1340508439~|~command~|~2~|~NULL~|~on
20~|~2012-06-24 05:27:20~|~1340508440~|~command~|~2~|~NULL~|~on
{FANCYTABLE}

 reduced device stats
======================

{FANCYTABLE(head=>id~|~date~|~timestamp~|~skey~|~device_id~|~value_num~|~value_str)}
1~|~2012-06-24 05:27:01~|~1340508421~|~temp~|~1~|~10~|~10
4~|~2012-06-24 05:27:04~|~1340508424~|~temp~|~1~|~10~|~10
5~|~2012-06-24 05:27:05~|~1340508425~|~temp~|~1~|~11~|~11
6~|~2012-06-24 05:27:06~|~1340508426~|~temp~|~1~|~12~|~12
7~|~2012-06-24 05:27:07~|~1340508427~|~temp~|~1~|~11~|~11
9~|~2012-06-24 05:27:09~|~1340508429~|~temp~|~1~|~11~|~11
10~|~2012-06-24 05:27:10~|~1340508430~|~temp~|~1~|~12~|~12
11~|~2012-06-24 05:27:11~|~1340508431~|~command~|~2~|~NULL~|~on
14~|~2012-06-24 05:27:14~|~1340508434~|~command~|~2~|~NULL~|~on
15~|~2012-06-24 05:27:15~|~1340508435~|~command~|~2~|~NULL~|~off
17~|~2012-06-24 05:27:17~|~1340508437~|~command~|~2~|~NULL~|~off
18~|~2012-06-24 05:27:18~|~1340508438~|~command~|~2~|~NULL~|~on
20~|~2012-06-24 05:27:20~|~1340508440~|~command~|~2~|~NULL~|~on
{FANCYTABLE}

in this example, the storage was reduced by 35%

****************
Round algorithm
****************


In this sample, they have 92 items

 simple round algorithm (developpement only)
=============================================


rounded by 1000 modulos / 27 differents lines (__70% reduced__)

.. image:: ../../_static/images/421

 flapping elimation algorithm (developpement only)
===================================================


__Note__: This algorithm, is already implemented in "Reduce device stats volumetry" mercurial branch. The round is optional, in developpement, you must add a parameter in domogik.cfg in database section if you would like affine reduce stats with round optino.

.. code-block:: json


    db_round_filter = {"12" : { "total_space" : 1048576, "free_space" : 1048576, "percent_used" : 0.5, "used_space": 1048576 },"13" : { "hchp" : 500, "hchc" : 500, "papp" : 100, "iinst" : 2 }}{CODE}
    
    rounded by 1000 range (up/down = 500) / 5 differents lines (__95% reduced__)
    
    .. image:: ../../_static/images/422
    