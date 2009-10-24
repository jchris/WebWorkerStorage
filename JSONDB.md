# JSONDB

This Document describes a simple storage API for web developers. The goal of the storage API is ease of use. It is targeted at modern web applications that need a simple, flexible and reliable in-browser storage solution.


## Version

Pre-0.1


## Authors

Jan Lehnardt, J Chris Anderson, Damien Katz


## Minimal API
  - Non-relational (no references between records)
  - No transaction API is exposed to JavaScript.
  - Synchronous
    - rely on Web Workers for multi-process support 
    - (why implement something twice?)


## Motivation
To build the simplest useful data store for web developers. JSONDB is a key/value store, with range queries. This combines the simplicity of localStorage or cookies with the ability to create custom indexes that can be used for complex queries.


## Storage
  
At the heart of JSONDB is a persistent key-value store which supports range-queries. Traditionally this is implemented with a B-Tree or similar data structure although the spec doesn't care what's under the covers.

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


### It's Enumerable!

`map()`, `reduce()` (js native), etc.


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

[WW-message-passing]: http://www.whatwg.org/specs/web-workers/current-work/#handler-worker-onmessage



