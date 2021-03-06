.. _dojo/on:

dojo/on
=======

:Authors: Kris Zyp
:Project owner: Kris Zyp
:Available: 1.7.0

.. contents::
  :depth: 2

The dojo/on module is a general-purpose event handler for DOM nodes and other event emitting objects, providing normalized event listening and event dispatching functionality. This module is designed to be lightweight and fast, based on modern browsers' event model.

===========
dojo/on API
===========

The module's value is an on function that can be directly called to add an event listener. The on function is the form:

.. js ::

  on(target, eventType, listener);

The following parameters should be provided to the on function:

* target - This is the target object (a DOM node or other event emitting object) that will be the source of the events. The target object may be a host object with it's own event capabilities (like DOM elements or the window), or it may be an event emitting JavaScript object (an object with an on() method like Dijits).
* eventType - This is the name of the event to be listening for (like "click"). This may include a (CSS) selector to specify the target nodes to listen for.
* listener - This is the function that will be called when this event takes place. The listener function will be called with 'this' as the target object (or the element targeted by the selector in the case of event delegation) and the first and only argument will be the event. The event object is normalized to have the important standard properties and methods of a W3C event (target properties, preventDefault(), stopPropagation()).

The basic usage looks like:

.. js ::

  define(["dojo/on"], function(on){
    on(document, "click", clickHandler);
  });

The return value from the on function is a signal handler that has a cancel() method that can be used to stop listening for the events. For example, to listen for a single click, one could do:

.. js ::

  var signal = on(document, "click", function(){
    // cancel after first event
    signal.cancel();
    // now perform any other action
  });



Use with query module
---------------------

The on function is also available on queried NodeList's with the NodeList on() method. For example, we could write:

.. js ::
  
  // Dojo 1.7 preferred
  define(["dojo/query"], function($){
    $("button").on("click", clickHandler);
  });
 
  // Pre 1.7 style
  dojo.query("button").on("click", buttonClickHandler);

Normalization
-------------

One of the key benefits of using dojo/on is that it provides event normalization, event listeners will receive an event object with the properties defined by the W3C event model, even in Internet Explorer. Generally, dojo/on does not normalize non-standard properties. There are some non-standard geometry properties that are often desirable, that are not normalized by dojo/on. The dojo/dom-geometry module provides a normalizeEvent function that can be used to normalize the pageX, pageY, layerX, and layerY properties on events.

Multiple Events
---------------
You can listen to multiple event types with a single call by comma-delimiting the event names. Then we can listen for multiple events (with delegation) with one call. For example, we can listen for touchend and dblclick:

.. js ::

  on(element, "dblclick, touchend", handler);

Event Delegation
----------------
The on function also provides event delegation functionality. One can use a selector in the event type name to indicate the nodes that are targetted for event listening. The on function will then use respond to event bubbling and trigger the listener when the appropriate child nodes trigger the event. The format for  selector-based event listening is to use "<selector>:<eventType>" as the eventType. For example, to listen for click events on elements with the myClass class name, we could do:

.. js ::

  on(document, ".myClass:click", clickHandler);

To listen for double clicks on the document and clicks on buttons with myClass class name, we could do:

.. js ::

  on(document, "dblclick, button.myClass:click", clickHandler);

Note that event delegation will only work on events that bubble. Most DOM events do bubble, but there are a few exceptions. The "mouseenter" and "mouseleave" events do not bubble, but "mouseover" and "mouseout" are the bubbling counterparts. The "focus" and "blur" events do not bubble, but dojo/on normalizes "focusin" and "focusout" as bubbling equivalents. Also, "scroll" events don't bubble.

Also note that dojo/query must be loaded for event delegation to work. The dojo/query module is part of Dojo base and therefore is normally loaded unless you are doing a baseless application and dojo/query hasn't been incldued.

Extension Events
----------------

The eventType parameter may also be an extension event. An extension event is a custom event that may be based on extended functionality. Dojo includes several extension events, including touch gestures available in dojo/gestures and mouse tracking functionality with dojo/mouse's enter and leave extension events. For example, to listen for the mouse hovering over a DOM node, we could write:

.. js ::

  define(["dojo/on", "dojo/mouse"], function(on, mouse){
    on(node, mouse.enter, hoverHandler);
  });

You can also create your own extension events. An extension event is simply a function (or any object with a call() method) that will be called with two parameters. The first parameter is the target and the second is the listener.

The module's on function also has several others properties/functions on it for additional functionality:

selector function
-----------------

The on.selector function can be used to apply event delegation when extension events are used (since you can't use the "<selector>:<type>" syntax with an extension event). The on.selector function is called with the CSS selector as the first argument and the event type as the second argument. For example, to listen for the mouse.enter extension event on elements with the myClass class name, we could write:

.. js ::

  define(["dojo/on", "dojo/mouse"], function(on, mouse){
    on(node, on.selector(".myClass", mouse.enter), myClassHoverHandler);
  });

emit function
-----------------

The on.emit function provides a normalized mechanism for dispatching events. This method will dispatch an event using the native event facilities when available, and will emulate these facilities otherwise. The emit function takes three arguments (the first two closely mirror the on function):

* target - This is the target object (a DOM node or other event emitting object) that will be the source of the event. The target object may be a host object with it's own event capabilities (like DOM elements or the window), or it may be a JavaScript object with an on() method.
* eventType - This is the name of the event type to be dispatched (like "select"). This event may be a standard event (like "click") or a custom event (like "finished").
* eventProperties - This is an object with the properties of the event to be dispatched. Generally you should align your properties with W3C standards. Two properties are of particular importance:

* eventProperties.bubbles - This indicates that the event should bubble up, first firing on the target object, next on the target object's parent (parentNode) and so on until it reaches the top of the DOM or bubbling is stopped. Bubbling is stopped when a listener calls event.stopPropagation().
* eventProperties.cancelable - This indicates that the event's default action can be cancelled. The default action is cancelled by a listener by calling event.preventDefault(). The emit method does not perform any default action, it returns a value allowing the calling code to perform any default action.

The emit function returns the event object unless the event is cancelable and is cancelled by one of the listeners, in which case it will return false. For example:

.. js ::

  define(["dojo/on"], function(on){
    var event = on.emit(button, "click", {
      bubbles: true,
      cancelable: true,
      which: 1
    });
    // if event is not false, the event was not cancelled, we can do our default action
    if(event){
      submitForm();
    }
  });

pausable function
-----------------

The on.pausable function provides a means for pausing an event listener, while still preserving the listeners order and state. The on.pausable() function can be called just like on() (with the same arguments). The only difference is the returned signal handler will include pause() and resume() methods. The pause() method will cause the listener to not be called when the specified event takes place. The resume() method will cause the listener to be called again. For example, we could write:

.. js ::

  var buttonHandler = on.pausable(button, "click", clickHandler);
  on(disablingButton, "click", function(){
    buttonHandler.pause();
  });

once function
-------------

The on.once function allows you to register a listener that will be called just once in response to an event. This works just like on(), but the listener will be called a single time and then it will be removed as a listener. For example:

.. js ::

  on.once(finishedButton, "click", onFinished);


Converting from dojo.connect
----------------------------
dojo/on can replace dojo.connect when connect is used for connecting to DOM nodes and event emitting objects (see the dojo/Evented page for more information). If you're connecting to a plain method, use dojo/aspect instead.  Also, note that some event emitting objects, like dijits, have their own event naming conventions and may need to be changed to remove "on" from the names and lower-case the remaining event names used with dojo.connect for some event emitting objects like dijits.

Transitioning to Dojo 2.0
-------------------------
The dojo/on module is expected to be a core module in Dojo 2.0 with the API introduced in 1.7. The dojo/on module can be used for listening to events on DOM and host objects, as well Evented objects such that your code should transition to 2.0. However, the event emitting objects in Dojo (including Dijits, Dnd, and Animation) are likely to change their events (both names and emitted event objects) in 2.0, so one should not assume that code using dojo/on to listen to Dojo objects will work unchanged in 2.0.
