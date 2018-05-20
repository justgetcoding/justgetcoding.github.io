---
layout: post
title:  "Learning Javascript VII - Statements"
date:   2017-08-15 12:10:45 -0800
categories: intro
image: pic02.jpg
author: "Sean Hornsby"
---

{{ page.title }}
================
{{author}}

Now that we know how to assign variables, and how to write functions, it is time to open the toolbox and see what is inside. JavaScript comes with some handy tools that we can use to do. These are mostly conditionals and loops, and there aren't actually that many.

#### If
The if statement performs a comparison and _if_ that comparison evaluates to true, the body of the statement runs. We need to learn the comparison operators too. Remember `=` is an assignment operator. If you try use it in a comparison, it will not work correctly. How then does one test for equality? `==` and `===` are the equality and strict equality operators. Equality: `==` will try to coerce the types of both items and will return true if it can. Strict equality `===` will not.

`!=` and `!==` are the inequality versions of the above.

`>`, `>=`, `<`, `<=` are greater than, greater than or equal to, less than, and less than or equal to.

There are also a couple of logical operators that can be used to chain conditionals. `&&` is and, `||` is or. 

A note on strict and loose equalities. Use the strict version as your default. If you know you want type coercion to be ok, then you can choose to use the loose equailty.

```javascript
function reallyTrue(x,y) {
  if (x === y) return true
  return false
}
function kindOfTrue(x,y) {
  if (x == y ) return true
  return false
}
function greaterThan(x,y) {
  if (x > y) return true
  return false
}
function notEqualTo(x,y) {
  if (x != y) return true
  return false
}
function complexComparison(x,y,z) {
  if( x === y && y === z) return "x === z"
  return "x !== z"
}
// and so on...
```

#### Else

_Else_ is the back half of the _if_ statement. If you have more than one outcome, you can use else (but don't have to, see examples above). If you have more than two outcomes, you will use else. In the above examples I used a pattern that eliminates the need for else. I also did not wrap my statements in braces. I could have, and it would work fine. I would have, if they had been any more complex than they were. Let's see what that looks like.

```javascript
// This works exactly the same but could be said to read more clearly.
function reallyTrue(x,y) {
  if (x === y) {
    return true
  } else {
    return false
  }
}

// It is certainly how you should write if-else statements when they get any more complex
function moreIfs(x,y) {
  if (x > 0 && x < 100) {
    console.log("x is in range")
    if (y > x) {
      console.log("and y is greater than x!")
    } else if (y < x) {
      console.log("and y is less than x!")
    } else {
      console.log("and y equals x!")
    }
  } else if (x < 0) {
    console.log("x is below zero")
  } else {
    console.log("x is above 100")
  }
}
```

When I have exhausted the alternate possibilities, I end the _if-else-if_ with a simple `else`. This works, logically, because I know what state the data is in by elimination.

#### Switch

Switch is an alternative to _else if_. It can be clearer to read and reason about in some cases.



#### For

The workaday for statement is the jumping off point for some of the more complex statements in JavaScript. There are more elegant loops, but it isn't a bad idea to try it with a simple for loop first and after you have it working, decide if there is a better tool to use. A _for_ statement takes three expressions and a statment. The syntax can look a lot like a function declaration, but look closely and you will see the statements are separated by semicolons instead of commas. This will be the cause of many errors if you are not careful. The statements are, in order, an initialization, a condition, and a final-expression. The first time through the loop, the initialization is run, then the conditional is checked, if it evaluates to true, the statement body is run and then the final-expression.

```javascript
var strings = ["a", "b", "c"]
for (var i = 0; i < strings.length; i++) {
  // do something fun with i
  console.log(strings[i])
}
```
In this loop, we are going to count up, starting with the initialized value, 0, and walk up until `i` is no longer less than `strings.length`. We didn't talk about it, but the data types have some methods and properties associated with them. Array has a property, length, that tallies the number of items in the array and returns that as a `number`. In this case, strings.length evaluates to 3. The final-expression, `i++`, is an incrementer. It adds 1 to the current value of `i`. Here is a table of the associated values as the loop runs:

| _i_ | strings[_i_] |
| --- | --- |
|  0  | "a" |
|  1  | "b" |
|  2  | "c" |
|  3  |  -  |

The loop begins and i is set to zero, that is less than 3, so the body runs. The value at the 0 index of the array _strings_ (that's what strings[0] means), is the string "a", so it is logged to the console. The body is finised, so the final-expression runs, incrementing i to 1. 1 is still less than 3, so the body runs again, this time logging the value of strings[1], "b", to the console. Final-expression runs again and now i is 2. 2 is less than 3, so the body runs, logging the value of strings[2], "c", to the console and then final-expression runs again, setting i to 3. 3 is _not_ less than 3, so the loop stops.

Hopefully that all makes sense. There are other loop constructs that we will talk about in a future lesson, and more advanced ways to use the simple for loop, but this is enough for now.

#### While

While loops operate similarly to for loops. Unlike a for, they have no initializer or final-expression. This means you have to create the value for the initializer outside the loop. Incrementing (or decrementing, or changing in whatever way) the evaluated value is also up to you.

```javascript
var strings = ["a", "b", "c"]
var n = 0
while (n < strings.length) {
  console.log(strings[n])
  n++
}
```

This produces the same output as the for loop above. Be aware, the value of `n` has been mutated. After the loop has run, n will equal 3, in this case.

#### Do (while)

Do...while is a flipped version of the do loop. It is guaranteed to run once. 

```javascript
var strings = ["a", "b", "c"]
var n = 0
do {
  console.log(n)
  console.log(strings[n])
  n++
} while (n < strings.length)
```

