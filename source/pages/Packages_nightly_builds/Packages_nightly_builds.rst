****************************
Nightly builds for packages
****************************

.. toctree::



Nightly builds packages are packages generated from the "default" branch of the repository with the latest updates. The goal is to provide up to date experimental packages in order people to test the new plugins.

In this page, we explain how to set up a nightly build repository.

Prerequisites :
================

* Python 2.6 or above
* Sqlalchemy 

Create environment
===================

Create a folder for nightly tools :
.. code-block:: json


    
    # mkdir nightly-tools     
    # cd nightly-tools/      
    


Create a /var/lock/domogik directory :
{code()}
# mkdir /var/lock/domogik
{code}

Create a local copy of the Domogik repository :
.. code-block:: json


    
    # hg clone http://hg.domogik.org/domogik/
    or
    # hg clone /home/domogik/domogik/
    

This creates a nightly-tools/domogik folder. __Don't use this repository for anything else :__ it will be automatically updated.

Add domogik package to the python configuration :
.. code-block:: json


    
    # echo "/root/nightly-tools/domogik/src" > /usr/local/lib/python2.5/dist-packages/domogik.pth     
    


Create a folder for logs : 
.. code-block:: json


    
    mkdir ~/nightly-tools/log
    


Create a basic configuration file : 
.. code-block:: json


    
    # mkdir /etc/domogik
    # echo "
    [domogik]                                                                       
    log_dir_path = /root/nightly-tools/log/                                         
    log_level = debug                                                              
    src_prefix = /root/nightly-tools/domogik/src/
                                                                                    
    [database]                                                                      
    db_prefix = foo
    
    [rest]
    rest_server_ip = 127.0.0.1
    rest_server_port = 666        
    " >  /etc/domogik/domogik.cfg
    


Create script nightly.sh
=========================

.. code-block:: json


    
    #!/bin/bash
    
    ### Params
    DATE=$(date "+%Y-%m-%d %H:%M")
    VERSION=".dev"$(date "+%Y%m%d")
    REPO_URL=http://repo.domogik.org/
    TMP_DIR=/root/nightly-tools/tmp/
    SRC_DIR=/root/nightly-tools/domogik/
    LOG_DIR=/root/nightly-tools/log/
    
    
    ### Generate nightly packages
    
    mkdir -p $TMP_DIR
    rm -Rf $TMP_DIR/*
    
    cd $SRC_DIR
    hg revert --all
    hg pull
    hg update default
    
    cd $SRC_DIR/src/tools/packages/
    pwd
    ./create_all_nightly_packages.sh $TMP_DIR
    
    for fic in $TMP_DIR/*
      do
        echo $fic
        wget --post-file=$fic "$REPO_URL/version/send?qqfile=$(basename $fic)&amp;deploy=true&amp;repository=nightly"
    done
    
    
   

Set up crontab
===============

Edit crontab :
.. code-block:: json


    
    # crontab -e
    


Add this line :
.. code-block:: json


    
    0 4 * * * /root/nightly-tools/nightly.sh > /root/nightly-tools/log/last-build.log
    
