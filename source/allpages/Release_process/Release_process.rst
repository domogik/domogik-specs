****************
Release process
****************

.. toctree::



Terms
======

* version : 0.1.0, 0.2.0, 0.2.1, ...
* release : 0.2.0 alpha1, 0.2.0 alpha2, 0.2.0 beta1

FAQ
====

Where do we do developments ?
******************************

New developments (except for plugins/external members) must be done in dedicated branches. When a development is ready/tested it can be merged in the "default" branch.

Where do we do bugfixes ?
**************************

Bugfixes are done in "default" branch. If needed, bugfixes will be merged in the appropriate branches (releases or developments).

What is the purpose of the default branch ?
********************************************

The default branch is the "version+1". It should be kept as stable as possible in order not to block plugins developpers. Only these tasks may be done on this branch :
* plugins development 
* bugfixes
* merge from development branches (for finished/tested developments only!!)

When do we create a branch ?
*****************************

We create a branch for the version ("0.1", "0.2") when the first alpha/beta is released. In this branch, we will tag all the releases ("0.2.0 alpha1", "0.2.0 alpha2", ...)
Merging rules
* All fixes are done on "default" branch
* A fix needed for another branch must be merged to this branch from default

Lifecycle of a version
=======================

A Domogik version follows the several steps : 
* specifications
* development
* tests and fixes
** tests
** alpha1
** tests
** alpha2
** ...
** tests
** beta1
** ...
** final release
* delivery to public

We are describing here an overview of what has to be done in the version process. Please see ((ReleaseProcess|#Detail_of_the_operations|the detail of the operations)) at the bottom of this page.

Alpha versions
***************

Alpha are versions where all main development has been done. There may be some bugs or some partial features.

!!!!Generate the first alpha of the release 0.2.0
* Create a branch named 0.2 (not 0.2.0!!!) from the branch default
* Create a tag 0.2.0-alpha1 on this new branch
* Create a .tar.gz package tagged as "0.2.0-alpha1"
* Put the package on the ((Download)) page in __Test releases__ chapter
* Create the version 0.2.0-alpha1 version in the tracker
* Start the test campaign

!!!!Generate the others alpha
* After all bugs on the previous alpha has been fixed, create a tag 0.2.0-alpha2 on the 0.2 branch
* Create a .tar.gz package tagged as "0.2.0-alpha2"
* ...

!!!!Report/fix a bug/ticket
* In the tracker / administration / customized fields / Version, in the list add the version that will be delivered (so that future bugs can be put for this version).
* Bugs should be reported in the dedicated version.
* Bugs have to be fixed in the 0.2 branch.
* At the end of the version, all fixes must be merged on the default branch

Beta and candidate (RC) versions
*********************************

A beta version is a version where all developments are finished and all features should be functionnal.
A candidate version is a version which has been tested and seems to be a good candidate for the final version. This version's goal is to check there is no more bugs.

!!!!Generate the beta/Candidate version
* After all bugs on the previous version has been fixed, create a tag 0.2.0-beta2/rc3 on the 0.2 branch
* Create a .tar.gz package tagged as "0.2.0-beta2/rc3"
* Put the package on the ((Download)) page in __Test releases__ chapter
* Create the version 0.2.0-beta2/rc3 version in the tracker
* Start the test campaign

!!!!Report/fix a bug/ticket
* In the tracker / administration / customized fields / Version, in the list add the version that will be delivered (so that future bugs can be put for this version).
* Bugs should be reported in the dedicated version.
* Bugs have to be fixed in the "default" branch and have to be merged in the 0.2 branch.

Final release
**************

The final release for public usage.

!!!!Generate the version
* In the tracker / administration / customized fields / Version, in the list add the version that will be delivered (so that future bugs can be put for this version).
* After all bugs on the last candidate version has been fixed, create a tag 0.2.0 (yes, 0.2.0 !!) on the 0.2 branch
* Create a .tar.gz package tagged as "0.2.0"
* Put the package on the ((Download)) page in __Domogik Core__ chapter
* Communicate

About 0.2.1, 0.2.2
*******************

These versions will be about minor enhancements or fixes.

!!!!Generate the version
* Make the fixes/enhancements
* Test them
* Create a tag 0.2.1
* Create a .tar.gz package tagged as "0.2.1"
* Put the package on the ((Download)) page in __Domogik Core__ chapter
* Communicate

How to do the different actions
********************************

!!!!Make sure the code is up to date
* Check that ''~np~src/domogik/common/__init__.py~/np~'' contains the current versions (database and application).
* Check that ''install/upgrade_scripts.py'' contains all scripts to upgrade from previous versions to the current one.

!!!!Create a branch from another one
''For more information about branches, see ((MercurialBranches|this page))''.
First, go into the __source__ branch (the branch from which you want to create the new branch) :
.. code-block:: json


    
    $ hg update <branch name>
    


Then create the new branch and commit. Example :
.. code-block:: json


    
    $ hg branch 0.1.0.alpha1                                  
    marked working directory as branch 0.1.0.alpha1   
    

Now, __complete the CHANGELOG file__ with data that will be present in the mail announce of the release.

And commit the new branch with its changelog : 
.. code-block:: json


    
    $ hg commit -m "Create branch 0.1.0.alpha1"      
    


For the next push action, you will need to use the "-f" option because of the newly created branch :
.. code-block:: json


    
    $ hg push -f # (or hg push --new-branch ?)
    


!!!!Create .tar.gz package
Following operations have to be done in the appropriate branch :

!!!!!Adapt package.sh file for release
* check README file is OK for installation instructions
* adapt exclusion patterns with uneccessary folders/files and things still in dev

!!!!!Launch package.sh

This script will :
* set the log level to ''info'' in domogik.cfg sample file
* set the version in setup.py
* remove choice for ''develop'' mode in install.sh
* create a ''.tgz'' file in your ''/tmp'' directory

Launch the script, and get the .tgz file.

Example 
.. code-block:: json


    
    $ ./package.sh tip 0.2.0-alpha1
    Generate package...
    Package successfully created : /tmp/domogik-temp.tgz
    Package extracted in post processing path : /tmp/domogik-post-12089
    Install.sh updated : force install mode
    domogik.cfg updated : force info log level
    setup.py, release : release number updated
    Final package generated : /tmp/domogik-0.2.0-alpha1.tgz
    


This will create a package for the tip revision (the last in branch). Release is set to 0.2.0-alpha1. 
You can use ./package.sh 0f090a8a6a3b 0.2.0-alpha1" to create a package for a specific revision (0f090a8a6a3b here).

Commit updates made to __package.sh__ :
.. code-block:: json


    
    $ hg commit -m "Package.sh for 0.2.0-alpha1"       
    


!!!!Test campaign
!!!!!Prepare test campaign
Create a dedicated milestone in Trac. Example : 0.1.0 - alpha 1 (test campaign) for bug reports

!!!!Test campaign
((Test_campaigns|More information here))

!!!!!Important tests
They can be different between releases. Basically they are :
* installation tests
* main organization tests (house, areas, rooms creation)
* main plugins tests (list, start, stop, configure)
* main devices tests (create, affect a feature to a place, check that actuators and sensors work fine)
* tests about bug fixed on last release

!!!!Cherrypicking

Cherrypicking is (here) the process that allows you to copy the modifications made from the 'default' branch to a specific branch.

All the bug fixing as to be made in the 'default' branch.

((Use_mercurial|#Cherrypicking|See here how to process))