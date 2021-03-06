.. _dijit/form/DataList:

dijit.form.DataList
===================

:Status: Draft
:Version: 1.0
:Authors: Doug Hays
:Developers: Doug Hays
:Available: since V1.7

.. contents::
    :depth: 2

DataList is a read-only data store that processes inline OPTION tags as data items.  This store implements the new :ref:`Dojo Object Store API <dojo/store>`.  The DataList store is also a synchronous store. All the functions directly return results, so you don't have to use asynchronous callbacks in your code.


========
Examples
========

HTML5 markup
------------

.. html ::

  <select data-dojo-type="dijit.form.DataList" data-dojo-props='id:"fruit"' >
        <option value="Ap">Apples</option>
        <option value="Ba">Bananas</option>
        <option value="Bl">Blueberries</option>
        <option value="Or">Oranges</option>
  </select>

  <script type="text/javascript">
        var store = dijit.byId('fruit');
        alert('fruit that start with "B" = ' + store.query({name:/^B.*/}).map(function(option){ return option.name; }));
  </script>

.. image:: DataList.png
