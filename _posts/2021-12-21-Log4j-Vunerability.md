---
layout: post
title: Log4j Vulnerability 
author: Charles Thomas
---

The other weekend my Twitter blew up talking about a vulnerability in something called Log4j. Based on the number of tweets I saw I assumed it was bad but I had no idea what Log4j was or what had happened. This led me down the rabbit hole of trying to understand what was going on. This post serves to document what I found out.

# What is Log4j?
[Log4j](https://logging.apache.org/log4j/2.x/index.html) is a logging library for Java. This means it is used by many applications in Java to write their logs . Instead of printing them with `System.out.println` like I usually do)

# What is the vulnerability in it?
Part of what made this story hard for me to follow was that several vulnerabilities were found in it in quick succession.

The first one has the catchy name CVE-2021-44228 allowed attackers to run their code on other people's machines if that machine was using Log4j. This is known as Remote Code Execution (RCE).

This was followed by CVE-2021-45046 which discovered that the fix for the original vulnerability was not complete.

Finally, CVE-2021-45105 is a different vulnerability that allowed attackers to crash programs using Log4j. This is known as a Denial of Service (DOS) attack.

# How does CVE-2021-44228 work?
The description on Apache's [website](https://logging.apache.org/log4j/2.x/security.html) describes it as "Apache Log4j2 JNDI features do not protect against attacker-controlled LDAP and other JNDI related endpoints." That is a lot of acronyms that I didn't understand so I'm going to start by breaking them down.

## JNDI
JNDI stands for Java Naming and Directory Interface. To understand what this means we first need to explain the term: Directory service.

A directory service is a service on your computer or network that allows you to map resources to names and then use those names to look them up. It's the tech equivalent of a phone book. One example of this is the file system on your local machine that allows you to find data by giving it a nice filename.

Because there are many kinds of directory services, Java provides an API that sits on top of them so you can access many different directory services in the same way. This is JNDI.

## LDAP
LDAP stands for Lightweight Directory Access Protocol and it is a way of communicating with a directory service. It is an open-source standard so it can be used by a variety of services.

## How the vulnerability works?
So now we know what JNDI and LDAP are, we can explore how the vulnerability can be exploited.

Log4j allows you to interpolate values into the strings you log. This is to allow you to log the values of variables or other useful pieces of data.

Because of this, it is possible to log values the user has sent to you. For instance, you might log the value of a HTTP header from a request to debug something. This means you're writing whatever the user put in that header to that string.

By default Log4j would attempt to interpret certain values in a special way. If the value you're interpreting started with `jndi:ldap//` - it would realise that the string is a reference to an object that can be accessed via LDAP using JNDI. So to be helpful it would attempt to look up that resource at the location specified by the string.

This means an attacker can make your code lookup a resource on an LDAP server controlled by them.

Now when log4j receives the resource it attempts to deserialise it. Now if the resource it attempts to deserialise is a Java class it will end up executing some of this code. This means that there is now a way of executing random code from the internet in your machine.

# Summary
So in summary, people using affected Log4j and that were logging user's input gave attackers a way of running arbitrary Java code on their machine. 

Due to how popular this library is it has worried the entire community.

# Useful links
* [Log4j Security Page](https://logging.apache.org/log4j/2.x/security.html)
* (Explanation from JFROG](https://jfrog.com/blog/log4shell-0-day-vulnerability-all-you-need-to-know/)
* [LDAP](https://en.wikipedia.org/wiki/Lightweight_Directory_Access_Protocol)
* [JNDI](https://en.wikipedia.org/wiki/Java_Naming_and_Directory_Interface)
