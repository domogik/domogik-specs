!WARNING

__This is the old main page of the wiki, his content is not up to date. This is only an archive which will be soon removed
__
! Domogik projet 
!! Overview 
Domogik is a home automation software working on GNU/Linux operating systems

!! Status / Roadmap 
* ((CurrentStatus|Current status))
* [http://trac.domogik.org/domogik/roadmap|Roadmap]
* ((Screenshots|Screenshots))
* ((NextReleases|Ideas for next versions))

!! Developers team 
* ((WhoIsWho|Who is who))

!! How to help us 
* ((I18n|Traduction)) -- Domogik is looking for translators
* [http://trac.domogik.org/domogik/wiki/WebInterfaceModel#Wearelookingfor|UI resources] -- Domogik is looking for icons, etc

!! Releases 
* ((Domogik_version_numbering|Release numbering))

!!! Changelog
''Following changelog pages will be filled when first development version will become stable (in fonctionnality and structure)''
* Database Changelog
* REST Changelog
* Official Plugins Changelog
* Core Changelog
! End-user documentation 
!! Compatibility 
!!! Browser 
||__Browser__|__Main UI__
Firefox 3.0 / 3.5| No CSS reflexion, No background gradient
Firefox 3.6|No CSS reflexion
Chrome 5.0|OK||

!! Installation 
(([TOC(doc/Installation-*,|inline, noheading)]))

''TODO when released ok''
* Download package
* Install package
* Start Domogik

!! How to use Domogik 
!!! Domogik Overview 
''TODO when released ok''

(([TOC(doc/Presentation-*,|inline, noheading)]))

!!! Domogik Administration 
''TODO when released ok''

(([TOC(doc/Administration-*,|inline, noheading)]))

!!! Domogik Usage 
''TODO when released ok''

(([TOC(doc/Usage-*,|inline, noheading)]))


!! UI customisation 
''TODO when released ok''

!! Plugins 
!!! Device or software plugins 

Each plugin has its own page with the detail of its functionalities and requirements.

||__Plugin__|__Description__|__Target release version__
[tiki-index.php?page=plugins/X10 | X10] |Use X10 devices|0.1.0
[tiki-index.php?page=plugins/Plcbus|Plcbus] |Use Plcbus devices|0.1.0
[tiki-index.php?page=plugins/CallerIdModem|CallerIdModem] |Get caller ID with a modem|0.1.0
[tiki-index.php?page=plugins/Teleinfo|Teleinfo] |Get electricity consumtion information|0.1.0
[tiki-index.php?page=plugins/Mirror|Mirror] |Use of Mir:ror by Violet|trunk
[tiki-index.php?page=plugins/Wol|Wol] |Wake up computers with Wake on Lan|trunk
[tiki-index.php?page=plugins/XBMCNotification|XBMCNotification] |Send notifications to a XBMC Media Center|trunk
[tiki-index.php?page=plugins/GoogleAgenda|GoogleAgenda] |Get events from a google agenda|trunk
[tiki-index.php?page=plugins/IP-x800|IP-X800] |Use IP-X800 card|trunk
1Wire |Use OneWire devices |0.1.0||

Note : a target release version ''trunk'' indicates that the plugin is under development and can be checked out from Mercurial

!!! Domogik internal plugins 
REST is a special plugin acting as a gateway between xPL and the user interface.

||__Plugin__|__Description__|__Target release version__
[tiki-index.php?page=plugins/REST|REST]|Global information about REST|0.1.0
[tiki-index.php?page=plugins/REST-base|REST : /base]|Get data from database (area, rooms, devices, events, etc)|0.1.0
[tiki-index.php?page=plugins/REST-command|REST : /command]|/command : send commands to devices|0.1.0
[tiki-index.php?page=plugins/REST-events|REST : /events]|/events: get events from devices|0.1.0
[tiki-index.php?page=plugins/REST-stats|REST : /stats]|/stats : get stats from database|0.1.0
[tiki-index.php?page=plugins/REST-account|REST : /account]|List accounts, login, etc|0.1.0
[tiki-index.php?page=plugins/REST-plugin|REST : /plugin]|Start, stop xPL plugins|0.1.0
[tiki-index.php?page=plugins/REST-xpl-cmnd|REST : /xpl_cmnd]|Directly send a xPL message|0.1.0
[tiki-index.php?page=plugins/REST-statmgr|REST : Statistics Manager]|Record in database xpl activity on network|0.1.0||


!!How To

||TODO : Howto for installing a module, configuring plugin and creating device on Domogik||
! Development 
!!Rules to read before coding!
* ((Developer_rules|Rules to respect absolutly!!))

!! How to get install and get ready for developing Domogik  
* ((Use_mercurial|Grab the sources (mercurial)))
* ((Install_mercurial_windows|How to get Mercurial working on Windows))
* ((Domogik_installation_for_developpers|Domogik's installation))
* ((Errors_and_solutions|Some errors and their solutions))


!! General presentation 
* ((DevGeneral|General technical description on how Domogik is working))

!! Plugins 
* ((Mocks|Mocks))
* ((PluginDevelopment|How to develop a plugin))
** ((MultipleInterfacesPlugin|Multiple interfaces in a plugin))
** ((Plugin_setting_timer|Setting a Timer in a plugin))
* ((ReflexionAboutPluginFacilities|Reflexion about plugin facilities))
* ((AdaptNonPythonPlugin|How to adapt a non-python xpl plugin to Domogik ?))

!! Protocols 
* ((zwave|Information about zwave))

!! xPL 
* ((xPLDomogik|xPL &amp; Domogik))
* ((REST_statmgr|xPL Statistics Manager))
* ((xPL_config_request|How to fetch a config item over xPL))
* ((xPL_plugin_manager|xPL plugin manager))
* Domogik schema
** ((xPL_Domogik_system_schema|Domogik.system schema))
* Non official (xPL project) messages 
** ((xPL_teleinfo_schema|Teleinfo schema))
** ((xPL_calendar_schema|Calendar schema))
 
!! Database 
* ((Database_structure_first_version|Database structure))
* ((Spec_technologies|Technology list))
* ((Devices|Device types, features and usages))
* ((Actuators|Actuators))
* ((Sensors|Sensors))

!! User interface 
* ((Web_interface_model|Model for the web interface))
* Graphical resources
** ((Available_icons|List of already available icons)) 
* ((DjangoHttpProxy|HTTP proxy for django))


!! About coding 
* ((CodingRules|Coding rules))
* [http://doc.domogik.org|Code documentation]
* ((Internationalization|Internationalization))

!! Tools 
* [http://rennes1.dunnewind.net:8010/|Build bot]
* [http://hg.domogik.dunnewind.net/hgweb.cgi|Mercurial web interface]
* [DemoData] : create demo database
* [http://www.jsonlint.com/|Json validator]
* [http://hginit.com/|A mercurial tutorial]
* [http://www.timestamp.fr/|Play with timestamp]
!! Tests
* ((Core_team_test_capacity|Core Team test capacity))

!! Other stuff 
* ((WikiStructure|How to organize wiki)) -- Documentation organisation
* ((WikiGuide|How to use the Wiki)) -- naming conventions, internationalization...
