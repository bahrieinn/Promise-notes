Promise-notes
=============

Collection of resources / notes on the concept of promises in JS

##Resources
* [NetTuts+ Wrangle Async Tasks With JQuery Promises](http://net.tutsplus.com/tutorials/javascript-ajax/wrangle-async-tasks-with-jquery-promises/)
* 

##Notes
A promise object is a one-time event (typically the outcome of an async task). Promises allow us to decouple the actual call itself (e.g. $.ajax) from the subsequent actions based on the result of the call. 

How we used to write async functions:
```javascript
function myAsyncFunction() {
    $.getJSON('/api/data.json', function(data) {
        // Handle the data
    });
}
```
Here, `myAsyncFunction()` is responsible for **2 things** - Getting the data **AND** doing stuff with the data, and ideally we want single responsibility methods.

So we probably want something that looks more like the following:
```javascript
function myAsyncFunction(){
    $.getJSON('/api/data.json', mySeparateFunction(data) );
}

function mySeparateFunction(data){
    // Magic
}
```
Here we are a little closer to separating our responsibilities by abstracting our callback into its own function but it is still explictly tied to the async call. With the help of promises, we can completely separate the two with the following:
```javascript
function myAsyncFunction(){
    return $.getJSON('/api/data.json');
}

function mySeparateFunction(data){/*do stuff*/};

myAsyncFunction().done( mySeparateFunction );
```

With this last pattern, we utilize jQuery's `.done()` function which just calls `mySeparateFunction` as soon as our async call is **resolved** and the promise object is returned.

##jQuery's promise object functions
* `.done()` 
* `.fail()` 
* `.always()` 
* `.then()` 
