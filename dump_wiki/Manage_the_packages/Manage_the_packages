!Manage the packages
{maketoc}

!!What is a package ?
The ''package'' term has been introduced in Domogik 0.2.0. A package is a piece of software which has features in Domogik. Currently a package can be : 
* a plugin
* an external member (no code, only configuration files to handle an external xPL client : Rfxcom xPL, ...)

''Notice : the packages management is not available in development as you already have access to all the packages sources.''

!!!Where can I find the packages ?
Domogik is delivered without any packages (so, without any plugins) since the 0.2.0 version. To use your Plcbus, onewire or other devices, you need first to install the package which handles these devices. This installation can be done from the administration pages of Domoweb.

All packages are available on online repositories. Currently there are 4 official repositories. You can see them on http://repo.domogik.org/repository/ :

{IMG(attId=&quot;415&quot;)}{IMG}

!!!!The stable repository
This is the only activated repository after a Domogik installation. It is the main repository with official, stable and validated packages.

!!!!The testing repository
This is the repository with working packages. These packages are not yet validated so they could be unstable.

!!!!The experimental repository
This is the repository with experimental packages. They are not stable and are available only for testing or preview.

!!!!The nightly builds repository
Every night, all packages available in Domogik sources are generated. These packages are not stable and may even not work at all.

!!How can I activate repositories ?
To add or remove a directory, you must manually edit (as ''domogik'' user) the file __/etc/domogik/sources.list__. Here is an example with the 4 official repositories configured :
{CODE()}
# Domogik official repositories
# priority   # url
500          http://repo.domogik.org/repository/stable/
400          http://repo.domogik.org/repository/testing/
300          http://repo.domogik.org/repository/experimental/
100          http://repo.domogik.org/repository/nightly/
{CODE}
The higher the priority is, the higher a package in the corresponding repository will have priority during a package installation.

Activating repositories is a manual operation for security reasons.

!!Looking for the packages list without having Domogik installed ?
If you want to see the packages list, just go to http://repo.domogik.org/package/. 

{IMG(attId=&quot;398&quot;)}{IMG}

By default only stable packages are displayed. Just check the appropriate checkboxes to view packages from other repositories.

!!Manage packages from Domoweb
Just go to the Domoweb administration panel. In the left menu, go to the section __Hosts__ : you will see the list of all hosts where Domogik is installed. Here is the list on a single host installation (darkstar is the name of the computer) :

{IMG(attId=&quot;400{file name=&quot;menu_01.png&quot;}&quot;)}{IMG}

Click on the host name :

{IMG(attId=&quot;399&quot;)}{IMG}

On the top, you will find 3 tabs : 
* Repositories : list all the activated repositories and allow to update the cache.
* Plugins : list all plugins packages.
* External members : list all external members packages.

!!!Repositories
Updating the cache consist in getting from the repositories the list of the available packages. To update the cache, just click on the __Update cache__ button :

{IMG(attId=&quot;401&quot;)}{IMG}

When the cache is updated, you will get a notification :

{IMG(attId=&quot;402&quot;)}{IMG}

!!!Plugins
{IMG(attId=&quot;403&quot;)}{IMG}

This page is divided in 2 sections :
* Installed : the list of the installed plugin packages.
* Available : the list of the plugin packages you could install. When a plugin has been installed, it is not displayed anymore in the available list.

!!!!Search for a plugin
You can use the search field to find a plugin with a keyword :

{IMG(attId=&quot;404&quot;)}{IMG}

!!!!Install a plugin
When you have found the plugin you are looking for, just click on the __Install__ button :

{IMG(attId=&quot;405&quot;)}{IMG}

If the package requires a dependency, which is not installed, you will get an error message :

{IMG(attId=&quot;406&quot;)}{IMG}

{IMG(attId=&quot;407&quot;)}{IMG}

When the plugin will be installed, you will get a notification :

{IMG(attId=&quot;408&quot;)}{IMG}

The plugin is now displayed in the installed list :

{IMG(attId=&quot;409&quot;)}{IMG}

!!!!Enable and configure a plugin
You need now to enable the plugin. If you don't do it, the plugin won't be available in the plugin list of the left menu. just click on the __Enable__ button :

{IMG(attId=&quot;410&quot;)}{IMG}

You will get a notification when the plugin is enabled :

{IMG(attId=&quot;411&quot;)}{IMG}

And, the __Enable__ button is replaced by both __Disable__ and __Configure__ buttons :

{IMG(attId=&quot;412&quot;)}{IMG}

You can now ((Plugins_installation_configuration|configure your plugin)) 

!!!!Uninstall a plugin
To uninstall a plugin, you first have to : 
# stop it
# disable it

!!!External members
External members management is the same as plugins except that you don't need to enable or configure an external member.

!!Multi hosts installation
In a multi host installation, you will see all the hosts in the left menu. 
When clicking on a host, you will only be able to manage plugins : the cache is managed on the main host and external members packages can only be installed on the main host.
