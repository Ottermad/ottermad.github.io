---
layout: post
title: Musing on Microservices
author: Charles Thomas
---

Microservices have been commonplace among technology companies of all sizes and in this post I hope to explore some of the pros and cons of them and what you consider when thinking about whether or not they are a good choice for the problems you're solving.

Let's start by quickly addressing what are microservices? Microservices are a way of structing your application so that instead of having one big application (referred to as a monolith), you have multiple smaller applications that communicate with each other over a network.

So now why might you want to do this? Generally, microservices set out to solve two problems: scalability (how can I make my application handle more load?) and availability (how can I keep my application serving requsts more of them time?). So let's deal with each of these issues seperately.

Microservices can help improve scalablity by allowing you run multiple copies of your app on different machines. However, you can do this with a monolith as well - just run more copies of the whole monolith (unless of course your application is so big you cannot reasonably run it as a monolith). Instead microservices provide a more subtle advantage: they allow you to scale different parts of your application differently. For example, you might have a section of your application such as authorization that has to process a very high number of requests where as another part of your application such as settings which has much lower traffic. In a microservices archetecture, you can scale these parts of your application seperately.

In principle, this is great - it allows you to scale parts of your application independently, saving you money on hosting costs and allowing you handle higher traffic loads easier. However, the important question to ask yourself is does this ability 
