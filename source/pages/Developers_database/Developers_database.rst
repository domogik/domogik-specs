*********
Database
*********


.. toctree::



Rules to respect absolutly
===========================

When making changes to the database, you ~~#F00:__must__~~ :
* Write the code that will upgrade / downgrade the database. See ((Developers_install_process|make changes to the database)).
* Write unit tests prooving your modifications are working. See ((Developers_tests|this page)).

0.1.0 Model
============

||__Part__|__Description__
((Database_structure_first_version|1st model))|Initial database model||

DEV. Model
===========

||__Model__|__Description__|__Status__
((Reduce_DeviceStats))|Reduce DeviceStats data|{GAUGE(value=>50, max=>100, label=>''dev'', perc=>true, labelsize=>50, height=>20, color=>green, bgcolor=>#EEEEEE)}{GAUGE}||

Ideas for Future Model
=======================

||__Model__|__Description__|__Status__
((Database_ui_terminal|UI Terminals Registration))|Terminals registration system|{GAUGE(value=>20, max=>100, label=>''draft'', perc=>true, labelsize=>50, height=>20, color=>green, bgcolor=>#EEEEEE)}{GAUGE}
((Database_graphs_improvements))|Graphs improvements|{GAUGE(value=>10, max=>100, label=>''dev'', perc=>true, labelsize=>50, height=>20, color=>green, bgcolor=>#EEEEEE)}{GAUGE}
((Database_building_description))|Building description|{GAUGE(value=>10, max=>100, label=>''dev'', perc=>true, labelsize=>50, height=>20, color=>green, bgcolor=>#EEEEEE)}{GAUGE}||