**********************************
Specifications for the Repository
**********************************
.. toctree::



Terms
======
* package : any component packaged that could be stored in the repository. Example : a plugin, a widget, an icon pack, etc

Needs
======
What do we need to store in the repository ?
*********************************************
* plugins
* web ui widgets
* icons pack
* web ui themes

Domogik Releases
*****************
The plugin repository should offer packages for several Domogik releases :
* last version (old stable)
* actual (stable)
* unstable (development version)
* experimental (proof of concepts, etc)

Multiple repositories
**********************
We would like to allow multiple repositories for the following needs :
* make mirrors
* allow external people/companies to have their own repositories with their own plugins

With all these repositories, we would like to be able to :
* synchronize a repository with another one (mirror feature)
* use several repositories at the same time on one domogik client. Example : a developer will use official Domogik repository for common plugins and his own repository for his plugins
* indicate priorities in the list of used repositories (in case a package is available in 2 different repositories)

Technology
***********
* HTTP seems the easiest way to provide files

Dependencies
*************
Should we implement dependencies? Maybe it is too early for that :)

Logic
******
* downgrading a package should generate an explicit warning before installing (we should allow to downgrade for test/development purposes)
* when an xml file (share/domogik/*) already exists, the choice is given to the user


Repository
===========
Tree
*****
.. code-block::
    
    /<release>/<category>/<package name>.tgz   # package
                          <package name>.txt   # package description
    


Example : 
.. code-block::
    
    /stable/
        plugins/
            onewire.tgz
            onewire.txt
            cidmodem.tgz
            cidmodem.txt
            ...
        web-ui-widgets/
            dmg_1x1_basicActuatorBinary.tgz
            dmg_1x1_basicActuatorBinary.txt
            dmg_1x1_basicSensorNumber.tgz
            dmg_1x1_basicSensorNumber.txt
            ...
        ...
    /dev/
        plugins/   
            xbmc.tgz
            xbmc.txt
        web-ui-widgets/
            dmg_4x4_xbmcPlaylist.tgz
            dmg_4x4_xbmcPlaylist.txt
    


Package description file
*************************
Example : 
.. code-block::
    
    plugin_type = plugin        # plugin, web-ui-widget, etc
    plugin_name = onewire
    plugin_version = 0.1
    plugin_longname = Onewire support
    plugin_description = Bla bla bla \
    bli bli bli \
    blo blo blo
    


Package file
*************
!!!!Tree
The structure is the same than in the sources. Example for a type ''plugin'' :
.. code-block::
    
    share/              
        domogik/
            plugins/
                myplugin.xml
            stats/
                myplugintechnology/
                    xpl.schema1.xml
                    xpl.schema2.xml
                    ...
            url2xpl/
                myplugintechnology/
                    command1.xml
                    command2.xml
                    ...
    domogik/
        xpl/
            bin/
                myplugin.py
            lib/
                mypluginlib1.py
                mypluginlib2.py
    


Client configuration files
***************************
!!!!/etc/domogik/sources.list
An update tool has to be developed to update local repository
Example :
.. code-block::
    
    # priority      url
    # (0..1000)     http(s)://<server>/<release>
    500             http://repo.domogik.org/stable
    100             http://repo.domogik.org/dev
    900             http://myownrepo.com/dev
    

Here, an example for a developper :
* first line : the official stable repository
* second line : the official development repository
* third line : the developper repository 

Repository configuration files
*******************************
A tool (launched with crontab) has to be developed to manage a repository sync.
Example :
.. code-block::
    
    [old-stable]
    sync = disabled
    [stable]
    sync = enabled
    master = http://repo.domogik.org/stable
    [dev]
    sync = enabled
    master = http://repo.domogik.org/dev
    


Packager tools
===============
Creator
********
Parameters :
* hg version
* plugin name


Installer
**********
Features :
* update local repository
* upgrade packages
* search
* show details
* install

UI interaction
===============
At the end, it would be nice to allow the web UI to be able to install packages and update them.

Roadmap
========
Release 1
**********
* Create package creator
* Create package installer

Release 2
**********
* Create first repository
* Set configuration files format
* Use only one repository
* Create update tool
* Create search/show tool
* Create install tool
* Create upgrade tool

Release 3
**********
* Create synchronisation tool
* Allow several repositories