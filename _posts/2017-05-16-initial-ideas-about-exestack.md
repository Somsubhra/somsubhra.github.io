---
layout: post
title: Initial ideas for exestack
---

So I have just kicked off writing an open source event driven code executor platform called [exestack](https://github.com/exestack) on Github. The idea behind the platform is to execute a piece of code on the cloud triggered by an event happening anywhere in the physical or the virtual world. The idea is very much similar to my previous implementation of [LambdaCloud](http://terracloud.india.endurance.com/) (which is closed source), which executes functions defined in python, ruby or php in response to events like database or file system writes.

So you can say this is some form of a re-write of the LambdaCloud platform, but with the following differences:

* I want to have a generic core web-hooks like platform which can collect all the events and probably queue them. The events handler would then make some form of a RPC or REST API call.

* I do not want to restrict code to be defined as functions in a few available runtimes. Rather I want to standardize the runtime - so the best option is to abstract it out using containers (docker comes to my mind here). So I'll provide a platform where the user can push code in the form of docker images and the platform should be able to spin off containers from these images and run them.

* I want to provide some sort of bridge layer where the actual RPC or the REST call happens from the web hooks platform to the container.

Basically with these concepts in mind, I have come up with the following modules:

* **controller** - To manage all the meta-data like user and project information, event wiring, etc.

* **eventengine** - To accept all the events from the physical and the virtual world and react to them according to the event wiring defined in the controller. (I have still not figured out how this wiring should look like)

* **dockyard** - Runtime to run the user defined code. This will basically use some form of docker / kubernetes / mesos - yet to come up with the best solutions.
