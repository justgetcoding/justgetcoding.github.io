---
layout: post
title:  "Extending core functionality"
date:   2017-02-21 10:10:45 -0800
categories: intro
image: pic10.jpg
author: "Sean Hornsby"
---

{{ page.title }}
================
{{author}}

Today we are going to talk about writing code that extends the core JavaScript functionality.
It draws technique from polyfills (shims), and allows you to add new methods directly onto existing
prototypes.

To start with, we are going to extend Array to have an actual numeric sort. You are likely aware that
arrays have a .sort() method, but if you have ever tried to use that to sort numbers, you were probably
disappointed with the results. That is because by default it converts the elements to strings and compares
them by unicode point order. Not what you are looking for when you pass it [15, 10, 5, 89, -3, 0]!

It is pretty simple to just supply sort with a comparison function, but it really isn't that much more difficult
to extend Array with a new method built to sort numbers. That's just what we're going to do.

The code used to compare numbers instead of strings is right in the MDN entry for sort() [link here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort "MDN Array.sort()"). It's the heart
of what we are going to use. It looks like this:

```javascript
function compareNumbers(a, b) {
  return a - b;
}
```

If you were to type:
```javascript
[15, 10, 5, 89, -3, 0].sort( ( a, b ) => a-b }
```
you would get back exactly what you expect, [-3, 0, 5, 10, 15, 89]. You could use that every time you wanted to sort numbers.
Or, you could decide you would rather type:
```javascript
[15, 10, 5, 89, -3, 0].numericSort();
```
Extending the prototype is easy enough, just grab the prototype and give it a new method.
```javascript
Array.prototype.numericSort = function() {

}
```
Later we will add a little bit of boilerplate that keeps us safer when globally adding this type of code, 
but for now let's just focus on making it work. The next step is to grab the Object being passed into the method.

```javascript
var O = Object(this);
```
Then we just hardcode the comparison function from earlier:
```javascript
return O.sort( ( a, b ) => a-b);
```
That's it. Once that code is available, numericSort() will do the work for us. Here it is all together:
```javascript
// numericSort.js
module.exports = function () {
  if(!Array.prototype.numericSort) {
    Array.prototype.numericSort = function() {
      if(this == null) {
        throw new TypeError('this is null or not defined');
      }
      var O = Object(this);
      return O.sort( ( a, b ) => a-b);
    }
  }
}

//app.js
require('./sort')();
console.log([15, 10, 5, 89, -3, 0].numericSort()); // [-3, 0, 5, 10, 15, 89]
```

