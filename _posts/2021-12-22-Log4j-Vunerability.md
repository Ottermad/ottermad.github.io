---
layout: post
title: Log4j Vunerability 
author: Charles Thomas
---

The other weekend my Twitter blew up with references to some kind of vunerability in something called Log4j. Based on the amount of tweets I saw I assumed it was bad but I had no idea what Log4j was or what had happened. This led me down the rabbit hole of trying to understand what was going on. This post serves to document what I found out.

# What is Log4j?
[Log4j](https://logging.apache.org/log4j/2.x/index.html) is a logging library for Java. This means it is used by many application in Java to write their logs (instead of just printing them with `System.out.println` like I usually do)

# What is the vunerability in it?
Part of what made this story hard for me to follow was that several vunerabilities were found in it in quick succession.

The first one has the catchy name CVE-2021-44228 which allowed attackers to run their code on other people's machines if that machine was using Log4j - this is known as Remote Code Execution (RCE).

This was followed by CVE-2021-45046 which discovered that the fix for original vunerability was not complete.

Finally, a little while later CVE-2021-45105 which is a different vunerability that allowed attackers to crash programs using Log4j. This is known as Denial of Service (DOS) attack.

# How does CVE-2021-44228 work?
The description on Apache's [website](https://logging.apache.org/log4j/2.x/security.html) describes it as "Apache Log4j2 JNDI features do not protect against attacker controlled LDAP and other JNDI related endpoints." That is a lot of acyronmns that I didn't understand so I'm going to start by breaking them down.

## JNDI
JNDI stands for Java Naming and Directory Interface. To understand what this means we first need to explain the term: Directory service.

A directory service is a service on your computer or network that allows you to map resources to names and then use those names to look them up. It's tech equivilent of a phone book. One of example of this is the file system on your local machine that allows you to find data by giving it a nice filename.

Because there are many kinds of directory services, Java provides an API that sits on top of them so you can access many different directory services in the same way. This is JNDI.

## LDAP
LDAP stands for Lightweight Directory Access Protocol and it is a way of communicating with a directory service. It is an open source standard so it can be used by a vareity of services.

## How the vulnerabilty works?
So now we know what JNDI and LDAP are, we can explore how the vulnerability can be exploited.

Log4j allows you to interpolate values into the strings you log. This is to allow you log the values of variables or other useful pieces of data.

Because of this it is possible to log values then user has sent to you. For instance, you might log the value of a HTTP header from a request in order to debug something. This means you're writing whatever the user put in that header to that string.

By default Log4j would attempt to interpret certain values in a special way. If the value you're interpreting started with `jndi:ldap//` - it would realise that the string is a reference an object that can be accessed via LDAP using JNDI. So to be helpful it would attempt to look up that resource at the location specified by the string.

This means an attacker can make your code look a resource on an LDAP server controlled by them.

Now when log4j recieves the resource it attempts to deserialise it. Now if the resource it attempts to deserialise is a Java class it will end up executing some this code. This means that there is now a way of executing random code from the internet in your machine.

# Summary
So in summary, people using affected Log4j and that were logging user's input gave attackers a way of running arbitary Java code on their machine. 

Due to how popular this library is it has worried the entire community.

# Useful links
* [Log4j Security Page](https://logging.apache.org/log4j/2.x/security.html)
* (Explanation from JFROG](https://jfrog.com/blog/log4shell-0-day-vulnerability-all-you-need-to-know/)
* [LDAP](https://en.wikipedia.org/wiki/Lightweight_Directory_Access_Protocol)
* [JNDI](https://en.wikipedia.org/wiki/Java_Naming_and_Directory_Interface)
