********************
Views of the web UI
********************

*Each view can be oriented top to bottom, or left to right
*Template system for pages??
* Several background choices: color, gradient, image, video, applet
** Image : transparency is adjustable
** Image : position is adjustable (horizontally, vertically)
** Applet : Flash applet only
** Applet : position is adjustable (horizontally, vertically)
** Applet : no possible action or button
** Applet : ~~#C00:Dedicated section to control the Flash Applet ??~~
** Applet : (eg. http://yowindow.com/weatherwidget.html)
** Video : (eg. webcam)
** Video : ~~#C00:Dedicated section to control the Video ??~~

Default view
=============

*Each page will have a default view (all size/orientation)
*All ((Web_ui_sections|sections)) are available for selection

If a section/widget is not compatible with the terminal size, a blank area will be displayed, with a message.

Specific view
==============

A specific view can be created for a specific criteria: display size range, orientation, or a registered terminal.

*Only the ((Web_ui_sections|sections)) that match the criteria are available for selection

Technical specifications
*************************

*Data preloading
The sections/widgets should be able to give data requirements to the view, and have those data ready to use on the page template.
*Plugin-able modules system
**Sections/Widgets registration, for loading only when displayed
**Portlets: http://pypi.python.org/pypi/django-portlets/
**Dynamic Template Loader: http://djangosnippets.org/snippets/851/
**Dynamic import from an installed app: http://djangosnippets.org/snippets/1413/
