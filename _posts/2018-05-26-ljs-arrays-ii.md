---
layout: post
title:  "Arrays, a Gateway Into JavaScript (part II)"
date:   2018-05-26 12:00:00
categories: intro
image: pic02.jpg
author: "Sean Hornsby"
---

In the last article, I covered the basics of arrays and a few of the methods they come bundled with in JavaScript. Before I dive much deeper I want to offer a couple caveats. There is way more depth to this topic than I have covered so far. I have definitely glossed over some of the concepts involved. I am not trying to present this as a comprehensive or complete set of lessons on the topic. What I *am* trying to do here is help people understand how to use array methods and hopefully glean some insight into how and why they work.

Hopefully I find the right balance between oversimplified and understandable.

#### Callbacks
At the heart of unlocking array methods is the idea of callbacks. I remember (because it really wasn't that long ago) being overwhelmed by all of the new lingo in programming. These days I take for granted my (hard-won?) understanding of terminology. But I remember being confused by the concept of a callback.  For some context, lets look at the syntax of Array.prototype.map() courtesy of [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

``` javascript
var new_array = arr.map(function callback(currentValue[, index[, array]]) {
    // Return element for new_array
}[, thisArg])
```
Let's rip the optionals out and strip it down to essentials.
``` javascript
.map(function callback(currentValue) {})
```
What this means is that, when we call the map method, we are being asked to pass into it a function. For *reasons* (convention being one of them), this function, in this context, is referred to as a ***callback***. We can call it whatever we want (or, in the case of anonymous functions, nothing at all). So the most important takeaway from this section is, don't get hung up on the language.

So far this is all very hypothetical, so let's get hands-on.  I chose `.map` for several reasons. In simple terms, it is the non-mutating version of the much more common `.for` and `.forEach` methods. If I want get the square of each element in an array, and store it in a new array, I can use `.forEach` like so:

```javascript
let  arr  =  [1,2,3,4,5];
let mutatedArr = [];
arr.forEach(function square(i) {
  mutatedArr.push(i*i)
});
//mutatedArr is now [ 1, 4, 9, 16, 25 ]
```

Using map is very similar with some subtle differences.
```javascript
let  mappedArr  =  arr.map(function square(i)  {
  return  i  *  i;
});
// mappedArr is now [ 1, 4, 9, 16, 25 ]
```

In both cases, the function I defined inline, and called ***square***, is the ***callback***. I could have called it anything, the name is only important to me. In this case it tells me (and future me) what the intent of the function is. Also, in both cases, (because of how `.forEach` and `.map` work), the function is run once for each element in the array (in my case I named it `arr`) I called the method on. I know this because it says so in the docs:

> The  `map()`  method creates a new array with the results of calling a provided function on every element in the calling array.

> The `forEach()` method executes a provided function once for each array element.

Many, but not all, array methods work on every item in the array. `.pop` and `shift` are examples of methods that **do not**

What is the callback doing? How does it work? What is going on?! Let's look at the map version one more time and then dissect it.
```javascript
let arr = [1,2,3,4,5];
let  mappedArr  =  arr.map(function square(i)  {
  return  i  *  i;
});
```
`arr` is an array with five elements. `arr.map(callback)` is going to run the callback method 5 times, passing in an element each time. In our case it will pass in `1`, then `2`, etc. The callback method we have provided to `.map` is 

```javascript
function square(i)  {
  return  i  *  i;
})
```
What happens if we call `square(1)`? The function will multiply 1 by itself and return the value `1` of that computation to the caller. How about `square(2)?` This time it multiplies 2 by itself and returns `4` to the caller. `.map` will insert those values into an array that it instantiates on the spot. When it has been called once for each element, it will return that array. In our case we are storing the value returned in a variable called `mappedArr`

Seeing all of that in action helps, I hope, demystify the idea of ***callbacks***. In the end, they are just functions. That also means, because functions are first-class in JavaScript, we can pass them in instead of defining them on the spot. If we declare the function outside of the `.map` call, we can then use it in the `.map` call:
```javascript
function  square(i) {
  return  i  *  i;
}

let  mappedArr  =  arr.map(square); // [1, 4, 9, 16, 25]
```
There is a good discussion to be had about when and why you should use this style over just writing the function in the call itself, but it is too much to cover here.

Let's see how other methods utilize the ***callback***.
#### Filter
Filter is another good (non-mutating) method in the Array prototype. 
>The `filter()` method creates a new array with all elements that pass the test implemented by the provided function.

```javascript
var newArray = arr.filter(callback(element))
```

Using our same array, imagine we want to return only the values greater than 3.

```javascript
let arr = [1,2,3,4,5];
let filteredArr = arr.filter(function(i) {
  return i > 3;
});
// filteredArr = [4, 5]
```
Our callback takes each value and returns the result of the computation `i > 3`. JavaScript returns that value as a Boolean (true or false). In the cases where that value is true, `.filter` stores that element in an array. Just like `.map`, when it has been called once for each element, it will return that array. We store it in the variable `filteredArr`.

One thing to be aware of with filter, the callback is expected to be a test. It should return `true` or `false`. JavaScript (along with other languages) also has `truthy` and `falsy` values. If you are getting weird results from a call to `.filter`, it might be because you aren't explicitly returning a Boolean.
#### Reduce
Reduce melted my brain. Over and over again. Even after I understood callbacks. Even after I successfully used `.reduce`, repeatedly. It's not hard to understand why it is confusing:
>The `reduce()` method applies a function against an accumulator and each element in the array (from left to right) to reduce it to a single value.

Applying a function to each element is understandable. It is explainable. It is demonstrable. But now I am also including a what? Oh, an accumulator... I guess it accumulates things (spoiler: it does). All of that is going to then return a *single value*. Ok.

The most commonly shown example of reduce is adding numbers together. So let's look at that. Just keep in mind it is an extremely reductionist example of what reduce can do (pun fully intended).

```javascript
let arr = [1,2,3,4,5];

let  reducedArr  =  arr.reduce(function(accumulator,  i)  {
  return  accumulator + i;
}, 0); // return 15
```
For the first time I am passing two values into the ***callback***. The first value is the accumulator, and the second is the current element of the array. Most often it will be called `current_value` or `curr` or some variation, but I decided to use `i` as I have been doing for all the other methods. Also, and this is important because it is one reason why the documentation can be incredibly confusing, after the ***callback*** I am passing it the value `0` (last line, just before the closing paren and the semicolon). Why?

That value is referred to as the `initialValue`. It is *optional*, and it is the first time I have used an optional value in these tutorials. The `.reduce()` method acts slightly differently depending on if `initialValue` is passed. In fact, it is easier to explain in the case that `initialValue` is passed, so that is where I will start.

If initial value is passed, the accumulator will start with that value. The callback will be called for each element in the array, just like we are used to. After the first element, the accumulator is set to the return value from the previous call.

In our case, on the first pass, the accumulator is set to 0 and the callback is given the first element, 1. The body of the function adds those values together and returns 1. The accumulator is set to that value and the callback runs with the next element of the array. So on the second pass, the callback gets 1 (the accumulator), and 2 (the value of the second element). The function adds those together and returns 3. The accumulator is set to 3 and the callback runs again with 3 (the accumulator), and 3 (the value of the third element). This continues until there are no more elements, at which point the method returns the accumulator.

 Here is what that looks like in table form.

| Accumulator | i *(current value)*| return value|
|--|--|--|
| 0 | 1 | 1 |
| 1 | 2 | 3 |
| 3 | 3 | 6 |
| 6 | 4 | 10 |
| 10 | 5 | 15 |

At the end of the run, our reducer returns 15, the sum of the numbers 1, 2, 3, 4, and 5.


What happens if we **do not** pass an `initialValue`? In that case, `.reduce()` does some behind-the-scenes work. It takes the first value of the array as the initial value and skips the first run through the callback. In other words, instead of starting at the first element, it starts at the second. The result, in our case, is the same. As the method begins, it notices there is no `initialValue`. So it gets the value of the first element in the array and sets the accumulator to that value. Then it runs the callback, starting at the second value. 

| Accumulator | i *(current value)*| return value|
|--|--|--|
| 1 | 2 | 3 |
| 3 | 3 | 6 |
| 6 | 4 | 10 |
| 10 | 5 | 15 |

That is probably the simplest use case and result for `.reduce()`, and it is a good place to start. It really is the tip of the iceberg though. Remember how the definition says that reduce returns a *single value*? It is very easy to get trapped by that definition into thinking that it will always return a *simple* value. This is not true. That value can be anything. In our case we got back a single integer. It could have been a string. It could be an array, or an object. In fact, both `.map()`, and `.filter()` are just forms of `.reduce()` That blew my mind. Here is the `.map()` call we made earlier in the article as a `.reduce()`

```javascript
let arr = [1,2,3,4,5];

let  fakeMap  =  arr.reduce(function(accumulator,  curr)  {
  return  acc.concat(curr  *  curr);
}, []) // [1, 4, 9, 16, 25]
```

And the filter:

```javascript
let  fakeFilter  =  arr.reduce(function(accumulator,  curr)  {
  if (curr  >  3) { 
    return  accumulator.concat(curr)
  }
  return  accumulator;
},[]) // [4, 5]
```

Building on how we know the first reducer (the sum of values) works, see if you can figure out how the map and filter reducers work. Reach out to me with any questions. I'll pick it up again here next time, along with a discussion on how `.sort()` is nowhere near as simple as it sounds.