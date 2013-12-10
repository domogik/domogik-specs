*************************************
Specifications : packages repository
*************************************


Overview
=========

In Domogik 0.4.0 the packages management will be different from the 0.3 release. Here are the main points :
* packages are no more in Domogik sources : they are available on github repositories (or somewhere else). Basically, a package will now be a zip online file url.
* we won't use anymore a cache feature of the packages list : this is a source of various bugs and there are no real good points on doing this. Now, the packages list will always be downloaded when displaying the related page in domogik admin (or any other UI). We will need so to handle some cache feature (HTTP 200/304) to improve performances.


Points that are not yet very clear
***********************************


* Rating system
* How to handle several repositories in the display ?
* Nightly builds
* Branches management for plugin repositories
* How to get a zip from a tag in git ?
* Documentation building
* MD5
* Use github accounts for login on the tool for developpers ?
* Normalizer 'focus' packages picture format

Global specifications
======================


Domogik admin part (or any other UI)
*************************************

For all Components (Domogik admin, user interfaces for icons, ...) (let's call it a *client*)that want to install packages, here is allow it will work :

The user display the *packages* main page. This page is only displayed for a *stable* repository.
* the page will try to download a json file from the online tool (let's call it *DRM*). the json file will be grab by calling an url with a parameter that contains the needed packages type. Example : GET http://drm/packages/dmg_version=0.4.0&amp;repo=stable&amp;type=plugin,foo. The dmg_version parameter is used to display only the packages compliant with the domogik release. The repo parameter is used to choose the repository from which we want to display the packages. There are 1 "special" value for repo : "stable". This means that this is the stable repository of this server. Any other repositories will not be considered as stable and could be used for various purpose : nightly builds, testing, experimental, ...
* the json file is downloaded
* the page layout is created. There may be several parts in the page layout : this depends on the client. The layout can be updated when a new client release is installed. In the layout there can be several parts : "focus on", "more downloaded", "best rated", ... This will allow to have nice pages like https://play.google.com/store . Each part will get its informations from a section of the json (see json chapter for more informations). Each package displayed on the page will have these informations : icon, type+name, version, start of the description. A click on it should expand it and display all needed informations and the install button.

The user display an alternate repository *packages* page. 
* the page will download the json file
* the page layout is created. For non stable repositories, there is no "fun" layout. For each type required, the following will be displayed : a title with the type and the list of all packages



Json file
**********


To allow clients to display nice pages as https://play.google.com/store, the json will be split in several sections. The sections will be the same, whatever the types a client requested. Here are some ideas :

* a section 'repository' with informations about the repository :
** type : stable, testing, ...
** owner (domogik, society, someone, ...)
** domogik min release compatibility (0.4.0)
** domogik max release compatibility (999.999.999 by default), will maybe use in the future
* a section by package type required by the client. Each package contains :
** TODO
* a section 'more downloaded'. Each package contains :
** type, name. This will be sort of a shorcut to find the package in the package type related section
* a section 'best rated'. Content is the same as 'more downloaded'
* a section 'lastests'. Content is the same as 'more downloaded'
* a section 'focus'. This section will be used by the DRM owner to "suggest" some packages to user. This may be a new package, a christmas icon theme in december, .... 2 actions can be done : install or go to an url. Each package contains :
** type : plugin, icon, ... An extra value should be allowed : advertising. This will tell that this is not a package but just sort of an advertising. This could be use for some communication operations later If this extra value is set, there will be no install operation available.
** name
** a "big picture" link. This picture format should be normalized !
** optionnal : an url. This could be use to open a dedicated page. 

DRM
****


!!!!Users
There will be 2 sort of users that can use DRM : 
* developpers to publish new packages
* owners to manages packages
* anonymous

!!!!Developpers
A developper can do the following actions : 
* login, logout
* list its packages
* add a package (which will be reviewed by an owner before being activated)
* disable an existing package

!!!!Owners
An owner can't do the same actions as a developper! If an owner needs to do so, he should create 2 accounts.

An owner can do the following actions :
* login, logout
* list last added packages
* list all packages and filter/order them
* validate or not a package and give a description of the result

!!!!Anonymous
Anonymous people will have a read only view of the validated packages as already done on repo.domogik.org in 0.3

Detailed specifications
========================


TODO :)