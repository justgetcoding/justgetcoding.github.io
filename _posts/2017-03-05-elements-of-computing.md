---
layout: post
title:  "Elements of Computing - Intro"
date:   2017-03-01 10:10:45 -0800
categories: intro
image: gates.png
author: "Sean Hornsby"
---

{{ page.title }}
================
{{author}}

![Splash](/images/EoC1.png){:class="img-responsive"}

As a programmer with no formal training, I am always looking for ways
to pick up more CS fundamentals. Getting practical programming concepts is "easy,"
just start working on projects. You will develop some sort of competence rapidly.
However, there are a whole lot of topics that you may have skipped over, had no
time to learn, or just didn't understand quickly enough. Algorithms are one of these
topics (one I cover in other posts). At an even lower level, perhaps the lowest level, is
the topic of how computers compute.

I was fully aware of my ignorance on that subject, but also satisfied that it wasn't necessary
to learn all of that CS stuff in order to be a good programmer. I still feel like this is
probably true, but I've come to realize two things. First, I don't want to be a good programmer,
I want to be a great programmer. Second, it is going to help get better at acquiring every other
skill I want/need. Anything that makes programming less mysterious, makes the programmer more
powerful.

My brother told me he had been working through a course on building a computer from the ground up
and that he thought I would find it interesting. That was yesterday, and I haven't been able to stop
working through the problems and reading the material. Far from being academically dull or too mathematically
advanced, it has been engaging and surprisingly simple, at first. the challenge level ramps up. The more
I completed, the more I began to think about how I could apply these lessons on a broader level. Over
the next weeks, I am going to be writing a series on this course and my progression through it. 

The course is called "Building a Modern Computer from First Principles," and is referred to as, "Nand2Tetris," and
everything you need to follow along is <a href="http://www.nand2tetris.org/">here</a>.

Tools I am using include:
* [VSCode](https://code.visualstudio.com/download)
* [Logic.ly](https://logic.ly/download/)
* The [software downloads](http://www.nand2tetris.org/software.php) from the nand2tetris project.

Before we jump into the project work, there are a few other things to cover. I am
mainly a JavaScript programmer, so the file formats involved were new to me. That
said, they use pretty straightforward syntax. Writing the code for the chips happens
in a Hardware Descritpion Language (HDL). The HDL files are run with the included
Hardware Simulator. Here is an example HDL file

```
/**
 * Not gate:
 * out = not in
 */

CHIP Not {
    IN in;
    OUT out;

    PARTS:
    // Put your code here:
}
```

It starts with a documentation comment block. First line is the type of chip. The next
lines (only one in this case) describe the logic of the chip. Here, for the Not Gate,
'out' should equal the opposite of in.

Next is the implmentation. We are making a new CHIP called Not. Then we declare the
inputs and outputs of the chip. These are the parts that will be exposed, the interface.
PARTS will hold the logic. Throughout the course, we will be building up a library of
parts that we can then use in successive chip programs.

Once the chip is built, we can open it in the Hardware Simulator and run its tests. Let's
take a look at the HS now:

![Hardware Simulator](/images/HS-intro.png){:class="img-responsive"}

Load the chip in by clicking the chip icon in the top left or using the File dropdown.
Load the test by clicking on the scroll icon (next to the red flag) or 'Load Script'
in the File dropdown. Run the test by clicking on the Run button or selecting Run from
the Run dropdown (how many times can I say run in one sentence?). Messages show up on the
very bottom of the simulator. What you are looking for is "End of Script - Comparison
ended successfully." This is just an overview, we'll cover failures and other messages
in another post.

That's it. That's all you need to follow this course. I use one more tool for convenience,
a program called Logicly (linked above). It makes visualizing and actualizing the chips
a bit more user friendly. It has a free 30 day trial, and has helped me tremendously. I
will cover its use in a separate post.