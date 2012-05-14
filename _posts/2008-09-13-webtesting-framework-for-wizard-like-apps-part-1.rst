--- 
layout: post
title: WebTesting Framework for wizard like apps - Part 1
wordpress_id: 166
wordpress_url: http://tmayad.loonyb.in/?p=166
date: 2008-09-13 12:03:25 +05:30
---
.. -*- mode: rst -*-

This isn't an original idea. But I have my own two cents to add and here goes.

The project I'm working on has a website with a wizard like interface where you enter your details as required on each page and click continue to go through to the last page of the wizard.

Here are some ideas for you if you want to test such a site. You can use selenium_ or any other web testing frame work to do the actual driving. What I'm proposing is a layer above that specific for the web site. Confused already? stay with me, I'll try to make it all clear in a bit.

First of all we need an answer class. It contains all the answers you need for your flow through the wizard. I prefer to keep it flat, but some people like to keep it a collection of objects according to logical section/page.

It is hard to continue like this, isn't it? Let's take an example. :) That will make it much easier.

.. _selenium: http://selenium-rc.openqa.org/
