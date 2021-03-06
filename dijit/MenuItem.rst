.. _dijit/MenuItem:

dijit.MenuItem
==============

.. contents::
    :depth: 2

:Status:
:Version:
:Authors:

These are the line items in a Menu Widget. The display for the MenuItem consists of 3 columns namely Label, Icon and the Accelerator key. Although Menu can display accelerator keys there is no infrastructure currently to actually catch and execute these accelerators. The developer is responsible for the key event handler to support this.

A programmatically created MenuItem
-----------------------------------

.. code-example ::

  .. js ::

    <script type="text/javascript">
    dojo.require("dijit.MenuBar");
    dojo.require("dijit.MenuItem");
    var pMenuBar;
    function fClickOne() {alert("You clicked on Menu Item #1")};
    function fClickTwo() {alert("You clicked on Menu Item #2")};
    dojo.addOnLoad(function(){
    ExampleMenu = new dijit.Menu({id:"SampleM"});
    ExampleMenu.addChild(new dijit.MenuItem({label:"Always Visible Menu", disabled:true}));
    ExampleMenu.addChild(new dijit.MenuItem({label:"Item #1", onClick:fClickOne,  accelKey:"Shift+O"}));
    ExampleMenu.addChild(new dijit.MenuItem({label:"Item #2", onClick:fClickTwo, disabled:true, accelKey:"Shift+T"}));
    ExampleMenu.placeAt("wrapper");
    ExampleMenu.startup();
    });
    </script>

  .. html ::

     <div id="wrapper"></div>


Creation from markup is more simpler and structured.

.. code-example ::

  .. js ::

    <script type="text/javascript">
	dojo.require("dijit.MenuBar");
	dojo.require("dijit.PopupMenuBarItem");
	dojo.require("dijit.Menu");
	dojo.require("dijit.MenuItem");
    </script>

  .. html ::

	<div id="menubar" data-dojo-type="dijit.MenuBar">
	    <div data-dojo-type="dijit.PopupMenuBarItem" id="Item Menu">
	    <span>Items</span>
	        <div data-dojo-type="dijit.Menu" id="fileMenu">
	            <div data-dojo-type="dijit.MenuItem" data-dojo-props="onClick:function(){alert('Item 1')}">Item #1</div>
	            <div data-dojo-type="dijit.MenuItem" data-dojo-props="onClick:function(){alert('Item 2')}">Item #2</div>
	            <div data-dojo-type="dijit.MenuItem" data-dojo-props="onClick:function(){alert('Item 3')}, disabled:true">Item #3</div>
                </div>
            </div>
        </div>


Accessibility
=============

Keyboard
--------

==========================================    =================================================
Action                                        Key
==========================================    =================================================
Navigate menu items                        		Top and Down arrow keys
Activate a menu item                       		Spacebar or enter
==========================================    =================================================


Implementation Notes
====================

See :ref:`dijit.Menu <dijit/Menu>`.
