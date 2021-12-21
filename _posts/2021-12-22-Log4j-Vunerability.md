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
