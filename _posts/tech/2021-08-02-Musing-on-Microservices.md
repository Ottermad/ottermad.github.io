---
layout: post
title: Musing on Microservices
author: Charles Thomas
---

Microservices are commonplace among technology companies of all sizes and in this post, I hope to explore some of the pros and cons of them and what you should consider when deciding if they are a good solution for the problems you're solving.

Let's start by quickly addressing a common question: what are microservices? Microservices are a way of structuring your application so that instead of having one big application (referred to as a monolith), you have multiple smaller applications that communicate with each other over a network.

So why might you want to do this? Generally, microservices set out to solve two problems: scalability (how can I make my application handle more load?) and availability (how can I keep my application serving requests more of the time?). Let's deal with each of these issues separately.

Microservices can help improve scalability by allowing you to run multiple copies of your app (often on different machines). However, you can do this with a monolith as well - just run more copies of the whole monolith  Instead, microservices provide a more subtle advantage: they allow you to scale different parts of your application separately according to demand. For example, you might have a part of your application such as authorization that has to process a very high number of requests while another part of your application such as settings has much lower traffic. In a microservices architecture, you can scale these parts of your application separately.

In principle, this is great - it allows you to scale parts of your application independently, saving you money on hosting costs and allowing you to handle higher traffic loads more easily. However, the important question to ask yourself is whether or not different parts of your application actually have drastically different scalability needs and does the ability to scale them separately outweigh the cost of the added complexity?

It's also worth asking what is currently limiting your ability to scale your application as a monolith? If it's CPU usage or memory, then perhaps, microservices may be a solution, however, you may be being bottlenecked by something else such as your database. In this case, microservices will not solve your problem, although the common pattern of having one database per microservice might help you. However, you can get the same effect by having your monolith connect to multiple databases.

Additionally, whether or not to use microservices isn't as much of a binary choice as it seems. Service-based architectures have been around for a while and you don't have to go the whole way and have thousands of microservices. If you have only part of your application that needs to deal with high traffic then you can just split out that piece of your application. Now while some people are worried about having to split out their application later I would make the case that for many people it is not too difficult to pull out a part of your application as long as you don't have complicated joins between tables that are not related (and if you do, this might be a sign of a different design problem).

When it comes to availability, a similar school of thought applies. Unless different parts of your application have different availability requirements, can you just run multiple copies of your monolith? And even if you have parts of your application that have high availability requirements will moving to microservices increase your availability? Running microservices in production can be difficult and introduces several more infrastructure components to worry about (e.g. a Kubernetes backplane) which, if they go down could reduce your availability. It is worth considering whether or not you really need such high availability and whether it is worth the cost of trying to achieve it? Perhaps it costs your business less to go down every now and again than it does to hire and maintain a team of DevOps engineers.

It's also important to think about compound failure when dealing with microservices. With a monolith, if at least one copy of your monolith is up 99.9% of the time (ignoring external dependencies such as databases) then your uptime is 99.9%. Now, imagine you have a microservices architecture with two services A and B which must both be up for the user to do anything. If both of these services are up 99.9% of the time then your total uptime is actually 0.999 x 0.999 x 100 = 99.8%. This difference may seem small but given that these compounds for each dependency you have, you can quickly have much lower availability than you thought. 

The other thing to consider when thinking about availability is failure modes. In a microservices architecture, you have more individual components, which means you have more combinations of things that can go wrong. This often makes it harder to reason about behaviour in the case of a bug or a crash. For example, if one service (service A) goes down but another (service B) stays up, on one hand, you can keep serving requests to service B, however, service A and B may now be out of sync with each other (for example, service B has consumed some event that service A hasn't) which now may lead to unexpected and confusing behaviour. In many cases, it is actually better for a failure to mean that your application just stops, rather than half processing requests.

The final thing to think about with microservices is what I'm calling: microservices as a design pattern. In some companies, microservices have become a way of managing code complexity. In some codebases where you might have a class, in others, you may now have a microservice. Now while this approach can work, if you are considering adopting microservices, for this reason, I would strongly suggest you consider whether or not it is worth the overhead of having to support such a high number of microservices. Instead you should consider whether the are design patterns or policies that can make your codebase easier to work with such as the use of interfaces or assigning teams to different sections of codebase.

Now microservices are not all bad and when implemented well they can be very effective but I hope I have provided some things to think about when considering whether or not they are the right architecture for your next project.

Further reading:
* [https://dataintensive.net/](https://dataintensive.net/)
* [https://www.theregister.com/2020/03/04/microservices_last_resort/](https://www.theregister.com/2020/03/04/microservices_last_resort/)
* Do you have any recommendations please let me know!
