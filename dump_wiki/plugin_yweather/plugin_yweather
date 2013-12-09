{maketoc}

!Purpose
This plugin get weather informations from Yahoo Weather online service.

__Warning : this plugin is not fully developped yet. Ticket #586 need to be processed before previsionnal data could be stored in database__

!Known features
* http://trac.domogik.org/domogik/ticket/773

!Plugin configuration
!!Enabling plugin
You can enable plugin by using :
{CODE()}
dmgenplug yweather
{CODE}

Now, restart Domogik manager (using root / sudo) :
{CODE()}
/etc/init.d/domogik restart manager
{CODE}
!!Configuration
In Domogik administration, go to yweather configuration page.

!!!en-current
Enable getting current weather data from Yahoo Weather. Il you have a local weather station, you could set this option to False and use local weather station plugin to get current data.
Default : True

!!!en-prev
Enable getting previsionnal weather data from Yahoo Weather.
Default : True

!!!unit
Temperature unit
* c : Celcius
* f : Farenheit

!!!city-1
City code for the first city you want to get data about. To get city code :
# Go to http://weather.yahoo.com/
# Search for your city
# You are sent to an url like this : http://weather.yahoo.com/france/pays-de-la-loire/nantes-613858/
# The number (here : 613858) is your city code

!!!device-1
Device address for city-1. This address is set by you and is the address you should affect to a device when creating it. 
If you want to use Yahoo Weather for previsionnal and a local weather station for current data, you should set this address in the 2 plugins.

!!!city-2
City code for the second city you want to get data about.

!!!device-2
Device address for city-2.

!!Start plugin
You can now start the plugin (start button).

!!Check plugin works
||TODO||

!Creating a device
 
Before, you have to execute :
from src directory
src/tools/packages/insert_data.py  /usr/local/share/domogik/plugins/yweather.xml

In administration, go to __Organization &gt; Devices__ page. Create a new device like this :
||TODO||

!Helpers
''To get an introduction to helpers, you can read the ((Plugins_helpers|Helper documentation)). To use a helper, the plugin must be stopped.''

||TODO||

!Developper notes
~~#390:__Notice :__ this plugin is one of existing weather related plugins. To get rules about these plugins (in order them to be compatible), see ((Plugin_weather_recommendations| the weather plugin's recommendations)).~~

!!Useful links
* http://developer.yahoo.com/weather/

!!RSS
Example URL for Nantes (Fr) :
* in Celsius : http://weather.yahooapis.com/forecastrss?w=613858&amp;u=c
* in Fahrenheit : http://weather.yahooapis.com/forecastrss?w=613858&amp;u=f

!!Xml Strucure : 

{CODE(colors=&quot;xml&quot;)}
&lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot; standalone=&quot;yes&quot; ?&gt;
&lt;rss version=&quot;2.0&quot; xmlns:yweather=&quot;http://xml.weather.yahoo.com/ns/rss/1.0&quot; xmlns:geo=&quot;http://www.w3.org/2003/01/geo/wgs84_pos#&quot;&gt;
      &lt;channel&gt;
            &lt;title&gt;Yahoo! Weather - Nantes, FR&lt;/title&gt;
            &lt;link&gt;http://us.rd.yahoo.com/dailynews/rss/weather/Nantes__FR/*http://weather.yahoo.com/forecast/FRXX0072_c.html&lt;/link&gt;
            &lt;description&gt;Yahoo! Weather for Nantes, FR&lt;/description&gt;
            &lt;language&gt;en-us&lt;/language&gt;
            &lt;lastBuildDate&gt;Mon, 08 Nov 2010 11:00 am CET&lt;/lastBuildDate&gt;
            &lt;ttl&gt;60&lt;/ttl&gt;
            &lt;yweather:location city=&quot;Nantes&quot; region=&quot;&quot; country=&quot;France&quot;/&gt;
            &lt;yweather:units temperature=&quot;C&quot; distance=&quot;km&quot; pressure=&quot;mb&quot; speed=&quot;km/h&quot;/&gt;
            &lt;yweather:wind chill=&quot;12&quot; direction=&quot;300&quot; speed=&quot;27.36&quot; /&gt;
            &lt;yweather:atmosphere humidity=&quot;72&quot; visibility=&quot;9.99&quot; pressure=&quot;948.19&quot; rising=&quot;0&quot; /&gt;
            &lt;yweather:astronomy sunrise=&quot;7:59 am&quot; sunset=&quot;5:40 pm&quot;/&gt;
            &lt;image&gt;
                  &lt;title&gt;Yahoo! Weather&lt;/title&gt;
                  &lt;width&gt;142&lt;/width&gt;
                  &lt;height&gt;18&lt;/height&gt;
                  &lt;link&gt;http://weather.yahoo.com&lt;/link&gt;
                  &lt;url&gt;http://l.yimg.com/a/i/brand/purplelogo//uh/us/news-wea.gif&lt;/url&gt;
            &lt;/image&gt;
            &lt;item&gt;
                  &lt;title&gt;Conditions for Nantes, FR at 11:00 am CET&lt;/title&gt;
                  &lt;geo:lat&gt;47.22&lt;/geo:lat&gt;
                  &lt;geo:long&gt;-1.55&lt;/geo:long&gt;
                  &lt;link&gt;http://us.rd.yahoo.com/dailynews/rss/weather/Nantes__FR/*http://weather.yahoo.com/forecast/FRXX0072_c.html&lt;/link&gt;
                  &lt;pubDate&gt;Mon, 08 Nov 2010 11:00 am CET&lt;/pubDate&gt;
                  &lt;yweather:condition text=&quot;Partly Cloudy&quot; code=&quot;30&quot; temp=&quot;12&quot; date=&quot;Mon, 08 Nov 2010 11:00 am CET&quot; /&gt;
                  &lt;description&gt;
                        &lt;![CDATA[&lt;img src=&quot;http://l.yimg.com/a/i/us/we/52/30.gif&quot;/&gt;&lt;br /&gt;&lt;b&gt;Current Conditions:&lt;/b&gt;&lt;br /&gt;Partly Cloudy, 12 C&lt;BR /&gt;&lt;BR /&gt;&lt;b&gt;Forecast:&lt;/b&gt;&lt;BR /&gt;Mon - Heavy Rain. High: 12 Low: 7&lt;br /&gt;Tue - AM Light Rain. High: 11 Low: 7&lt;br /&gt;&lt;br /&gt;&lt;a href=&quot;http://us.rd.yahoo.com/dailynews/rss/weather/Nantes__FR/*http://weather.yahoo.com/forecast/FRXX0072_c.html&quot;&gt;Full Forecast at Yahoo! Weather&lt;/a&gt;&lt;BR/&gt;&lt;BR/&gt;(provided by &lt;a href=&quot;http://www.weather.com&quot; &gt;The Weather Channel&lt;/a&gt;)&lt;br/&gt;]]&gt;
                        &lt;/description&gt;
                  &lt;yweather:forecast day=&quot;Mon&quot; date=&quot;8 Nov 2010&quot; low=&quot;7&quot; high=&quot;12&quot; text=&quot;Heavy Rain&quot; code=&quot;40&quot; /&gt;
                  &lt;yweather:forecast day=&quot;Tue&quot; date=&quot;9 Nov 2010&quot; low=&quot;7&quot; high=&quot;11&quot; text=&quot;AM Light Rain&quot; code=&quot;11&quot; /&gt;
                  &lt;guid isPermaLink=&quot;false&quot;&gt;FRXX0072_2010_11_08_11_00_CET&lt;/guid&gt;
            &lt;/item&gt;
      &lt;/channel&gt;
&lt;/rss&gt;
&lt;!-- api4.weather.ch1.yahoo.com compressed/chunked Mon Nov 8 02:31:00 PST 2010 --&gt;
{CODE}

Data to get : 
* &lt;yweather:location city=&quot;Nantes&quot; region=&quot;&quot;   country=&quot;France&quot;/&gt;
* &lt;yweather:units temperature=&quot;F&quot; distance=&quot;mi&quot; pressure=&quot;in&quot; speed=&quot;mph&quot;/&gt;
* &lt;yweather:wind chill=&quot;75&quot;   direction=&quot;250&quot;   speed=&quot;12&quot; /&gt;
* &lt;yweather:atmosphere humidity=&quot;53&quot;  visibility=&quot;6.21&quot;  pressure=&quot;29.97&quot;  rising=&quot;0&quot; /&gt;
* &lt;yweather:astronomy sunrise=&quot;6:22 am&quot;   sunset=&quot;10:00 pm&quot;/&gt;
* &lt;yweather:condition  text=&quot;Partly Cloudy&quot;  code=&quot;30&quot;  temp=&quot;75&quot;  date=&quot;Mon, 12 Jul 2010 1:00 pm CEST&quot; /&gt;
* &lt;yweather:forecast day=&quot;Mon&quot; date=&quot;12 Jul 2010&quot; low=&quot;60&quot; high=&quot;75&quot; text=&quot;Mostly Cloudy&quot; code=&quot;28&quot; /&gt;
* &lt;yweather:forecast day=&quot;Tue&quot; date=&quot;13 Jul 2010&quot; low=&quot;61&quot; high=&quot;78&quot; text=&quot;Partly Cloudy&quot; code=&quot;30&quot; /&gt;

Condition codes are described here : http://developer.yahoo.com/weather/#codes

!!xPl schema
See ((Plugin_weather_recommendations|weather's plugins common page))

!!Data taken from Yahoo Weather
||TODO||