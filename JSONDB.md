# JSONDB

This Document describes a simple storage API for web developers. The goal of the storage API is ease of use. It is targeted at modern web applications that need a simple, flexible and reliable in-browser storage solution.


## Version

Pre-0.1


## Authors

Jan Lehnardt, J Chris Anderson, Damien Katz


## Motivation

To build the simplest useful data store for web developers. JSONDB is a key/value store, with range queries. This combines the simplicity of localStorage or cookies with the ability to create custom indexes that can be used for complex queries.


## Minimal API

The API described in this document is meant to be the base for more elaborate storage solutions. It aims to only include features that are required to build larger, more complex storage solutions and no more.

JSONDB is a non-relational database. There are no tables, no SQL or SQL-like query language. No object relational mapper (ORM) is required to use JSONDB.

The API is a pure JavaScript API that runs within a page's context in the browser (and in non-browser JavaScript environments).

JSONDB does not support transactions. Each operation is atomic.

The core API is synchronous. If wrapped in a [WebWorker][WebWorkers] and using [WebWorkers Message Passing][WW-message-passing] JSONDB supports asynchronous, concurrent access through a lockless MVCC API.

_We are happy to add an asynchronous component to this document. Patches are welcome._

## Storage
  
At the heart of JSONDB is a persistent key-value store which supports range-queries across the sorted keys, as well as across secondary indexes on the values.

Traditionally this is implemented with a B-Tree or similar data structure although the spec doesn't care what's under the covers.

The JSONDB API is designed to provide a solution that meets the needs for most web application development, with the minimum of implementation complexity.



### Storage Example

real world use case w/o web worker. in page.

sortable todo list


### Storage API

Run through some API actions, including native JS features.

    var jsondb = new JSONDB("dbname");
    
    jsondb["some_key"] = {"some":"json"};
    
    jsondb.forEach(function(key, value) {
      // in order traversal
    });
    
    jsondb.forEach(function(key, value) {
      // reverse order traversal
    }, {
      "descending":true
    });
    
    jsondb.forEach(function(key, value) {
      // inorder traversal, 
      // starting from "startkey", 
      // ending with "endkey"
      // you can use throw() to stop traversal
    },{
      "startkey":"a", 
      "endkey":"z"
    });
    
    jsondb.forEach(function(key, value) {
      // reverse order traversal, starting from "startkey"
      // you can use throw() to stop traversal
    },{
      "startkey":"z",
      "descending":true 
    });
    
    // delete a btree
    JSONDB.drop("dbname");


#### It's (sorta) Enumerable!

    // multiply by 7
    // map returns a new JSONDB based on the mapped return values
    // the original JSONDB instance is not altered
    jsondb.map(function(key, value) {
      return value * 7;
    });
    
    // count stuff, initialize sum with 0
    // iterates over the database on read time doing a "full table scan"
    var total = jsondb.reduce(function(key, value, acc) {
      return acc + value;
    }, 0);


#### Database Properties

    jsondb.name; // "dbname" (database name)
    jsondb.length // 3 (number of elements)


## Example Use Cases

Show some simple examples to demonstrate the JSONDB coolness.


### Web Worker MVCC & Validations

revs for document updates.

sequence secondary index

validation functions


### Incremental Indexing

groups of map funs following seq index with back index

reduce is at runtime


### Remote Replication

maintain


## Web Worker Extensions

singleton web worker
html rendering
receive messages from other domains


## Security

JSONDB databases are subject to the same-origin policy, a page or worker can only access JSONDB databases belong to the same domain.



## References

[WebWorkers]:  http://www.whatwg.org/specs/web-workers/
[WW-message-passing]: http://www.whatwg.org/specs/web-workers/current-work/#handler-worker-onmessage

*

## TODO:
 - Discuss
  - Can keys be more than strings? ( `db[{"a":1}] = 77`)
  
