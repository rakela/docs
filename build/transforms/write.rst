.. _build/transforms/write:

Build Transform write
=====================

:Version: 1.7
:Author: Rawld Gill

.. contents::
   :depth: 2

=======
Summary
=======

Writes a resource a destination location.

===========
Description
===========

This transform writes the possible-transformed resource text to the destination unless the resource has been tagged
"noWrite". If the resoure has been tagged noWrite, the transform does nothing.

Note: typically a noWrite tag is added during some other transform that contains logic that makes a decision the
resource is not needed. If a noWrite decision can be made during descovery, then the resource should not be scheduled
for the write transform to begin with.

=============
Profile Knobs
=============

None.

===============
Source Location
===============

util/build/transforms/write.js
