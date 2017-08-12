---
layout: post
title:  "Learning Javascript IV - Data Types"
date:   2017-08-12 14:10:45 -0800
categories: intro
image: pic02.jpg
author: "Sean Hornsby"
---

{{ page.title }}
================
{{author}}

Now we know how to store _stuff_ in variables... what kind of stuff can we store there? The answer is, almost whatever we want. There are obvious things like numbers and strings. Something called a Boolean, which is a fancy way of saying something that can be either `true` or `false`. There are a couple of weird things like 'null' and 'undefined' (we'll talk about those eventually). There is a new data type introduced in ES6 called a Symbol. Altogether, these are known as primative values. There is one more type, but calling it one type belies the complexity of it. This is the Object type.

Objects, in JavaScript, are a collection of properties. What does that even mean? Anything more complex than a primative is an object. This includes arrays, dates, maps, JSON (important, but not for today), and functions. Yes, functions are objects. And objects are a data type. And data types can be stored in variables. In JavaScript, functions are first-class citizens. This probably doesn't mean anything to you yet, but it is very powerful. It means that you can pass functions, as arguments, to other functions. I am just realizing that this is the chapter on data types, and we should have the first-class function talk when we get to the chapter on functions. Just remember that it is powerful and awesome. Let see some data types!

```javascript
"data" // string
5 // number
true //boolean
null // object
undefined // undefined

[1,2,"a","b"] // object
{name: "Sean", age: 40} // object
function (p) {console.log(p)} // function
```

You might have noticed I left out symbols. We'll come back around to it. And didn't I say null was its own type? It is one of the primatives, but through a quirk in the language it returns a typeof `object`. Have I mentioned that JavaScript has quirks? There are also only three examples of objects. Each of those types has a more specfic name too. The first one is an array, the second is an object literal, and the last one is a function.  Functions are technically function objects, but typeof on a function just returns function.

I used a new term a couple of times up there, and it turns out it is another keyword, 'typeof'. It is an operator that returns the type of the operand, as a string. It is useful, although not as useful as it could be. 

```javascript
typeof true // returns 'boolean'
typeof undefined // returns 'undefined'
typeof 5 // returns 'number'
```

Why I haven't told you to try any of this stuff on your own before now is a mystery. The best way to learn is to do, so it is time to do. Open your terminal, either standalone or the one inside VSCode (ctrl-~). Type `node` and hit enter. You are now in the node repl. A REPL is a Read-Eval-Print Loop, which is a fancy way of saying it will let you run javascript code. If you need to exit the REPL, hit ctrl-c twice. Type in any of the lines from the last block (stop before the //) and hit enter. You should get the same results I did. The REPL is a handy tool. It can be used simply, to check if some javascript is doing what you think it should be doing, and in more complex ways as well. If you see some code you want to try, the REPL is a good place to check.

JavaScript is not type-safe. You do not have to declare what type of data you are going to store, or use, or accept. It also uses type coercion. Many people hate this. Many people love this. Let me give you a pretty common example.

```javascript
  let userInputOne = "1"
  let userInputTwo = "2"
  let addedInputs = userInputOne + userInputTwo // expecting 3, we actually get '12'
```

What is going on here? We may have thought we were going to get numbers but instead got string representations of numbers. Then we thought we were using the addition operator (+) but it is an overloaded operator. When it is used between strings it becomes the concatenation operator. Concatenation is the act of linking things together. Great for building strings, not so great for performing addition. Now that we know those are strings, it makes sense. Let's try something else.

```javascript
  let userInputOne = 1
  let userInputTwo = "2"
  let addedInputs = userInputOne + userInputTwo // still expecting 3, we still get '12'
```

What happens in this case? Our first value is a number, so shouldn't it just blow up? Obviously `+` can't be both addition and concatenation at the same time. But it doesn't blow up. It gives as the concatenated string, again. How? Well, our number got implicitly coerced into a string. This will happen to you. You will scratch your head and wonder why the math isn't mathing. Then you will remember this lesson, crack a wry smile, and fix the issue quickly.

Can strings get coerced into numbers? Yeah, let's see how.

```javascript
  let userInputOne = 4
  let userInputTwo = "2"
  let multipliedInputs = userInputOne * userInputTwo // no idea what to expect, genuinely surprised when we get 8

  //also works if none of the inputs are numbers, as long as they can be coerced into numbers
  let three = "3"
  let six = "6"
  let times = three * six // 18
```
This is way less likely to happen to you. You might even be tempted to use this implict conversion to your advantage. I would suggest you do not rely on it. Any time you want to convert types, do it explicitly, using the built-in methods. It will make your code better, and more importantly, it will make your code more readable.

Strings, numbers and booleans should suit you in almost every case, for simple data. When you want to start grouping data, you reach for the objects. Arrays in JavaScript are a simple collection of comma-separated values. They do not have to be of the same type, and can, in fact, be of any type.

```javascript
[1,2,3,6,7,10]
["a", "z", "r"]
[true, false, false]
[1, "1", true]

[1, [2,3], {name: "sean"}, false, [{project: "iron hand", status: "suspended"}, 24, "aprs"]]
```

Object literals are a collection of key:value pairs.
```javascript
{make: "Ford", model: "Taurus", year: 1987, miles_driven: 275203}
// the value can be a primative, as above, or an object
{username: "Tom", address: {street: "Fairchild", number: 217}, phone_numbers: [5551212, 5552121]}
```
Arrays, object literals, and functions are the workhorses of JavaScript.

Functions are a special kind of object, but they are still objects. They aren't used to hold data, but they can _be_ data. We'll cover functions next.