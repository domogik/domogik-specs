!DomoWeb Widgets
||__Created:__|20/03/2012
__Creator:__|Ferllings
__Reviewers:__|
__Status:__|{GAUGE(value=&gt;90, max=&gt;100, label=&gt;''draft'', perc=&gt;true, labelsize=&gt;50, height=&gt;20, color=&gt;green, bgcolor=&gt;#EEEEEE)}{GAUGE}
__Target:__|0.2.2 (domoweb)
__References:__|((Packages_info_json|info.json file))||

!!Structure
* Each widget id should respect a naming convention: 'creator_size_shortDescription'.
** creator: The creator name (letter/number only, no space or punctuation)
** size: the widget size with the following format: width'x'height
** short description (letter/number only, no space or punctuation) 

^(ex. dmg_1x1_BasicBooleanActuator)^

The widget root folder name should be identical to the widget id.
^/usr/share/domoweb/widgets/&lt; id &gt;/...^

!!!info.json
{CODE(caption=&quot;json description file&quot;)}
{
            json_version: 1,
            identity: {
                        type: 'dmg_widget',
                        id: 'dmg_1x1_test',
                        version: 0.1,
                        name: 'Basic test widget',
                        description: 'Description for Basic test..',
                        creator: 'Domogik',
                        creator_email: 'xx@xxx.fr',
                        ...
            },
            images: {
                        icon: 'icon.png',
                        banner: 'banner.png',
                        scrennshot: 'screenshot.png',
            },
            parameters: {
                        height: 1,
                        width: 1,
                        display_border: true,
            },
            features: [
                        {
                                    id: 'mafeature',
                                    type: 'sensor.boolean',
                                    filters: ['...', '...'],
                        },
                        {...},
            ],
            configs: [
                        {
                                    id: 'maconfig',
                                    type: '...',
                                    default: '0',
                        },
                        {...},
            ],
            css: ['style.css', '...'],
            js: ['main.js', '...'],
}
{CODE}

* version : ((Packages_info_json|see info.json page))
* type : the type id for the widget element is 'dmg_widget'.
* identity : ((Packages_info_json|see info.json page))
* images : ((Packages_info_json|see info.json page))
* parameters :
** height, width: widget size format (1 to 4)
** display_border (default: true) : Whether or not a border should be displayed around the widget.
* features :
** id : string to identify the feature in the widget options
** label : string to describe the parameter
** type: type of selectable features
** filters (optional) : filter the list on one of the item list. 
format : &lt;techno&gt;.&lt;device&gt;.&lt;feature&gt; (* can be used)
* configs :
** id : string to identify the config item in the widget options
** label : string to describe the parameter
** type : type of the config data
* css : list of css files included in the 'css/' folder
* js : list javascript files included in the 'js/' folder
!!!!config types with available options
http://wiki.domogik.org/Spec_field_types

!!!js/main.js
This file contains the widget main initialization functions.
{CODE(caption=&quot;Base structure&quot;)}(function($) {
    $.create_widget({
        _init: function() {
        },

        _statesHandler: function(states) {
        },
        
        _eventHandler: function(timestamp, value) {
        },
    });
})(jQuery);{CODE}

!!!!_init function
Used to initialize the widget
!!!!_statsHandler function
Callback function used when requesting stats.
!!!!_eventHandler function
Callback function used when receiving event.
!!!css/style.css
The widget css stylesheet file.
* Each rule should start with the widget id as class name (ex. .dmg_1x1_minimalSensorNumber') 

!!!template.py
The content of this file will be copied inside the widget &lt;div&gt; object:
For now only static HTML is allowed. Later we should be able to use django template tags.
{CODE(caption=&quot;Template&quot;)}
&lt;div id='widget_instance_1' class='widget dmg_1x1_minimalSensorNumber height_1 width_1 border'&gt;
... content of the template.py file ...
&lt;/div&gt;
{CODE}

!! Internal processing and data
{IMG(attId=&quot;395&quot;)}{IMG}
!!! Django Start
* The 'widgets' folder is parsed
* If the json version is supported:
** The widget is registered in the 'widget' table
** The css &amp; js assets are registered in 'widget_css' and 'widget_js' tables
!!! Placement in page
* A new instance is created (widget_instance), with a 'config' icon
* When 'config' is clicked, a panel is opened
** Some default options are displayed : 
*** name and subname (if null, nothing is displayed)
** The features and configs items (from the info.json file section) are displayed
* When the config panel is closed:
** The values are saved in widget_feature/widget_config tables
** The feature/page links are sent to RINOR via REST API, for compatibility with other UI
!!! Page load
For each widget instance (widget_instance)
* css &amp; js include tags are generated (widget_css widget_js), (no duplication)
* widget options are generated for widget call (widget, widget_feature, widget_config)
^{id: ..., features:[], configs:[]}^
* widget call is generated
^$('#widget_instance_1').dmg_1x1_minimalSensorNumber(options);^
* widget template is inserted