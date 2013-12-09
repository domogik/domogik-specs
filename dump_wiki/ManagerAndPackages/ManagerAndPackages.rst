.. toctree::



********
Purpose
********
This messages are used by REST for acting or requesting managers about packages. See ((REST_package|REST /package page)) for more detail.

*************
Xpl messages
*************
List installed packages on an host
===================================
Notice : the request (xpl-cmnd) for getting the list of installed packages list is used on rest startup only. Manager sends updates when starting and everytime an install or uninstall action has run.

Command : 
.. code-block::
    
    xpl-cmnd                                           
    {                                                                               
    ...                                                                       
    }                                                                               
    domogik.package                                                                 
    {                                                                               
    command=installed-packages-list                                                
    host=<host or *>   
    }
    


Response : 
.. code-block::
    
    xpl-trig                                           
    {                                                                               
    ...                                                                       
    }                                                                               
    domogik.package                                                                 
    {                                                                               
    command=installed-packages-list                                                
    host=<host>
    fullname0=<package fullname : type-name>
    name0=<package name>
    type0=<package type : plugin,...>
    version0=<package version>
    enabled0=<yes/no>
    fullname1=...
    name1=...
    type1=...
    version1=...
    enabled1=...
    ...
    }                                                                               
    


Notice : the uuid is needed because several request are done in the same time by the user interface (and so by rest).

Get package dependencies for a package
=======================================
Command : 
.. code-block::
    
    xpl-cmnd                                           
    {                                                                               
    ...                                                                       
    }                                                                               
    domogik.package                                                                 
    {                                                                               
    command=get-dependencies                                                 
    host=<host>        
    type=<plugin, external, ..>
    id=<package id>
    }
    


Response : 
.. code-block::
    
    xpl-trig                                           
    {                                                                               
    ...                                                                       
    }                                                                               
    domogik.package                                                                 
    {                                                                               
    command=get-dependencies                                                 
    host=<host>        
    type=<plugin, external, ..>
    id=<package id>                                         
    [error=<error message>]
    [dep0-id=<dependency id>]
    [dep0-type=<dependency type : python, plugin, other, ...>]
    [dep1-id=...]
    [dep1-type=...]
    ...
    }                                                                               
    


Check package dependencies
===========================
Command : 
.. code-block::
    
    xpl-cmnd                                           
    {                                                                               
    ...                                                                       
    }                                                                               
    domogik.package                                                                 
    {                                                                               
    command=check-dependencies                                                 
    host=<host>        
    [dep0=<dependency>]
    [dep1=...]
    ...                                               
    }
    

''Dependency has python dependency format. Example : pySerial >= 2.4''

Response : 
.. code-block::
    
    xpl-trig                                           
    {                                                                               
    ...                                                                       
    }                                                                               
    domogik.package                                                                 
    {                                                                               
    command=check-dependencies                                             
    host=<host>                                           
    [error=<error message>]
    [dep0=<dependency>]
    [dep0-installed=<yes|no>]
    [dep0-release=<installed release>]
    [dep0-candidate=<release to install>]
    [dep0-cmd-line=<command line to install dependency : "sudo easy_install ....">]
    [dep1=...]
    [dep1-installed=...]
    [dep1-release=...]
    [dep1-candidate=...]
    [dep1-cmd-line=...]
    ...
    }                                                                               
    

When an error is detected for a dependency, message can be incomplete (current and following dependencies are not listed in xpl message). Here are possible following errors : 
* Wrong version format for '<dependency>' : should be 'foo (...)'              
* No candidate to dependency '<dependency name>' installation found                 
* Irrational version for dependency <dependency>

Install a package    
======================
A package is installed as two parts :
* the main host (the one with RINOR) part.
* the target host part.
If you have only one computer with Domogik, the two parts will be installed on the same host.

On main host, files needed by RINOR are installed (for plugins : xml files for url2xpl and stats). On target host, files needed on the host are installed (for plugins : python part of the plugin is installed there).

For all package's type you need to send the two xPL messages. For each message, concerned host's manager will know if it needs to install files or not.

Xpl part (target host part)
****************************
This message should be sent first.

Command : 
.. code-block::
    
    xpl-cmnd
    {
    }
    domogik.package
    {
    command=install
    host=<target host>
    source=<where we got the packet from. Actually only "cache" is handled>
    type=<package type>
    id=<package id>
    release=<release number>
    part=xpl
    }
    


Response : 
.. code-block::
    
    xpl-trig
    {
    }
    domogik.package
    {
    command=install
    host=<target host>
    error=<small error message>
    source=<where we got the packet from. Actually only "cache" is handled>
    type=<package type>
    id=<package id>
    release=<release number>
    }
    


For a plugin, if it is already installed and in running state, you will obtain the following error message : "Plugin '<plugin name>' is running. Stop it before installing plugin."

Rinor part
***********
This message should be sent only __after__ the previous (xpl part) give back its xpl-trig.

Command : 
.. code-block::
    
    xpl-cmnd
    {
    }
    domogik.package
    {
    command=install
    host=<target host>
    source=<where we got the packet from. Actually only "cache" is handled>
    type=<package type>
    id=<package id>
    release=<release number>
    part=rinor
    }
    


Response : 
.. code-block::
    
    xpl-trig
    {
    }
    domogik.package
    {
    command=install
    host=<target host>
    error=<small error message>
    source=<where we got the packet from. Actually only "cache" is handled>
    type=<package type>
    id=<package id>
    release=<release number>
    }
    


Uninstall a package    
========================
A package is installed as two parts :
* the main host (the one with RINOR) part.
* the target host part.

When uninstalling, we actually (0.2.0) only delete the description xml file for type __plugin__ and __external__

Command : 
.. code-block::
    
    xpl-cmnd
    {
    }
    domogik.package
    {
    command=uninstall
    host=<target host>
    type=<package type>
    id=<package id>
    }
    


Response : 
.. code-block::
    
    xpl-trig
    {
    }
    domogik.package
    {
    command=uninstall
    host=<target host>
    error=<small error message>
    type=<package type>
    id=<package id>
    }
    


For a plugin, if it is already installed and in running state, you will obtain the following error message : "Plugin '<plugin name>' is running. Stop it before installing plugin."

