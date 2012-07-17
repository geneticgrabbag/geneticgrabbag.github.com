---
layout: post
title: "Background Processing in a Spring Web Application"
date: 2008-05-01 17:46:14
categories:
- personal
- technology
- computing
- software-development
---
From the "Huh, well that's cool" department...

Today I figured how to run a background process from within a web application
that utilizes Spring 2.0 or greater.  At first, I investigated all sorts of
ways of adding multithreading to a web application before stumbling upon this
gem.

The key is that Spring provides a class, TaskExecutor, that allows you to run
a background task by simply creating a class that implements the Runnable
interface and hooking it up to your application with some simple configuration.

In short, as Spring allows Java web developers to program using POJOs and not
against a set of interfaces, TaskExecutor and its cohorts allow us to do
background processing using simple classes instead of forcing us to handle the
ugly details of multithreading and synchronization ourselves.

Thanks, [Spring dudes](http://blog.springsource.com/main/)!  Once again, you
save the day.

See [ Chapter 23](http://static.springframework.org/spring/docs/2.0.x/reference/scheduling.html#scheduling-task-executor-usage "Chapter 23")
of the [Spring Framework documentation](http://static.springframework.org/spring/docs/2.0.x/reference/ "Spring Framework documentation")
for more information.
