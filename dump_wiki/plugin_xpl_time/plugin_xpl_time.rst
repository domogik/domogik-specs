{maketoc}

!Plugin xpl_time

This plugin documentation is now available on [http://docs.domogik.org/plugin/xpl_time/dev/en/]


!Developper notes
!!xPL schema
The [DATETIME.BASIC schema|http://xplproject.org.uk/wiki/index.php?title=Schema_-_DATETIME.BASIC] is used by this plugin.

Example : 
{CODE()}
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
{CODE}   
* datetime : &lt;yyyymmddhhmmss&gt; 
* date : &lt;yyyymmdd&gt;
* time : &lt;hhmmss&gt;
* format1 : &lt;yyyymmddhhmmss+weekday&gt;        