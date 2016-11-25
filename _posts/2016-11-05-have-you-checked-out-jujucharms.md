---
layout: post
title: Have you checked out Jujucharms?
---

Over the past month, I have been exploring various PaaS providers in the market to study how they package and present their PaaS offerings to the users differently, when someone at work pointed out [Jujucharms](https://jujucharms.com/) by [Canonical](http://www.canonical.com/) (the same company behind Ubuntu). And taking a first look at it - I immediately liked it, just because of the clear and simple way in which they have presented application and service modelling.

Quoting for their website, "Juju is an application and service modelling tool that enables you to quickly model, configure, deploy and manage applications in the cloud with only a few commands. Use it to deploy hundreds of preconfigured services, OpenStack, or your own code to any public or private cloud."

You can explore the modelling tool yourself [here](https://demo.jujucharms.com/). As an example, I have a WordPress model setup with the Wordpress nodes scaled to 3, one apache node acting as a reverse proxy to the wordpress nodes, a mysql master database connected to the wordpress nodes and a slave mysql instance.

![Wordpress model](http://i.imgur.com/Wp7j3FM.png)

The best thing about this is when you deploy, Juju will take care of all the configuration required at the various nodes. (In the above example, the reverse proxy will be configured to point to the wordpress nodes, the slave database will be configured to replicate from the master database, etc.)

Once done with the modelling, you can deploy the models you generated for your applications and services to any of the public cloud platforms supported by Juju. 

![Public clouds supported by Juju](http://i.imgur.com/5adWXku.png)
