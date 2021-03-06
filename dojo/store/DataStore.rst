.. _dojo/store/DataStore:

dojo.store.DataStore
====================

:Authors: Kris Zyp
:Project owner: Kris Zyp
:Available: since V1.6

.. contents::
    :depth: 3

**dojo.store.DataStore** is an adapter for using Dojo DataStores with an object store consumer. This store allows the developer to convert existing datastores to implement the new :ref:`Dojo Object Store API <dojo/store>`.


========
Examples
========

.. js ::

 datastore = new dojo.data.ItemFileWriteStore({url:"data.json"});

 store = new dojo.store.DataStore({store: datastore});

 store.query("foo=bar").then(function(results){
   // use the query results returned from the server
 });

==============
Method Mapping
==============

With the DataStore store, store methods should intuitively map to DataStore API methods:

+-----------------------+----------------------------------------------------------------------------------+
|**Method**             |**Functionality**                                                                 |
+-----------------------+----------------------------------------------------------------------------------+
|get(id)                |This will do a `datastore.fetchItemByIdentity({identity: id})`.                   |
+-----------------------+----------------------------------------------------------------------------------+
|query(query, options)  |This will do a `datastore.fetch({query: query},options)`.                         |
+-----------------------+----------------------------------------------------------------------------------+
|remove(id)             |This will first do a `datastore.fetchItemByIdentity({identity: id})` followed     |
|                       |by a `datastore.deleteItem(item)`.                                                |
+-----------------------+----------------------------------------------------------------------------------+
|put(object, options)   |This will do a `datastore.newItem(object)` while respecting the options parameter.|
+-----------------------+----------------------------------------------------------------------------------+
