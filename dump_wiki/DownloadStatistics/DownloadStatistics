{maketoc}
!Purpose
Check number of downloads in access.log* files

!Script
{CODE()}
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
    #echo &quot;==== $fic ====&quot;
    file $fic | grep &quot;gzip compressed data&quot; &gt; /dev/null

    # gz file
    if [[ $? -eq 0 ]] ; then
        #echo &quot;=&gt; GZ file&quot;
        gunzip $fic
        fic=$(echo $fic | sed &quot;s/\.gz$//&quot;)
        count=$(grep &quot;$1&quot; $fic | wc -l)
        ((total = count + total))
        #echo &quot;   C=$count&quot;
    else
        #echo &quot;=&gt; regular file&quot;
        count=$(grep &quot;$1&quot; $fic | wc -l)
        ((total = count + total))
        #echo &quot;   C=$count&quot;
    fi
    # delete file
    rm $fic

done
echo &quot;TOTAL = $total&quot;
{CODE}

!Usage
{CODE()}
tikiwiki:/var/log/apache2# /root/stats/stats.sh domogik-0.1.0-alpha1.tgz
TOTAL = 39
tikiwiki:/var/log/apache2# /root/stats/stats.sh domogik-0.1.0-alpha2.tgz
TOTAL = 240
{CODE}