!The web interface model
This page is a draft helping us to create the domogik web interface.

!!General overview

!!Technical overview 
All the semantic and content is coded in XHTML 1.0 strict.
!! Design 
The design is separated from the content, using external CSS files.
To improve the user experience, we use the [http://jquery.com/|JQuery library] to add animations, effects and improved controls (graceful degradation).

__Interesting links to look at :__

* Designing icons :
** [http://icones.pro|icones pro]

* Drawing nice charts :
** [http://solutoire.com/flotr/|flotr] (require prototype.js framework)
** [http://www.jscharts.com/|jscharts] (free but not open-source)
** [http://code.google.com/p/flot|flot] (some bugs, lot of open bugs, pretty few dev/commits)
** [http://g.raphaeljs.com/|gRaphaÃ«l]
** [http://www.humblesoftware.com/finance/index|HumbleFinance] (use flotr)
** [http://omnipotent.net/jquery.sparkline/|jQuery Sparklines]
** [http://www.deensoft.com/lab/protochart/linechart.php|Protochart] (require prototype.js framework)
** [http://highcharts.com/|Highcharts] (by-nc, not gpl compatible !)
** [http://www.liquidx.net/plotkit/|PlotKit] (require Mochikit)
** [http://www.filamentgroup.com/lab/update_to_jquery_visualize_accessible_charts_with_html5_from_designing_with/|jQuery Visualize] (Accessible)
** [http://www.simile-widgets.org/timeline/|Timeline]
** [http://www.jqplot.com|jQplot] (gpl2, only one dev, looot of open bugs (110+) but also very active dev, many commits a day)
* Images :
** [http://www.lokeshdhakar.com/projects/lightbox2|lightbox2 for image management]
** [http://imageflow.finnrudolph.de/|nice slide effects for images]
* Scenarios:
** [http://www.simile-widgets.org/timeline/|Timeline]
** [http://neyric.github.com/wireit/|Wiring]
* Medias (coverflow):
** [http://www.simile-widgets.org/runway/|Runway] 
* Managing Lists
** [http://razorjack.net/quicksand/]
* Animated icons (for v0.2.0)
** [http://www.conforama.fr/webapp/wcs/stores/servlet/AmbianceView?langId=-2&amp;storeId=10001&amp;catalogId=10051]
* Color picker
** [http://acko.net/dev/farbtastic|farbtastic (GPL)]

!!!Accessibility 
The interface has dynamic content and advanced user interface controls developed with Ajax
So, to make this web application more accessible to people with disabilities, we are following the [http://www.w3.org/TR/WCAG/|Web Content Accessibility Guidelines] (WCAG) 2.0.
and using ARIA attributes ([http://www.w3.org/TR/wai-aria|Accessible Rich Internet Applications] (WAI-ARIA) 1.0) 
in order to provide more semantics to Assistive Technologies.

!!!Notes
* It was decided that CSS3 instructions can be used to create the design more easily.

!!!Color codes 
Here are the main colors used with the web interface:
 Gradient from !#000000 to !#403E3F::
  {HTML()}
&lt;div style=&quot;display:inline-block;height:1em; width:5em; background-color:#000000&quot;&gt;&lt;/div&gt;
&lt;div style=&quot;display:inline-block;height:1em; width:5em; background-color:#403E3F&quot;&gt;&lt;/div&gt;
{HTML}
 Gradient from !#534F45 to !#625E53::
  {HTML()}
&lt;div style=&quot;display:inline-block;height:1em; width:5em; background-color:#534F45&quot;&gt;&lt;/div&gt;
&lt;div style=&quot;display:inline-block;height:1em; width:5em; background-color:#625E53&quot;&gt;&lt;/div&gt;
{HTML}
 Gradient from !#BDCB2F to !#9BB528::
  {HTML()}
&lt;div style=&quot;display:inline-block;height:1em; width:5em; background-color:#BDCB2F&quot;&gt;&lt;/div&gt;
&lt;div style=&quot;display:inline-block;height:1em; width:5em; background-color:#9BB528&quot;&gt;&lt;/div&gt;
{HTML}
 Border !#B9C248::
  {HTML()}
&lt;div style=&quot;display:inline-block;height:1em; width:5em; background-color:#B9C248&quot;&gt;&lt;/div&gt;
{HTML}
 Gradient from !#908D6F to !#D2CDBC::
  {HTML()}
&lt;div style=&quot;display:inline-block;height:1em; width:5em; background-color:#908D6F&quot;&gt;&lt;/div&gt;
&lt;div style=&quot;display:inline-block;height:1em; width:5em; background-color:#D2CDBC&quot;&gt;&lt;/div&gt;
{HTML}
 Border !#979387::
  {HTML()}
&lt;div style=&quot;display:inline-block;height:1em; width:5em; background-color:#979387&quot;&gt;&lt;/div&gt;
{HTML}
 Background !#cccccc::
  {HTML()}
&lt;div style=&quot;display:inline-block;height:1em; width:5em; background-color:#cccccc&quot;&gt;&lt;/div&gt;
{HTML}
 Background !#eeeeee::
  {HTML()}
&lt;div style=&quot;display:inline-block;height:1em; width:5em; background-color:#eeeeee; border:1px solid#cccccc&quot;&gt;&lt;/div&gt;
{HTML}