****************************
How to use domodroid Source
****************************

Dependancies
=============
Android SDK and API 8
Eclipse
Android plugin for Eclipse
HG mercurial plugin for Eclipse

How to import Domodroid in Eclipse project
===========================================

First you need to clone the repro on a folder out of your Eclipse workspace and get the Basilic2 branch (actualy the only availlaible branch)

.. code-block::
    hg clone http://hg.domogik.org/domodroid
    
    cd domodroid
    
    hg update Basilic2


Launch Eclipse

Go to: File -> Import -> Existing Android project

Select the folder where you get Domodroid source and check "copy to the workspace"

Use HG
=======

With the HG plugin you found on resource a sub menu Team, in this menu you find all that you can need to push or pull modification.


__It's possible that the HG plugin don't work fine__