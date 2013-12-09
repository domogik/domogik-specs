!Nightly builds for packages
{maketoc}

Nightly builds packages are packages generated from the &quot;default&quot; branch of the repository with the latest updates. The goal is to provide up to date experimental packages in order people to test the new plugins.

In this page, we explain how to set up a nightly build repository.

!!Prerequisites :
* Python 2.6 or above
* Sqlalchemy 

!!Create environment
Create a folder for nightly tools :
{CODE()}
# mkdir nightly-tools     
# cd nightly-tools/      
{CODE}

Create a /var/lock/domogik directory :
{code()}
# mkdir /var/lock/domogik
{code}

Create a local copy of the Domogik repository :
{CODE()}
# hg clone http://hg.domogik.org/domogik/
or
# hg clone /home/domogik/domogik/
{CODE}
This creates a nightly-tools/domogik folder. __Don't use this repository for anything else :__ it will be automatically updated.

Add domogik package to the python configuration :
{CODE()}
# echo &quot;/root/nightly-tools/domogik/src&quot; &gt; /usr/local/lib/python2.5/dist-packages/domogik.pth     
{CODE}

Create a folder for logs : 
{CODE()}
mkdir ~/nightly-tools/log
{CODE}

Create a basic configuration file : 
{CODE()}
# mkdir /etc/domogik
# echo &quot;
[domogik]                                                                       
log_dir_path = /root/nightly-tools/log/                                         
log_level = debug                                                              
src_prefix = /root/nightly-tools/domogik/src/
                                                                                
[database]                                                                      
db_prefix = foo

[rest]
rest_server_ip = 127.0.0.1
rest_server_port = 666        
&quot; &gt;  /etc/domogik/domogik.cfg
{CODE}

!!Create script nightly.sh
{CODE()}
#!/bin/bash

### Params
DATE=$(date &quot;+%Y-%m-%d %H:%M&quot;)
VERSION=&quot;.dev&quot;$(date &quot;+%Y%m%d&quot;)
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
    wget --post-file=$fic &quot;$REPO_URL/version/send?qqfile=$(basename $fic)&amp;deploy=true&amp;repository=nightly&quot;
done

{CODE}   

!!Set up crontab
Edit crontab :
{CODE()}
# crontab -e
{CODE}

Add this line :
{CODE()}
0 4 * * * /root/nightly-tools/nightly.sh &gt; /root/nightly-tools/log/last-build.log
{CODE}