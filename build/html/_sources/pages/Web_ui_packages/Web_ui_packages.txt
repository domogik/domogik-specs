{IMG(src="https://docs.google.com/drawings/pub?id=1270aD9hLpPgboPCYwBNqCuZfS1ISzNEtMeO3a0VAo9g&amp;w=960&amp;h=720")}{IMG}

Package format
===============

The package is compressed in tar.gz format, with:
*The XML definition file
*A package icon, size 96x96px (displayed on the package installation list)
*A package sample image, ~~#F00:size to define~~ (displayed on the package information page)
*All the icon a 'images' sub folder
Each icon are square format and named based on the id and size (eg. 'iconid_16.png')
XML Format
===========

.. code-block:: json


    <package type="icons_page" version="1">
      <id>packageid</id>
      <description>
      My icons set
      </description>
      <changelog>0.1 - set creation</changelog>
      <version>0.1</version>
      <generated>2012-01-30 21:51</generated>
      <author>Me</author>
      <author-email>me@domogik.org</author-email>
      <icons>
        <icon>
          <id>iconid</id>
          <type>png</type>
          <label>My Icon</label>
          <size>64</size>
          <size>32</size>
          <size>16</size>
        </icon>
      </icons>
    </package>

Django Start
=============

*The packages list is loaded form the disk to the DomoWeb database (1).
So packages can be installed manually.
**The XML version is checked for compatibility with DomoWeb
**If the CSS does not exist, it is generated

 Package installation
======================

*The packages list is updated along with the cache update, but in a separate request from DomoWeb (2)
*The list of packages is displayed on the primary host page, with all the other packages lists
~~#F00:(add mockup)~~
*The package lists are generated from the actual installed list + the combined list from the repositories
.. code-block:: json


    FOREACH package FROM list_repositories
      IF package IS IN list_domoweb
        add package in list_installed
        IF package version > installed version
           set update possible
        END IF
      ELSE
        IF xml version IS OK
          add package in list_available
        END
      END IF
    END FOREACH

* More information and sample view is displayed on click to the "Info" button
The information is grabbed from repo.domogik.org using AJAX, and displayed in a window.
~~#F00:(add mockup)~~
* On "Install" click, DomoWeb download the package, and check the XML version (3)
* DomoWeb extract the package to /usr/share/domoweb/icons/page/(id du package) (4)
* DomoWeb generates the CSS file based on the XML informations
** The CSS format will be:
.. code-block:: json


    .packageid_iconid.icon64 { background-image:url(../images/iconid_64.png);}
    .packageid_iconid.icon32 { background-image:url(../images/iconid_32.png);}
    .packageid_iconid.icon16 { background-image:url(../images/iconid_16.png);}
    

 Set icon for a Page
=====================

~~#F00:(add mockup)~~
 Apply icon style
==================

Only apply class="packageid_iconid icon32"