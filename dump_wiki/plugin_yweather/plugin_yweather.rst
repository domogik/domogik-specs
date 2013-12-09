.. toctree::



********
Purpose
********
This plugin get weather informations from Yahoo Weather online service.

__Warning : this plugin is not fully developped yet. Ticket #586 need to be processed before previsionnal data could be stored in database__

***************
Known features
***************
* http://trac.domogik.org/domogik/ticket/773

*********************
Plugin configuration
*********************
Enabling plugin
================
You can enable plugin by using :
.. code-block::
    
    dmgenplug yweather
    


Now, restart Domogik manager (using root / sudo) :
.. code-block::
    
    /etc/init.d/domogik restart manager
    

Configuration
==============
In Domogik administration, go to yweather configuration page.

en-current
***********
Enable getting current weather data from Yahoo Weather. Il you have a local weather station, you could set this option to False and use local weather station plugin to get current data.
Default : True

en-prev
********
Enable getting previsionnal weather data from Yahoo Weather.
Default : True

unit
*****
Temperature unit
* c : Celcius
* f : Farenheit

city-1
*******
City code for the first city you want to get data about. To get city code :
# Go to http://weather.yahoo.com/
# Search for your city
# You are sent to an url like this : http://weather.yahoo.com/france/pays-de-la-loire/nantes-613858/
# The number (here : 613858) is your city code

device-1
*********
Device address for city-1. This address is set by you and is the address you should affect to a device when creating it. 
If you want to use Yahoo Weather for previsionnal and a local weather station for current data, you should set this address in the 2 plugins.

city-2
*******
City code for the second city you want to get data about.

device-2
*********
Device address for city-2.

Start plugin
=============
You can now start the plugin (start button).

Check plugin works
===================
||TODO||

******************
Creating a device
******************
 
Before, you have to execute :
from src directory
src/tools/packages/insert_data.py  /usr/local/share/domogik/plugins/yweather.xml

In administration, go to __Organization > Devices__ page. Create a new device like this :
||TODO||

********
Helpers
********
''To get an introduction to helpers, you can read the ((Plugins_helpers|Helper documentation)). To use a helper, the plugin must be stopped.''

||TODO||

*****************
Developper notes
*****************
~~#390:__Notice :__ this plugin is one of existing weather related plugins. To get rules about these plugins (in order them to be compatible), see ((Plugin_weather_recommendations| the weather plugin's recommendations)).~~

Useful links
=============
* http://developer.yahoo.com/weather/

RSS
====
Example URL for Nantes (Fr) :
* in Celsius : http://weather.yahooapis.com/forecastrss?w=613858&amp;u=c
* in Fahrenheit : http://weather.yahooapis.com/forecastrss?w=613858&amp;u=f

Xml Strucure : 
================

.. code-block:: xml
    
    <?xml version="1.0" encoding="UTF-8" standalone="yes" ?>
    <rss version="2.0" xmlns:yweather="http://xml.weather.yahoo.com/ns/rss/1.0" xmlns:geo="http://www.w3.org/2003/01/geo/wgs84_pos#">
          <channel>
                <title>Yahoo! Weather - Nantes, FR</title>
                <link>http://us.rd.yahoo.com/dailynews/rss/weather/Nantes__FR/*http://weather.yahoo.com/forecast/FRXX0072_c.html</link>
                <description>Yahoo! Weather for Nantes, FR</description>
                <language>en-us</language>
                <lastBuildDate>Mon, 08 Nov 2010 11:00 am CET</lastBuildDate>
                <ttl>60</ttl>
                <yweather:location city="Nantes" region="" country="France"/>
                <yweather:units temperature="C" distance="km" pressure="mb" speed="km/h"/>
                <yweather:wind chill="12" direction="300" speed="27.36" />
                <yweather:atmosphere humidity="72" visibility="9.99" pressure="948.19" rising="0" />
                <yweather:astronomy sunrise="7:59 am" sunset="5:40 pm"/>
                <image>
                      <title>Yahoo! Weather</title>
                      <width>142</width>
                      <height>18</height>
                      <link>http://weather.yahoo.com</link>
                      <url>http://l.yimg.com/a/i/brand/purplelogo//uh/us/news-wea.gif</url>
                </image>
                <item>
                      <title>Conditions for Nantes, FR at 11:00 am CET</title>
                      <geo:lat>47.22</geo:lat>
                      <geo:long>-1.55</geo:long>
                      <link>http://us.rd.yahoo.com/dailynews/rss/weather/Nantes__FR/*http://weather.yahoo.com/forecast/FRXX0072_c.html</link>
                      <pubDate>Mon, 08 Nov 2010 11:00 am CET</pubDate>
                      <yweather:condition text="Partly Cloudy" code="30" temp="12" date="Mon, 08 Nov 2010 11:00 am CET" />
                      <description>
                            <![CDATA[<img src="http://l.yimg.com/a/i/us/we/52/30.gif"/><br /><b>Current Conditions:</b><br />Partly Cloudy, 12 C<BR /><BR /><b>Forecast:</b><BR />Mon - Heavy Rain. High: 12 Low: 7<br />Tue - AM Light Rain. High: 11 Low: 7<br /><br /><a href="http://us.rd.yahoo.com/dailynews/rss/weather/Nantes__FR/*http://weather.yahoo.com/forecast/FRXX0072_c.html">Full Forecast at Yahoo! Weather</a><BR/><BR/>(provided by <a href="http://www.weather.com" >The Weather Channel</a>)<br/>]]>
                            </description>
                      <yweather:forecast day="Mon" date="8 Nov 2010" low="7" high="12" text="Heavy Rain" code="40" />
                      <yweather:forecast day="Tue" date="9 Nov 2010" low="7" high="11" text="AM Light Rain" code="11" />
                      <guid isPermaLink="false">FRXX0072_2010_11_08_11_00_CET</guid>
                </item>
          </channel>
    </rss>
    <!-- api4.weather.ch1.yahoo.com compressed/chunked Mon Nov 8 02:31:00 PST 2010 -->
    


Data to get : 
* <yweather:location city="Nantes" region=""   country="France"/>
* <yweather:units temperature="F" distance="mi" pressure="in" speed="mph"/>
* <yweather:wind chill="75"   direction="250"   speed="12" />
* <yweather:atmosphere humidity="53"  visibility="6.21"  pressure="29.97"  rising="0" />
* <yweather:astronomy sunrise="6:22 am"   sunset="10:00 pm"/>
* <yweather:condition  text="Partly Cloudy"  code="30"  temp="75"  date="Mon, 12 Jul 2010 1:00 pm CEST" />
* <yweather:forecast day="Mon" date="12 Jul 2010" low="60" high="75" text="Mostly Cloudy" code="28" />
* <yweather:forecast day="Tue" date="13 Jul 2010" low="61" high="78" text="Partly Cloudy" code="30" />

Condition codes are described here : http://developer.yahoo.com/weather/#codes

xPl schema
===========
See ((Plugin_weather_recommendations|weather's plugins common page))

Data taken from Yahoo Weather
==============================
||TODO||