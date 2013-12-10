*********************************
How to secure UI+REST API access
*********************************

||__Created:__|16/02/2012
__Creator:__|Ferllings
__Reviewers:__|
__Status:__|{GAUGE(value=>10, max=>100, label=>''draft'', perc=>true, labelsize=>50, height=>20, color=>green, bgcolor=>#EEEEEE)}{GAUGE}
__Target:__|???
__References:__| ||

This document will gather all techniques and ideas to secure Domogik UI access.

 Requirements
==============

* The link between the REST API and the UI should be secure (HTTPS use)
* The link between the Web browser and DomoWeb should be secure (HTTPS use)
* The REST API should have an authentification method, with multiple session handeling.
* DomoWeb should base the authentification and session on REST API authentification process.
* 2 different security level between Internal access and External access
** Internal access: Only the Admin section require auth. View auth is optional. Large connection time
** External access: Both  Admin and view sections require auth, Shorter connection time
** External public access: A stronger auth methode can be used for very unsecure access. (One time password)

 Techniques
============

REST Auth : http://developer.netflix.com/docs/Security#0_18325

 Independent techniques
========================

* VPN use
* Firewall configuration