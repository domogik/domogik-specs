{IMG(src=&quot;https://docs.google.com/drawings/pub?id=1270aD9hLpPgboPCYwBNqCuZfS1ISzNEtMeO3a0VAo9g&amp;w=960&amp;h=720&quot;)}{IMG}

!!Package format
The package is compressed in tar.gz format, with:
*The XML definition file
*A package icon, size 96x96px (displayed on the package installation list)
*A package sample image, ~~#F00:size to define~~ (displayed on the package information page)
*All the icon a 'images' sub folder
Each icon are square format and named based on the id and size (eg. 'iconid_16.png')
!!XML Format
{CODE()}&lt;package type=&quot;icons_page&quot; version=&quot;1&quot;&gt;
  &lt;id&gt;packageid&lt;/id&gt;
  &lt;description&gt;
  My icons set
  &lt;/description&gt;
  &lt;changelog&gt;0.1 - set creation&lt;/changelog&gt;
  &lt;version&gt;0.1&lt;/version&gt;
  &lt;generated&gt;2012-01-30 21:51&lt;/generated&gt;
  &lt;author&gt;Me&lt;/author&gt;
  &lt;author-email&gt;me@domogik.org&lt;/author-email&gt;
  &lt;icons&gt;
    &lt;icon&gt;
      &lt;id&gt;iconid&lt;/id&gt;
      &lt;type&gt;png&lt;/type&gt;
      &lt;label&gt;My Icon&lt;/label&gt;
      &lt;size&gt;64&lt;/size&gt;
      &lt;size&gt;32&lt;/size&gt;
      &lt;size&gt;16&lt;/size&gt;
    &lt;/icon&gt;
  &lt;/icons&gt;
&lt;/package&gt;{CODE}
!!Django Start
*The packages list is loaded form the disk to the DomoWeb database (1).
So packages can be installed manually.
**The XML version is checked for compatibility with DomoWeb
**If the CSS does not exist, it is generated

!! Package installation
*The packages list is updated along with the cache update, but in a separate request from DomoWeb (2)
*The list of packages is displayed on the primary host page, with all the other packages lists
~~#F00:(add mockup)~~
*The package lists are generated from the actual installed list + the combined list from the repositories
{CODE()}FOREACH package FROM list_repositories
  IF package IS IN list_domoweb
    add package in list_installed
    IF package version &gt; installed version
       set update possible
    END IF
  ELSE
    IF xml version IS OK
      add package in list_available
    END
  END IF
END FOREACH{CODE}
* More information and sample view is displayed on click to the &quot;Info&quot; button
The information is grabbed from repo.domogik.org using AJAX, and displayed in a window.
~~#F00:(add mockup)~~
* On &quot;Install&quot; click, DomoWeb download the package, and check the XML version (3)
* DomoWeb extract the package to /usr/share/domoweb/icons/page/(id du package) (4)
* DomoWeb generates the CSS file based on the XML informations
** The CSS format will be:
{CODE()}.packageid_iconid.icon64 { background-image:url(../images/iconid_64.png);}
.packageid_iconid.icon32 { background-image:url(../images/iconid_32.png);}
.packageid_iconid.icon16 { background-image:url(../images/iconid_16.png);}
{CODE}
!! Set icon for a Page
~~#F00:(add mockup)~~
!! Apply icon style
Only apply class=&quot;packageid_iconid icon32&quot;