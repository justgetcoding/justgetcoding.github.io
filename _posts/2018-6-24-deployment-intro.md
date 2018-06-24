---
layout: post
title:  "Deploying To The Web - Part I"
date:   2018-6-24 10:10:45 -0800
categories: intro
image: pic02.jpg
author: "Sean Hornsby"
---

## When Frustration Is Helpful

When I started conceptualizing this article, I naively thought it was going to be fairly easy to write. A friend online wrote:
>Can't wait for the day when I actually use both languages - PHP and JS - to create something pretty.

I see this sentiment fairly often, and I remember feeling the same way. I know how helpful it is to look at your development work in the "real" world. I also think it is helpful to pull back the curtain a little and see what it takes to get those concepts from abstract code pieces to a functional website. There is a lot of "magic" involved, and anything I can do to demystify that side of it will be a bonus. 

I find the best way to understand what is going on is to get it working and then break down the hows and whys. And that is where I got stuck. My assumptions (that it would be easy to write this article and that I know these tools) crashed into my reality. They did so in the best ways possible though.

To help this make sense, first I need to talk a little about myself. I am not a formally (classically?) trained programmer. I used freeCodeCamp, CodeSchool, Codecademy, and other online resources to teach myself the basics and then finished off at a 12 week bootcamp. It has been almost 2 years since I graduated. I currently work as a web developer at a clothing company. At work, we have a deployment strategy and environment in place, and I lean on that way more than I realized.

Setting up a development environment often involves installing things on your computer, setting them up, and then not touching them very often. A lot of times those things will interact with other things that you also hardly ever deal with. What this can mean, practically, is that I can ask you to do something like install a tool and that can fail for you in ways it does not fail for me. Furthermore, I might not even know why it fails for you or how to fix it.

You see, when I got to the section on using framework tools to quickly get a website up and running, the tool refused to install. Each of the frameworks (Vue, Angular, React), has command-line tools, and I find them tremendously helpful. There are a lot of caveats with that opinion, and I will get into them later. When I ran the command to install the vue-cli, it spent some time churning away and then errors started appearing in my console. They mostly involved missing files in the staging environment for nvm. If you are a code newbie, that probably makes no sense to me. While I understand the problem, I don't know, offhand, how to fix it. 

My article was no longer easy to write. In fact instead of writing my article I was now troubleshooting my whole setup. Was the problem that I have a mishmash of tools installed in various ways (curl, npm, brew)? Probably. Is there an easy fix? A quick google search tells me no, my problem is not some simple thing I overlooked. Not being able to use this tool, and more importantly, teach others how to use it, was derailing my whole article.

It was also very frustrating. It turns out, this frustration was the real lesson for me in all of this. The more frustrated I got with this problem, the more it brought back being a code newbie myself. Following along with a tutorial and then hitting some error that made no sense to me and was not part of the tutorial at all. Having to stop that flow of excited discovery. Troubleshooting these problems is often a cascade of additional frustration as you stumble upon one outdated solution after another. Most of the time, the solutions themselves are more complicated or terse than a code newbie is prepared for, which requires even more searching and scrabbling.

As developers, should we know our tools? Absolutely. But they represent a barrier to entry that can be tough to scale when all I want to do is see my basic html, css and javascript come together inside a browser in some way that approaches a real-world system. Sometimes I just want to get things going so I can examine the parts for a fuller understanding. I know that it is a bad idea to rely on "magic" permanently, but I think it is very valuable to be able to use it to teach myself the tricks. Remember, everything about this is "magic" to some degree at some point in our learning process. Somewhere down the chain, most of us stop understanding the how and why and just rely on the fact that it works (most of the time). Should I have to understand how transistors work together to perform logical operations with 1s and 0s? Should I need to understand how doping superconductors works?

As we progress as developers, our knowledge and experience will help us become frustrated less often, but it is important to remember what it was like when we were new too.

How did I solve my problem? I weighed my options. On the one hand, a deep dive into why npm install was failing, probably including uninstalling and reinstalling a lot of things repeatedly until I hit the magic permutation. On the other hand, I could try using yarn and see what happened. The yarn solution sounded way easier so I gave it a go. It wasn't perfectly smooth sailing, but the problems I encountered were simple to fix, and now I am finally back on track with my "easy" article!

> Written with [StackEdit](https://stackedit.io/).