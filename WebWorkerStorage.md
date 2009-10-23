# WebWorkerStorage

This Document describes a simple storage API for web developers. The goal of the storage API is ease of use. It is targeted at modern web applications that need a simple, flexible and reliable in-browser storage solution.


## Authors

Jan Lehnardt, J Chris Anderson, Damien Katz


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

## Security

Any website can create new WebWorkerStorage database. Simliar to the same-origin policy, a website can only access WebWorkerStorage databases belong to the same domain.


## Privacy

Websites can request permission to read other domain's databases. The user MUST be explicitly confirm or deny the request. Vendors MAY add limitations to a confirmed permission. For example "allow once", "allow for this session", "allow today", "allow forever".


## References

[WW-message-passing]: http://www.whatwg.org/specs/web-workers/current-work/#handler-worker-onmessage



