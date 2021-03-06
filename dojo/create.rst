.. _dojo/create:

dojo.create
===========

:Available: since V1.3

.. contents::
   :depth: 2

A convenient DOM creation, manipulation and placement utility shorthand.


============
Introduction
============

dojo.create() is designed to simplify the frequently used sequence of DOM manipulation:

* create a node,
* set attributes on it,
* and place it in the DOM.

It can be used with existing nodes too, if you want to assign new attributes and place it afterwards.

To see this utility in context, read the :ref:`DOM Quick Start <quickstart/dom>` first.

Since Dojo 1.7, ``dojo.create`` is exposed via the ``create`` method of the ``dojo/dom-construct`` module.  An alias is kept in ``dojo/_base/html`` for backward-compatibility.

=====
Usage
=====

The function takes up to four arguments:

.. js ::

    // Dojo 1.7+ (AMD)
    require(["dojo/dom-construct"], function(domConstruct){
      domConstruct.create(tag, attrs, refNode, pos);
    };
    
    // Dojo < 1.7
    dojo.create(tag, attrs, refNode, pos);

Here is the definition of arguments:

=========  ===========  =======================================================
Parameter  Type         Description
=========  ===========  =======================================================
tag        String|Node  Can be a string or a DOM node. If it is a string, it
                        will be treated as a node tag name, which will be used
                        to create a new node.
                        When creating a node the owner document of ``refNode``
                        is used. If ``refNode`` is ``null`` or unspecified,
                        :ref:`dojo.doc <dojo/doc>` is used.
attrs      Object|null  A dictionary of attributes to be set on ``node``.
                        This parameter is passed to :ref:`dojo.attr <dojo/attr>`
                        unmodified after the node is created.
                        Can be ``null`` or undefined meaning
                        "don't set any attributes". You should always specify
                        it explicitly (as ``null``) if you want to specify
                        the rest of arguments.
refNode    String|null  A string (interpreted as an id of a DOM node) or
                        a DOM node. This parameter is passed to
                        :ref:`dojo.place <dojo/place>` unmodified after the node is
                        created, and attributes are set.
                        Can be omitted meaning "don't place the node".
pos        String|null  Optional argument. Can be a number or one of the
                        following strings: "before", "after", "replace", "only",
                        "first", or "last". If omitted, "last" is assumed.
                        This parameter is passed to :ref:`dojo.place <dojo/place>`
                        unmodified after the node is created, and attributes
                        are set. Please see :ref:`dojo.place <dojo/place>`
                        for more details and examples.
=========  ===========  =======================================================


The function returns a DOM node it created with ``tag`` or the first argument, if it was a DOM node.

Dojo 1.7+ (AMD)
---------------

When using AMD format in a fully baseless application, ``create`` is accessed from the ``dojo/dom-construct`` module.

.. js ::

  require(["dojo/dom-construct"], function(domConstruct){
      // create a div node
      var node = domConstruct.create("div");
  });

Alternatively, you can load dojo base in AMD style and continue using ``dojo.create`` in the ``define`` or ``require`` callback:

.. js ::

  require(["dojo"], function(dojo){
      // create a div node
      var node = dojo.create("div");
  });

Dojo < 1.7
----------

.. js ::

  // create a div node
  var node = dojo.create("div");


========
Examples
========

Create a <div>:

.. js ::
  
  // dojo 1.7+ (AMD)
  require(["dojo/dom-construct"], function(domConstruct){
    var n = domConstruct.create("div");
  });

  // dojo < 1.7
  var n = dojo.create("div");

Create a <div> with content:

.. js ::
  
  // dojo 1.7+ (AMD)
  require(["dojo/dom-construct"], function(domConstruct){
    var n = domConstruct.create("div", { innerHTML: "<p>hi</p>" });
  });

  // dojo < 1.7
  var n = dojo.create("div", { innerHTML: "<p>hi</p>" });

Append a new <div> to <body> with no attributes:

.. js ::
  
  // dojo 1.7+ (AMD)
  require(["dojo/dom-construct", "dojo/_base/window"], function(domConstruct, win){
    var n = domConstruct.create("div", null, win.body());
  });

  // dojo < 1.7
  var n = dojo.create("div", null, dojo.body());

Place a new <div> as the first child of <body> with no attributes:

.. js ::
  
  // dojo 1.7+ (AMD)
  require(["dojo/dom-construct", "dojo/_base/window"], function(domConstruct, win){
    var n = domConstruct.create("div", null, win.body(), "first");
  });

  // dojo < 1.7
  var n = dojo.create("div", null, dojo.body(), "first");

Decorate and place an existing node:

.. js ::
  
  // dojo 1.7+ (AMD)
  require(["dojo/dom-construct", "dojo/_base/window"], function(domConstruct, win){
    domConstruct.create(node, { style: { color: "red" } }, win.body());
  });

  // dojo < 1.7
  dojo.create(node, { style: { color: "red" } }, dojo.body());

Create an <ul>, and populate it with <li>'s. Place the list as the first child of a node whose id equals "someId":

.. js ::
  
  // dojo 1.7+ (AMD)
  require(["dojo/dom-construct", "dojo/_base/array"], function(domConstruct, arrayUtil){
    var ul = domConstruct.create("ul", null, "someId", "first");
    var items = ["one", "two", "three", "four"];
    arrayUtil.forEach(items, function(data){
      domConstruct.create("li", { innerHTML: data }, ul);
    });
  });

  // dojo < 1.7
  var ul = dojo.create("ul", null, "someId", "first");
  var items = ["one", "two", "three", "four"];
  dojo.forEach(items, function(data){
    dojo.create("li", { innerHTML: data }, ul);
  });

Create an anchor, with an href. Place in <body>:

.. js ::
  
  // dojo 1.7+ (AMD)
  require(["dojo/dom-construct", "dojo/_base/window"], function(domConstruct, win){
    domConstruct.create("a", { href: "foo.html", title: "Goto FOO!", innerHTML: "link" }, win.body());
  });

  // dojo < 1.7
  dojo.create("a", { href: "foo.html", title: "Goto FOO!", innerHTML: "link" }, dojo.body());

============
Alternatives
============

Creating and/or placing with dojo.place()
-----------------------------------------

In some cases it is easier to create a node from an HTML fragment and place it, without applying any attributes, or specifying them as a part of the HTML fragment. If this is the case consider :ref:`dojo.place <dojo/place>`:

.. js ::
  
  // duplicating the following line with dojo.place():
  // dojo.create("a", { href: "foo.html", title: "Goto FOO!", innerHTML: "link" }, dojo.body());
  
  // dojo 1.7+ (AMD)
  require(["dojo/dom-construct", "dojo/_base/window"], function(domConstruct, win){
    domConstruct.place("<a href='foo.html' title='Goto FOO!'>link</a>", win.body());
  });

  // dojo < 1.7
  dojo.place("<a href='foo.html' title='Goto FOO!'>link</a>", dojo.body());

.. js ::
  
  // duplicating the following line with dojo.place():
  // var n = dojo.create("div", null, dojo.body());
  
  // dojo 1.7+ (AMD)
  require(["dojo/dom-construct", "dojo/_base/window"], function(domConstruct, win){
    var n = domConstruct.place("<div></div>", win.body());
  });

  // dojo < 1.7
  var n = dojo.place("<div></div>", dojo.body());

Setting attributes with dojo.attr()
-----------------------------------

While you can use dojo.create to set attributes on the existing node without placing it, using :ref:`dojo.attr <dojo/attr>` is recommended:

.. js ::
  
  // duplicating the following line with dojo.attr():
  // var n = dojo.create(node, { innerHTML: "<p>hi</p>" });
  
  // dojo 1.7+ (AMD)
  require(["dojo/dom-attr"], function(domAttr){
    domAttr.set(node, "innerHTML", "<p>hi</p>");
  });

  // dojo < 1.7
  dojo.attr(node, "innerHTML", "<p>hi</p>");

========
See also
========

* :ref:`dojo.place <dojo/place>`
* :ref:`dojo.destroy <dojo/destroy>`
* :ref:`dojo.empty <dojo/empty>`
* :ref:`DOM Utilities <quickstart/dom>`
