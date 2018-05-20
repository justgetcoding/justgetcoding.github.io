---
layout: post
title:  "Learning Javascript VI - Functions"
date:   2017-08-14 12:10:45 -0800
categories: intro
image: pic02.jpg
author: "Sean Hornsby"
---

{{ page.title }}
================
{{author}}

Functions are the engine which drive our programs forward. They are where the parts start to come together into machines that do some kind of work. As such, you can be assured there are a lot of opinions about them. We'll be spending a lot of time talking about functions.

There are 2.5 normal ways and one 'advanced way' to create functions. This is JavaScript, so read that with one huge caveat. There are many variations on those ways. Having half a way is weird, so let's tackle that first. You can use the function construtor to create functions but you probably never will. The constructor takes a series of arguments, followed by the function body. It is the least elegant way to write a function.

```javascript
var multiplier = new Function('a', 'b', 'return a * b')
```

The other choices are _function declarations_ and _function expressions_. Function declarations just declare a function. You start with the keyword `function`, add a name (if you want), a list of parameters inside parens, and then the function body inside braces. A function expression is what happens when you declare a function on the right hand side of an expression. It looks a lot like variable assignment, and that is because it is variable assignment.

```javascript
// declaration
function divider(x,y) { return x / y }
// can be written anonymously 
function (x) { return x }

// expression - quite often written anonymously
var doubler = function (x) { return x * 2 }
// but can use named functions also
var tripler = function tripler (x) { return x * 3 }

```

Things to be aware of. Function expressions are not hoisted. This means that you cannot try to use that function before you define it. Function declarations are. As long as a function is declared in the scope, anywhere, it is usable. This might sound like a deal breaker for expressions, but all it really means is that you have to organize your code in a certain way (define function expressions before you use them), and since organizing code is already important, hoisting isn't that big of a problem.

Also, functions do not have to fit on one line like the above examples.

```javascript
var longerFunction = function(x,y,z) {
  var summed = x + y + z;
  var doubledSum = summed * 2
  return doubledSum;
}
```

Furthermore, ES6 allows us to use an additional type of function, colloquially called a fat arrow function.

```javascript
// verbose
var myFirstFatArrow = (x) => {
  return x * 2
}

// terse
var mySecondFatArrow = x => x * 2
```
Those functions do the same thing. The first one looks similar to the function expressions you have already seen. Instead of using the `function` keyword, they just list the parameters, followed by a fat arrow ( => ), and then the function body. If there is only one parameter, it doesn't need to be enclosed in parens. If the function body sits on the same line, without braces, the `return` keyword is implied. They look funny at first, but they start to make sense pretty quickly. There is another (big) difference between 'normal' functions and fat arrow functions that has to do with the `this` binding, but since we haven't talked about `this` yet, we'll continue to ignore it for now.

The last step is 'running' the functions. We do that by invoking them. Invoking a function is as simple as writing the function name and following it with a set of parens. Inside the parens are our arguments (that will hopefully match up with the defined parameters).

If we take some of the functions from above, this is how we would use them:

```javascript
divider(6,3) // returns 2
doubler(22) //returns 44
mySecondFatArrow(22) // also returns 44
```

One last thing, we are going to be running our js files through node, just to test them out. In order to actually see any output in the console, we need to log the values to the console. That is done with a global function called `console.log()`. You put whatever you want to see inside the parens.

```javascript
// easy way
console.log(divider(6,3)) // logs 2 in the console

// longer way
var result = divider(6,3)
console.log(result) // also logs 2 in the console
```

Write a few functions. Try all of the different styles. See if you can write the same function. Open your editor, create a new javascript file called `functions.js`, and have a go. When you have written and invoked a few functions and want to see if they work, save the file, head to the terminal/console, and type `node functions.js`. If you don't see any output, make sure you are using console.log().

Take some time to play around with it. We're going to explore some of the tools availble to us next. 