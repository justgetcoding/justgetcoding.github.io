---
layout: post
title:  "Learning JavaScript II"
date:   2017-08-11 10:10:45 -0800
categories: intro
image: pic02.jpg
author: "Sean Hornsby"
---

{{ page.title }}
================
{{author}}

Ok, here we are. You have hopefully installed an editor, along with node, and you are ready to go. Maybe we should take one more beat to try and get ahead of any confusion. You are learning JavaScript. You will also hear it refered to as ECMAScript, and sometimes that will be shortened to ES and appended with a version number. Currently you will see ES6 being bandied about. What is all this stuff? ECMAScript is the standardization of the JavaScript language. The currently standard version of the, um, standard, is ES5. The currently hot version of the standard is ES6. ES6 isn't completely supported in browsers, but it can be transpiled back into compliant ES5. They are standards, so they move at a somewhat glacial speed. ES6 was finalized in 2015, ES7 in 2016, and ES8(!) this year. We will be focusing on a lot of the ES6 features.

That paragraph went on longer than I thought it would. None of it is all that important, to you, right now. I just want you to know that if people talk about ECMAScript or ESwhatever, they are talking about JavaScript. Now you know.

Let's have a look at some JavaScript

```javascript
var x = 4;
var y = 12;

function adds(x,y) {
  return x + y;
}

adds(x,y) // 16

```

That is good old ES5. There are two variable assignments using `var`, one function declaration using the `function` keyword. The function is named `adds` and it takes two parameters; x and y. The function body returns the result of adding x and y together. The last line is where I invoke the function, passing in two arguments, the previously declared variables x and y. This is simple, straightforward JavaScript.

If I was writing this today I would use ES6 and it would look like this:

```javascript
const x = 4
const y = 12

const adds = (x,y) => x + y

add(x,y) // 16
```
I have replaced `var` with `const`. I use a function expression, assigning an anonymous fat arrow function into to the const `adds`. I also skipped all the semicolons. Don't worry if that seems like a lot of differences. It will become clear as we move through the lessons. I didn't even mention partial application, currying, and immutability!
