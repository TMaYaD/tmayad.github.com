--- 
layout: post
title: WebTesting Framework for wizard like apps - Part 2
wordpress_id: 237
wordpress_url: http://tmayad.loonyb.in/?p=237
date: 2008-09-29 23:25:50 +05:30
---
.. -*- mode: rst -*-

Time for the example I promised. Lets take a train booking web site for example. It is a typical example a web based wizard. Lets Consider IRCTC The flow goes something like this:

Home Page
---------
* To Station
* From Station
* Type of Journey (One Way, Return)
* Date of Departure
* Date of Arrival*
* Class

Time Table Page
---------------
* Outward (and Return) Train: Can be selected using
  - Name
  - Number
  - Time and Date of departure
  - Route
* Quota
* Date of Journey (We may want to change the earlier provided one depending on availability

Possible next pages:
* Schedule
* Availability
* Fare
* 



