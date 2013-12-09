********************************************************************************************************
{IMG(src="http://code.google.com/p/domodroid/logo?cct=1319102596")}{IMG} Domodroid User Guide
********************************************************************************************************

Introduction
=============

Domodroid is a free Android user interface for Domogik under GNU/GPL v3 Licence. With Domodroid, users can control most of the devices supported by Domogik (PLCBus, X10, 1wire, Mjpeg Camera, WolPing, Yahoo Weather...).

Domodroid provides the following usages compatible with many technologies:

.. code-block::wrap="1",ishtml="1"
    <table>
    <tr>
    <td>
    <p><b> - Switch </b></p>
    <p><b> - Dimmer </b></p>
    <p><b> - Trigger </b></p>
    <p><b> - Camera </b></p>
    <p><b> - Sensor </b></p>
    <p><b> - Binary </b></p>
    </td>
    <td><img src="http://i40.tinypic.com/mn16yo.png" border="0"></td>
    </tr>
    </table>


Features and Informations
==========================

Domodroid 1.0 provides plenty of features: 
General
********
*Multi display compatibility (Smartphone and Tablet)
*Easy configuration: Set your REST IP/URL access and synchronize
*Ability to set the widget's update timer from 10 to 300 secondes
*Power Management control keeping your screen on during the use of Domodroid
*Full icon pack supported

Widgets
********
*6 animated widgets
*Auto-Updated with an asynchrone threading system
*Data widget with 2d chart engine

Map system
***********
*Creation of the "Domodroid" directory at the root of the external storage directory (or internal for some specific devices), maps have to be put in this directory.
**Zoom: 2 fingers pinch
**Drag: 2 fingers move
**Change map: 3 fingers tap

*Multi-touch gesture (Zoom, Drag, Change Map) can be activated from the "Options" screen.
Gesture activation must be activated only on powerfull devices otherwise Domodroid will certainly crashes. Bitmap rezising might cause OutOfMemory exception so domodroid will automatically reduce bitmaps exceeding 800*800px by √2.

*Png and SVG format supported:
To display SVG images, Domodroid use a modified version of the library svg-Android          
( http://code.google.com/p/svg-android/ ).
This library supports a subset of the SVG Basic 1.1 specification. Typically, you can just load your vector artwork in Illustrator and then save it as a SVG file (selecting the SVG Basic 1.1 option when asked) and it will work fine. Inkscape does not have direct support for SVG Basic, but many drawings will just work when saved as SVG from Inkscape. These are the features of SVG Basic not supported:

**All text and font features.
**Raster images (bitmaps).
**Symbols, conditional processing.
**Patterns.
**Masks, filters and views.
**Interactivity, linking, scripting and animation.
**Arc commands in paths (work on this is in progress).

*Add widgets button allows users to place a widget on the map by choosing an item from the feature list and touching the map to place the widget.

*Remove widgets button allows users to remove the widget from the map

{IMG(src="http://i39.tinypic.com/swy611.png")}{IMG}

Camera
*******
* Mjpeg Stream supported
* Framerate counter

To use the camera streaming feature, the Camera plugin has to be installed in Domogik. If none of your camera stream Mjpeg datas, you can use Zoneminder which a free video camera security application that encode many kind of video stream format to mjpeg stream.

{IMG(src="http://i51.tinypic.com/5v6paa.png")}{IMG}

Apps and Sources
=================
Domodroid is available on the Android Market and also on the code.google website which also allows you to download the last available sources
http://code.google.com/p/domodroid/

Contact
========
pierre.laine2@gmail.com


**************
Domodroid Dev
**************

Domodroid specification
========================
((Spec_Domodroid|Here))
Domodroid how to use source code
=================================
((Domodroid_Src|Here))
