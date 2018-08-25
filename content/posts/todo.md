+++ 
draft = true
date = 2018-06-26T17:03:00-07:00
title = "TODO LIST"
slug = "" 
tags = []
categories = ["Todo", "Draft"]
+++

---

1.  review docker. alpine. builder pattern. security+size. CI flow. building images. pulling images.
2.  SQL vs NoSQL. Cassandra vs MongoDB. Cassandra pros and cons.
3.  microservices. api gateway. service discovery -> DNS or registration/discovery. load balancing -> dedicated infrastructure or software like Ribbon. jwt. rest vs event/message based.
4.  how to contribute to open source projects. how to sell myself
5.  python: abstract class/method. [interface pattern](http://masnun.rocks/2017/04/15/interfaces-in-python-protocols-and-abcs/). magic methods. [context management](https://jeffknupp.com/blog/2016/03/07/python-with-context-managers/). [python try-except best practice](https://www.google.ca/search?q=python+try+except+best+practices&oq=python+try+except+best+p&aqs=chrome.0.0j69i57.3454j0j7&sourceid=chrome&ie=UTF-8)
6.  update about page for this Github page

# Note

- async/await introduced in 3.5
- async generator introduced in 3.6
- type hinting function annotation works from 3.5+
- type hinting variable annotation was introduced in 3.6

django personal best practice

- view: handles requests. retrieves request data, header, info
- service: handles business logic. work with DTOs. interact with data access objects
- DTO serializer/mapper: handles parsing of request data and building DTO objects
- template: handles view logic
- model: bare minimum. POCO class
- testing: utilize Django testing a lot, since all tests are done on a disposable testing database
- type hinting: along with abc(abstract base class) write interface utilizing codes
