---
layout: post
title:  "Extending core functionality II"
date:   2017-02-28 10:10:45 -0800
categories: intro
image: pic10.jpg
author: "Sean Hornsby"
---

{{ page.title }}
================
{{author}}

(This is part 2, if you are just joining us, read <a href="https://justgetcoding.github.io/intro/2017/02/21/extending-array.html">this first</a>.)

So you've had a few days to play with .numericSort() and maybe you've starting thinking, "what if I want to reverse the sort?"
Well, you have a couple of choices. You could extend Array again, with somthing like .reverseNumericSort(). That would work fine.
Or you could add a parameter to .numericSort(). I like that idea better. Let's see how that's done.

Figuring out the guts of the reversed sort is pretty simple. It's just the reverse of the forward sort.

```javascript
( a, b ) => b - a;
```
But how do we add that option to .numericSort()? It turns out that is pretty simple too. This is what we're starting with:
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
```
Let's just add a parameter called reverse. Our options will be 0 for forward and 1 for backward;
```javascript
// numericSort.js
module.exports = function () {
  if(!Array.prototype.numericSort) {
    Array.prototype.numericSort = function(reverse) {
      if(this == null) {
        throw new TypeError('this is null or not defined');
      }
      var O = Object(this);
      if(reverse) return O.sort( ( a, b ) => b - a);
      else return O.sort( ( a, b ) => a - b);
    }
  }
}
```
All that's left is to try it out.
```javascript
//app.js
require('./sort')();
console.log([15, 10, 5, 89, -3, 0].numericSort()); // [-3, 0, 5, 10, 15, 89]
console.log([15, 10, 5, 89, -3, 0].numericSort(1)); // [89, 15, 10, 5, 0, -3]
```