{maketoc}

!Purpose
This messages are used by REST for acting or requesting managers about packages. See ((REST_package|REST /package page)) for more detail.

!Xpl messages
!!List installed packages on an host
Notice : the request (xpl-cmnd) for getting the list of installed packages list is used on rest startup only. Manager sends updates when starting and everytime an install or uninstall action has run.

Command : 
{CODE()}
xpl-cmnd                                           
{                                                                               
...                                                                       
}                                                                               
domogik.package                                                                 
{                                                                               
command=installed-packages-list                                                
host=&lt;host or *&gt;   
}
{CODE}

Response : 
{CODE()}
xpl-trig                                           
{                                                                               
...                                                                       
}                                                                               
domogik.package                                                                 
{                                                                               
command=installed-packages-list                                                
host=&lt;host&gt;
fullname0=&lt;package fullname : type-name&gt;
name0=&lt;package name&gt;
type0=&lt;package type : plugin,...&gt;
version0=&lt;package version&gt;
enabled0=&lt;yes/no&gt;
fullname1=...
name1=...
type1=...
version1=...
enabled1=...
...
}                                                                               
{CODE}

Notice : the uuid is needed because several request are done in the same time by the user interface (and so by rest).

!!Get package dependencies for a package
Command : 
{CODE()}
xpl-cmnd                                           
{                                                                               
...                                                                       
}                                                                               
domogik.package                                                                 
{                                                                               
command=get-dependencies                                                 
host=&lt;host&gt;        
type=&lt;plugin, external, ..&gt;
id=&lt;package id&gt;
}
{CODE}

Response : 
{CODE()}
xpl-trig                                           
{                                                                               
...                                                                       
}                                                                               
domogik.package                                                                 
{                                                                               
command=get-dependencies                                                 
host=&lt;host&gt;        
type=&lt;plugin, external, ..&gt;
id=&lt;package id&gt;                                         
[error=&lt;error message&gt;]
[dep0-id=&lt;dependency id&gt;]
[dep0-type=&lt;dependency type : python, plugin, other, ...&gt;]
[dep1-id=...]
[dep1-type=...]
...
}                                                                               
{CODE}

!!Check package dependencies
Command : 
{CODE()}
xpl-cmnd                                           
{                                                                               
...                                                                       
}                                                                               
domogik.package                                                                 
{                                                                               
command=check-dependencies                                                 
host=&lt;host&gt;        
[dep0=&lt;dependency&gt;]
[dep1=...]
...                                               
}
{CODE}
''Dependency has python dependency format. Example : pySerial &gt;= 2.4''

Response : 
{CODE()}
xpl-trig                                           
{                                                                               
...                                                                       
}                                                                               
domogik.package                                                                 
{                                                                               
command=check-dependencies                                             
host=&lt;host&gt;                                           
[error=&lt;error message&gt;]
[dep0=&lt;dependency&gt;]
[dep0-installed=&lt;yes|no&gt;]
[dep0-release=&lt;installed release&gt;]
[dep0-candidate=&lt;release to install&gt;]
[dep0-cmd-line=&lt;command line to install dependency : &quot;sudo easy_install ....&quot;&gt;]
[dep1=...]
[dep1-installed=...]
[dep1-release=...]
[dep1-candidate=...]
[dep1-cmd-line=...]
...
}                                                                               
{CODE}
When an error is detected for a dependency, message can be incomplete (current and following dependencies are not listed in xpl message). Here are possible following errors : 
* Wrong version format for '&lt;dependency&gt;' : should be 'foo (...)'              
* No candidate to dependency '&lt;dependency name&gt;' installation found                 
* Irrational version for dependency &lt;dependency&gt;

!!Install a package    
A package is installed as two parts :
* the main host (the one with RINOR) part.
* the target host part.
If you have only one computer with Domogik, the two parts will be installed on the same host.

On main host, files needed by RINOR are installed (for plugins : xml files for url2xpl and stats). On target host, files needed on the host are installed (for plugins : python part of the plugin is installed there).

For all package's type you need to send the two xPL messages. For each message, concerned host's manager will know if it needs to install files or not.

!!!Xpl part (target host part)
This message should be sent first.

Command : 
{CODE()}
xpl-cmnd
{
}
domogik.package
{
command=install
host=&lt;target host&gt;
source=&lt;where we got the packet from. Actually only &quot;cache&quot; is handled&gt;
type=&lt;package type&gt;
id=&lt;package id&gt;
release=&lt;release number&gt;
part=xpl
}
{CODE}

Response : 
{CODE()}
xpl-trig
{
}
domogik.package
{
command=install
host=&lt;target host&gt;
error=&lt;small error message&gt;
source=&lt;where we got the packet from. Actually only &quot;cache&quot; is handled&gt;
type=&lt;package type&gt;
id=&lt;package id&gt;
release=&lt;release number&gt;
}
{CODE}

For a plugin, if it is already installed and in running state, you will obtain the following error message : &quot;Plugin '&lt;plugin name&gt;' is running. Stop it before installing plugin.&quot;

!!!Rinor part
This message should be sent only __after__ the previous (xpl part) give back its xpl-trig.

Command : 
{CODE()}
xpl-cmnd
{
}
domogik.package
{
command=install
host=&lt;target host&gt;
source=&lt;where we got the packet from. Actually only &quot;cache&quot; is handled&gt;
type=&lt;package type&gt;
id=&lt;package id&gt;
release=&lt;release number&gt;
part=rinor
}
{CODE}

Response : 
{CODE()}
xpl-trig
{
}
domogik.package
{
command=install
host=&lt;target host&gt;
error=&lt;small error message&gt;
source=&lt;where we got the packet from. Actually only &quot;cache&quot; is handled&gt;
type=&lt;package type&gt;
id=&lt;package id&gt;
release=&lt;release number&gt;
}
{CODE}

!!Uninstall a package    
A package is installed as two parts :
* the main host (the one with RINOR) part.
* the target host part.

When uninstalling, we actually (0.2.0) only delete the description xml file for type __plugin__ and __external__

Command : 
{CODE()}
xpl-cmnd
{
}
domogik.package
{
command=uninstall
host=&lt;target host&gt;
type=&lt;package type&gt;
id=&lt;package id&gt;
}
{CODE}

Response : 
{CODE()}
xpl-trig
{
}
domogik.package
{
command=uninstall
host=&lt;target host&gt;
error=&lt;small error message&gt;
type=&lt;package type&gt;
id=&lt;package id&gt;
}
{CODE}

For a plugin, if it is already installed and in running state, you will obtain the following error message : &quot;Plugin '&lt;plugin name&gt;' is running. Stop it before installing plugin.&quot;

