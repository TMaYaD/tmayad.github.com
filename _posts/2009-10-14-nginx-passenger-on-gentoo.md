--- 
layout: post
title: nginx passenger on gentoo
wordpress_id: 394
wordpress_url: http://tmayad.loonyb.in/?p=394
date: 2009-10-14 12:50:42 +05:30
---

A few days back my slice started giving me warnings about heavy swap
usage and my websites started crawling dead slow despite very low
traffic. [top](http://en.wikipedia.org/wiki/Top_(Unix)) gave me the
answer I needed. [Apache](http://www.apache.org/) is eating away a lot
of memory without doing anything. I've been hearing a good deal about
[nginx](http://nginx.net/) and wanted to give it a try.

Recently I've been working on a rails project and needed to deploy it.
Looking at rails guides pointed me to
[passenger](http://www.modrails.com/) for nginx. How ever the nginx
ebuild for portage doesn't support passenger. Some one has raised a
[bug\#266446](http://bugs.gentoo.org/show_bug.cgi?id=266446) and created
a patch for adding *passenger* use flag to nginx. There is one small
catch though, it raises a sandbox violation error. Besides it needs
passenger to be installed using ruby gem. A quick scan at the end of the
build log showed the error. nginx is trying to prepare passenger through
some rake task and causing the error.

I decided to write an ebuild for passenger and prepare it for nginx. A
quick google search and looking at a couple of other ebuilds threw up a
standard ebuild template for gem installations. A simple rake task later
I got my
[passenger222255eebuild](http://bugs.gentoo.org/attachment.cgi?id=205845)
and a [patch for nginx
ebuild](http://bugs.gentoo.org/attachment.cgi?id=205847&action=diff) to
go with it.

They are up on Gentoo bugzilla, grab them and place them in your
overlay.
