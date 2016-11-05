---
layout: post
title: Application Hosting and Testing on RHC
---

I am always on the lookout for places where I can host my web applications(for free). Github pages doesn’t help here as they are meant for static content. Google AppEngine is cool, but not for me as I don’t like the way and procedures for hosting.

Today I discovered [OpenShift](https://openshift.com), which comes for a variety of application hostings, supports multiple technologies and not to mention: it it free. [OpenShift](https://openshift.com) is based on RHC(RedHat Cloud) and comes with a variety of features.

So, to get started you need to sign up for a free account of Openshift Online. Once done with that we have an online console which has a pretty good GUI for managing applications and adding cartridges(Cartridges stand for the modules on which our project will be based).

But I prefer the command line which appears easier and quicker than the GUI on the web. To get started we need to have git and rubygems installed. For this do the following(Please note that this applies for Debian only)

```
sudo apt-get install git ruby1.9.1 rubygems
```

After this is done do the following:

```
sudo gem install rhc
gem update rhc
```

After this is setup, we need to setup rhc for the first time by running:

```
rhc setup
```

During this step, there will be a request for setting up a namespace which is very important for hosting applications. Once this is done, run

```
rhc cartridge list
```

This will show a list of applications that can be hosted. These include node.js, PHP, python, Ruby and also addons like mysql, phpmyadmin, mongodb, postgresql. This also features a Jenkins build system and Cron(job scheduler).

To start a new application, for example PHP run the following:

```
rhc app create -a appname -t php-5.3
```

This will create an app remotely and clone a local copy. To further add addons like mysql and phpmyadmin run:

```
rhc cartridge add -a appname -c mysql-5.1
rhc cartridge add -a appname -c phpmyadmin-3.4
```

After setting up mysql and phpmyadmin, the credentials for using them are displayed on the command line. It might be useful to note them down.

Once all requirements have been added, we can add the contents of the application to the repository and simply commit and push.

The url for accessing the application is https://appname-namespace.rhcloud.com and phpmyadmin can be accessed at https://appname-namespace.rhcloud.com/phpmyadmin
