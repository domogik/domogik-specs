.. toctree::



****************
Plugin xpl_time
****************


This plugin documentation is now available on [http://docs.domogik.org/plugin/xpl\_time/dev/en/]


*****************
Developper notes
*****************

xPL schema
===========

The [DATETIME.BASIC schema|http://xplproject.org.uk/wiki/index.php?title=Schema_-_DATETIME.BASIC] is used by this plugin.

Example : 
.. code-block::


    
    xpl-trig     
    {        
    ...  
    }             
    datetime.basic       
    {         
    datetime=20110308115010  
    date=20110308  
    time=115010 
    format1=201103081150101 
    }  
    
   
* datetime : <yyyymmddhhmmss> 
* date : <yyyymmdd>
* time : <hhmmss>
* format1 : <yyyymmddhhmmss+weekday>        