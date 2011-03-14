#format dojo_rst

dojox.mobile.IconItem
=====================

:Status: Draft
:Version: 1.0
:Authors: Yoshiroh Kamiyama
:Developers: Yoshiroh Kamiyama
:Available: since V1.5

.. contents::
    :depth: 2

IconItem represents an item that has an application component and its icon image. You can tap the icon to open the corresponding application component. You can also use the icon to move to a different view by specifying either of the moveTo, href or url parameters.

======================
Constructor Parameters
======================

+--------------+----------+---------+-----------------------------------------------------------------------------------------------------------+
|Parameter     |Type      |Default  |Description                                                                                                |
+--------------+----------+---------+-----------------------------------------------------------------------------------------------------------+
|transition    |String    |slide    |A type of animated transition effect. "slide", "fade", "flip", or "none".                                  |
+--------------+----------+---------+-----------------------------------------------------------------------------------------------------------+
|transitionDir |Number    |1        |The transition direction. If 1, transition forward. If -1, transition backward. For example, the slide     |
|              |          |         |transition slides the view from right to left when dir == 1, and from left to right when dir == -1.        |
+--------------+----------+---------+-----------------------------------------------------------------------------------------------------------+
|icon          |String    |         |The icon path for the item. If icon is not specified, the iconBase parameter of the parent widget is used. |
+--------------+----------+---------+-----------------------------------------------------------------------------------------------------------+
|iconPos       |String    |         |The position of an aggregated icon. IconPos is comma separated values like top,left,width,height           |
|              |          |         |(ex. "0,0,29,29"). If iconPos is not specified, the iconPos parameter of the parent widget is used.        |
+--------------+----------+---------+-----------------------------------------------------------------------------------------------------------+
|moveTo        |String    |         |The id of the transition destination view which resides in the current page. If you add the hash sign ('#')|
|              |          |         |before the id, the view transition updates the hash in the browser URL so that the user can bookmark the   |
|              |          |         |destination view. The user can also use the browser's back/forward button to navigate through the views in |
|              |          |         |the browser history.                                                                                       |
+--------------+----------+---------+-----------------------------------------------------------------------------------------------------------+
|href          |String    |         |A URL of another web page to go to.                                                                        |
+--------------+----------+---------+-----------------------------------------------------------------------------------------------------------+
|hrefTarget    |String    |         |A target that specifies where to open a page specified by href. The value will be passed to the 2nd        |
|              |          |         |argument of window.open().                                                                                 |
+--------------+----------+---------+-----------------------------------------------------------------------------------------------------------+
|url           |String    |         |A URL of an html fragment page or JSON data that represents a new view content (See examples below). The   |
|              |          |         |view content is loaded with XHR and inserted in the current page. Then a view transition occurs to the     |
|              |          |         |newly created view. The view is cached so that subsequent requests would not load the content again.       |
+--------------+----------+---------+-----------------------------------------------------------------------------------------------------------+
|callback      |Function  |         |A callback function that is called when the transition has been finished. A function reference, or name of |
|              |          |         |a function in context.                                                                                     |
+--------------+----------+---------+-----------------------------------------------------------------------------------------------------------+
|sync          |Boolean   |true     |If true, XHR for the view content specified with the url parameter is performed synchronously. If false, it|
|              |          |         |is done asynchronously and the progress indicator is displayed while loading the content. This parameter is|
|              |          |         |effective only when the url parameter is used.                                                             |
+--------------+----------+---------+-----------------------------------------------------------------------------------------------------------+
|label         |String    |         |A title of the item, which is displayed below the icon.                                                    |
+--------------+----------+---------+-----------------------------------------------------------------------------------------------------------+
|lazy          |Boolean   |false    |If true, the content of the item, which includes dojo markup, is instantiated lazily. That is, only when   |
|              |          |         |the icon is opened by the user, the required modules are loaded and dojo widgets are instantiated.         |
+--------------+----------+---------+-----------------------------------------------------------------------------------------------------------+
|requires      |String    |         |Comma-separated required module names to be loaded. All the modules specified with dojoType and their      |
|              |          |         |depending modules are automatically loaded by the IconItem. If you need other extra modules to be loaded,  |
|              |          |         |use this parameter. If lazy is true, the specified required modules are loaded when the user opens the icon|
|              |          |         |for the first time.                                                                                        |
+--------------+----------+---------+-----------------------------------------------------------------------------------------------------------+
|timeout       |Number    |10       |Duration of highlight in seconds. The default value is 10.                                                 |
+--------------+----------+---------+-----------------------------------------------------------------------------------------------------------+

========
Examples
========

See examples of `dojox.mobile.IconContainer <dojox/mobile/IconContainer>`_.