.. _dojo/robotx:


dojo/robotx
=============


.. contents::
    :depth: 2

Loads an external app into an iframe and points dojo.doc to the iframe document, allowing the robot to control it

========
Features
========

* `doh.robot.initRobot`

  Opens the application at the specified URL for testing, redirecting dojo to point to the application environment instead of the test environment.

* `doh.robot.waitForPageToLoad`

  Notifies DOH that the doh.robot is about to make a page change in the application it is driving,returning a doh.Deferred object the user should return in their runTest function as part of a DOH test.
