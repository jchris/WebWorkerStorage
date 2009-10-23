## Minimal API
  - Non-relational (no references between records)
  - No transaction API is exposed to JavaScript.
  - Synchronous
    - rely on Web Workers for multi-process support (why implement something twice?)

## Motivation
  To build the simplest useful data store for web developers. WebWorkerStorage is a key/value store, with range queries. This combines the simplicity of localStorage or cookies with the ability to create custom indexes that can be used for complex queries.
  
## Storage
  At the heart of WebWorkerStorage is a persistent key-value store which supports range-queries. Traditionally this is implemented with a B-Tree or similar data structure although the spec doesn't care what's under the covers.
  
  The WebWorkerStorage API is designed to provide a solution that meets the needs for most web application development, with the minimum of implementation complexity.
  

### Storage Example



    var btree = new WebStorage("dbname");
    
    btree["some_key"] = {"some":"json"};
    
    btree.forEach(function(key, value) {
      // in order traversal
    })
    
    btree.forEach(function(key, value) {
      // reverse order traversal
    }, false)
    
    btree.forEach("startkey", "endkey", function(key, value) {
      // inorder traversal, starting from "startkey", ending with "endkey"
      // use throw() to stop traversal
    })
    
    btree.forEach("endkey", function(key, value) {
      // reverse order traversal, starting from "endkey"
      // use throw() to stop traversal
    }, false)
    
    // delete a btree
    WebStore.drop("dbname");


## Web Worker Example

### Map Reduce

### Replication

## Web Worker Extensions
