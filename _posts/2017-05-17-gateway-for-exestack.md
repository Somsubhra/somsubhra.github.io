---
layout: post
title: Gateway for exestack?
---

One of the limitations of [LambdaCloud](http://terracloud.india.endurance.com) was that it only reacted to events and the execution to that was asynchronous. One of the most common use cases while writing applications is writing REST APIs over HTTP where you expect a response to the request on the same connection.

I would like [exestack](http://github.com/exestack) to support this particular use case, so I am thinking of writing a fourth module called Gateway just in front of Dockyard (the container runtime platform). This would basically mean code in Dockyard can be executed via two channels: Eventengine and Gateway.

Some features off the top of my mind that can be added to Gateway:

* authentication
* rate limiting
* documentation generation
