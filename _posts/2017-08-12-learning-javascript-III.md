---
layout: post
title:  "Learning JavaScript III"
date:   2017-08-12 10:10:45 -0800
categories: intro
image: pic02.jpg
author: "Sean Hornsby"
---

{{ page.title }}
================
{{author}}

I think a logical place to start is variables. You saw some variable assignment in the last post. In ES5 it looks like this:

`var beverage = "coffee"`

`var` is a keyword, and those are actually pretty important so let's talk about them first. Keywords tell the runtime that you are about to do something special. There are 33 reserved keywords with about that many more in various stages of implementation. Later we will get to how JavaScript is parsed, using terms like lexical grammar, but for now, just know there are certain words that are reserved because they 'do' things in JavaScript. Here are the three we are going to talk about _right now_: `var, let, const`.

A short aside inside the aside. JavaScript is less strict than other languages. There are a lot of ways to write code. Over time, people have learned that there are good ways and bad ways. There are a lot of opinions about this. The short version is, I will show you what can be done, and then I will show you ways it should be done. 

All three of these keywords declare variables. `var` is the 'old way,' and it is the most general version. For a long time `var` was the only way to explicitly declare a variable. It can be reassigned and accessed from nearly anywhere in the program. It can act goofy in certain situations. These days we have better keywords to handle variable, and you should really only use `var` when you need to.

Speaking of horrible ways to do things, there is another way to declare a variable that is even worse. You can implicitly declare a variable by just assigning a value to a word.

```javascript
age = 40
function globalCreator () {
  height = 69
  name = "Sean"
}
```
This will work, but it is bad practice. All of those variables have been stored globally. Why is that bad? The short version is that you will lose track of what can manipulate (mutate) that data and eventually that will cause a problem that is hard to track down. In addition, it makes the intent of the code unclear. Writing clear code is so important that I will say it again, now, before it even means anything to you. Writing human-readable code is the most important consideration when deciding how to write your code. We will get back to that later.

```javascript
var age = 40
function scopedVariables () {
  var height = 69
  var name = "Sean"
}
```
This is better. In the end, nothing changes for age, it is still a global, but at least the intent is clearer. The `var`s inside the function declaration are scoped to that function. They are inaccessible outside the function. This is a good thing. 

Creating a variable involves two steps that are often done in one line, but can (usually) be done separately. These are declaration and assignment. The keyword `var` starts the declaration and the operator `=` starts the assignment. The way this is parsed by the computer is not the way it is probaly parsed by your human brain. I am honestly not sure how important this is right now, but I am going to cover it because it can lead to unexpected behavior.

This is a behavior called `variable hoisting`. JavaScript takes several passes over your code before executing it. Variable declarations are processed in the first pass. Assignments are processed later. This happens even if they occur in the same line of code, but it is more mind-bending when it happens over several lines of code. That's the simple version, here's an example straight from MDN:

```javascript
bla = 2;
var bla;
// ...

// is implicitly understood as:

var bla;
bla = 2;
```

Like I said, not all that important right now, but hoisting can give you some trouble. The recommendation is to always declare your variables at the top of their scope. This is one of those "opinions." It happens to be a good one.

In ES6, we have two new variable keywords, `let`, and `const`. `let` is a lot like `var`. It can be declared without initialization. It can be reassigned and mutated. Unlike `var` though, `let` has a limited scope, and it won't create a global property, even when declared in the global scope. This won't mean anything to you now, but eventually it will make sense. It is almost always better to use `let` than `var`.

We also get access to `const`. Think of this as `constant`. They must be initialized at declaration. They cannot be reassigned or redeclared. They can be changed in very specfic ways (properties and methods can be added), but generally they are safe from mutation.

Another opinion incoming. Use `const` wherever possible. Use `let` when you can't use `const`. If for whatever reason you can't use `let`, then fall back to `var`.

In the end, the important thing to realise is that all three of these words are used to declare and assign variables. In most cases you can think of them interchangeably. These are essentially equivalent:

```javascript
var a = "a"
let b = "b"
const c = "c"
```

There are many types of data that can assigned with all three of these keywords, and we'll take a look at those types next.

------------
MDN Lexical Grammer (keywords) https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar