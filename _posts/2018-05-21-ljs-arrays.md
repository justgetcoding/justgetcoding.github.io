---
layout: post
title:  "Arrays, a Gateway Into JavaScript"
date:   2018-05-21 12:00:00
categories: intro
image: pic02.jpg
author: "Sean Hornsby"
---

{{ page.title }}
================
{{author}}

This post comes from a conversation I had with my new friend Ahmed ([@ahmedbengayess](https://twitter.com/ahmedbgayess)). He very recently started to learn front end development. Some of the array methods were tripping him up, and I asked him to share the details of his struggles. It wasn't all that long ago that I was having similar struggles, and, to be honest, I still do.

##### Warning, my bias for functional programming and immutable data will clearly shine through here. It is just that, bias, so take it with a grain of salt. 

Let me start by listing the methods he specifically called out:
`let troublesomeMethods = ['filter', 'map', 'find', 'findIndex', 'forEach', 'sort']`

I think arrays are a great place to dig deep into how JavaScript works. They can be simple or complex and the methods used can also be simple or complex. We can use arrays to build our understanding of JavaScript iteratively. Here is what you can expect from the rest of this article:

 1. Anatomy of arrays
 2. Types of methods
 3. Callbacks

#### Anatomy of an Array

This should be short and sweet (but then again, I do ramble sometimes). There is more going on behind the scenes but it isn't important now. An array is a collection of elements. Each element has two properties, an index and a value. JavaScript arrays are 0-indexed, which means the first element has an index of 0. Most computer languages are 0-indexed. Knowing this, lets break down an array into its elements and values.

`let troublesomeMethods = ['filter', 'map', 'find', 'findIndex', 'forEach', 'sort']`

|Element|Value  |
|--|--|
| 0 | 'filter' |
| 1 | 'map' |
| 2 | 'find' |
| 3 | 'findIndex' |
| 4 | 'forEach' |
| 5 |  'sort'|

What this means is that we hav an array, called `troublesomeMethods`. It has 6 elements, each storing a string value. Element 0 has a value of 'filter'. We can refer to that as `troublesomeMethods[0]`. The next element, element 1, has a value of 'map'. We can refer to that as `troublesomeMethods[1]`. All the way down the list, er, array.

Arrays also have a property called `length`. It will, unsurprisingly, return the length of the array. `troublesomeMethods.length` will return `6`. Notice that the length is a higher number than the last element of the array. That is a consequence of 0-indexing. It's not important, but something to be aware of.

One last thing, and while it might seem small or insignificant, it is actually really big. The value of an array can be anything. Strings, integers, floats, objects, other arrays, even functions. And a single array can hold any or all of these things. Don't get too hung up on this now, we'll cover this in more depth when it becomes important.

#### Types of Methods

Array methods can do one of two things. They can mutate the array they are called upon, or they can return a new value. What does that mean? Let's look at an example of a method that mutates the existing array, `sort()`. Below I show our existing array, then I use the sort method on it, and then I show the array again. Notice the first and third results are different. The array has been changed. This is mutation. 

```
troublesomeMethods // [ 'filter', 'map', 'find', 'findIndex', 'forEach', 'sort' ]
troublesomeMethods.sort() // [ 'filter', 'find', 'findIndex', 'forEach', 'map', 'sort' ]
troublesomeMethods // [ 'filter', 'find', 'findIndex', 'forEach', 'map', 'sort' ]
```
A lot of 'traditional' array methods will change (mutate) the array they are called on. This includes methods like push, pop, shift, and splice (but not slice).

Some methods that do not mutate the array are map, reduce, filter, slice, concat, find, findIndex. Wherever possible, these are the methods I reach for when I work with arrays.

#### Callbacks

This could be where it gets more difficult. Most of the methods do not take a simple (primitive) value as the argument, but rather a callback. Here is the syntax for find, from [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find): `arr.find(callback[, thisArg])`

This might be a good time to talk about how to read these signatures. In this one `arr` is the array the method will be called on. `find` is the name of the method. `[,thisArg]` is complicated. The square brackets `[]` indicate that this is an optional argument. What it dos for this function is set the this binding, which would require another whole post (or two) to explain. For now let's ignore it. Because I want the syntax to be clear, I am going to rewrite it without using the optional argument. 

`arr.find(callback)`

What is `callback`? Reading further into the MDN document it says that `callback` is a "function to execute on each value in the array." This function itself takes three arguments `element[, index, array]` Once again we will ignore the optional arguments for now and focus on `element`, which is "the current element being processed in the array."

What does that mean? Remember, the callback function will be called on each value in the array. Each time it is called, the value will be passed into the function.

Bear with me, I know this can be confusing. There is just a little more explanation and then I will hopefully clear it all up with examples.

Often times, the callback function is declared inside the method call. From MDN again:
```
var array1 = [5, 12, 8, 130, 44];
var found = array1.find(function(element) {
  return element > 10;
});
found // 12
```

What find is going to do here is pass each item in the array into the callback function. The callback will execute a test and return a value. If the test fails it will return false and the find keeps running. If the test passes, it will return the value and stop running. On the first pass it sends the first element, with a value of 5, to the function.  The body of the function checks to see if 5 is greater than 10. It isn't so it returns `false`. Then it goes to the next element, with a value of 12. This time the test passes, so it returns the value (not `true`, but the actual value, `12`) and stops running. 

`array.findIndex()` works almost exactly like `.find()` except it returns the index number of the element instead of its value.
```
var array1 = [5, 12, 8, 130, 44];
var found = array1.findIndex(function(element) {
  return element > 10;
});
found // 1 (remember the array is 0-indexed)
```

#### The Nitty Gritty

That almost takes care of find and findIndex. One distinction between the two, if nothing passes the test of find, it will return `undefined`. If the same thing happens to findIndex, it will return `-1`. This is useful but somewhat outside the scope of this disucssion.

Here is where we stand:
['filter', 'map', '~~find~~', '~~findIndex~~', 'forEach', 'sort']

`forEach()` is a nice method, and it has a lot in common with `.map()`, so I want to cover it when we get to `.map()` and `.filter()`. That means that we are tackling `.sort()` next.  The [MDN page](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) sums up everything that is wrong with sort in the three sentences:

>The `sort()` method sorts the elements of an array _[in place](https://en.wikipedia.org/wiki/In-place_algorithm)_ and returns the array. The sort is not necessarily [stable](https://en.wikipedia.org/wiki/Sorting_algorithm#Stability). The default sort order is according to string Unicode code points.

What that means is that it a) mutates the array, b) can return unpredictable values, and c) the default sort probably doesn't do what you expect.

Luckily, you can override the default sort, so you can write a sort that is appropriate for your data. Here is the syntax: `arr.sort([compareFunction])`. This time all (one) of the arguments are optional. If you don't pass a compareFunction, it will use the default sort. Whatever you are trying to do, it is very unlikely that the default sort will do it correctly.

#### (Mostly) Immutable Methods

`.forEach()` returns `undefined` no matter what you do in the callback. In that way it is immutable. `.map()`, `.filter()`, `.reduce()`,  `.concat()`, and `.slice()` return a new array but leave the existing array alone. Immutability isn't protected by JavaScript. If you really want, you can still screw up this immutability, but at least the methods themselves don't mess with the data.

With `.forEach()`, the callback is performed on each element in the array. Nothing is returned from the callback. Or rather, anything that is returned is ignored. 

`.map()` also iterates over each element in the array. The difference is, it creates a new array with each element being the return value from the callback. If you call `.map()` on an array with 5 elements, it will create a new array with 5 elements.

What is the difference between `.forEach()` and `.map()`? If you want to transform the data from one format to another, with a one to one ratio, use `.map()`. If you want to do something with some (or all, or none) of the data, use `.forEach()`.

```
var array1 = [5, 12, 8, 130, 44];
array1.forEach(function(element) {
  return element * 2;
});
// returns undefined
array1 // [5, 12, 8, 130, 44]

// A fairly useless case for forEach
// More often you see it being used to create a new array like this:

var newArray = [];
array1.forEach(function(element) {
  newArray.push(element * 2);
});
newArray // [ 10, 24, 16, 260, 88 ]
```

Using map, we can do similar things:

```
var array1 = [5, 12, 8, 130, 44];
var newArray = array1.map(function(element) {
  return element * 2;
});
array1 // [5, 12, 8, 130, 44]
newArray // [ 10, 24, 16, 260, 88 ]
```

`.filter()` has some similarities to `.find()`. The biggest differences are that it creates a new array with ***all*** the values that pass the test instead of just returning the first value that passes. We can even use the same callback:

```
var array1 = [5, 12, 8, 130, 44];
var foundFilter = array1.filter(function(element){
  return element > 10;
});
foundFilter // [ 12, 130, 44 ]
```

There is so much more, but this is already getting pretty long. I am going to break here, and in part II, we can dive deeper into complex callbacks and a few of the more complicated methods.