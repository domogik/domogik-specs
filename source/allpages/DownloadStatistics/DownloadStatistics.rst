.. toctree::


********
Purpose
********

Check number of downloads in access.log* files

*******
Script
*******

.. code-block:: json


    
    #!/bin/sh
    
    FILE=$1
    DATA_FOLDER=/root/stats/data/
    APACHE_LOG_FOLDER=/var/log/apache2
    
    # prepare env for data
    rm -Rf $DATA_FOLDER/*
    mkdir -p $DATA_FOLDER
    
    # copy log files
    cp $APACHE_LOG_FOLDER/access.log* $DATA_FOLDER
    
    # for each file, count $FILE number of DL
    TOTAL=0
    for fic in $DATA_FOLDER/*
      do
        #echo "==== $fic ===="
        file $fic | grep "gzip compressed data" > /dev/null
    
        # gz file
        if [[ $? -eq 0 ]] ; then
            #echo "=> GZ file"
            gunzip $fic
            fic=$(echo $fic | sed "s/\.gz$//")
            count=$(grep "$1" $fic | wc -l)
            ((total = count + total))
            #echo "   C=$count"
        else
            #echo "=> regular file"
            count=$(grep "$1" $fic | wc -l)
            ((total = count + total))
            #echo "   C=$count"
        fi
        # delete file
        rm $fic
    
    done
    echo "TOTAL = $total"
    


******
Usage
******

.. code-block:: json


    
    tikiwiki:/var/log/apache2# /root/stats/stats.sh domogik-0.1.0-alpha1.tgz
    TOTAL = 39
    tikiwiki:/var/log/apache2# /root/stats/stats.sh domogik-0.1.0-alpha2.tgz
    TOTAL = 240
    
