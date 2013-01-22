---
layout: post
tags: [Windows Azure, Consulting, Project]
title: "Six Months with Azure: Dos, Dont's and Oh hell nos"
---
{% include JB/setup %}

I figure six months is about the right amount of time to do a retrospective back on what you've been doing and figure out what went well, what didn't and what really didn't. It turns out I've been at the same client for the past six months and working with Windows Azure as well so it's pretty easy for me to tally the score. What I hope to do here is provide a list, in my brains order, of some of the things I wish I could tell myself 6 months ago.

Also as I was writing this post I realized that there's really two types information here, business and technical. I don't try to separate them out because they're all very important. As such feel free to skip around as you please.

## Open those ports

This was by far the most painful few weeks I've spent solving a problem. We were building a hybrid application that relied heavily on the Azure Service Bus. When we started and didn't have the luxury of using client provided laptops so we used our Pariveda provided ones. Since we didn't meet their security requirements and didn't want to go through the hub bub and whatnot of trying to get our laptops on their network, we used their guest wireless access points.

Turns out that their guest wireless network had lesser restrictions as far as network security than their corporate network. Debugging an application in the cloud is not easy right now, but debugging one that has networking issues and port conflicts? Forget about it. That leads me into the next lesson learned...

## Communicate early and often

It should be a no brainer but it really needs to be said. Open communication about the complexities of a project, *especially a project that is with a fairly new technology stack* is imperative. With the ports issue we had to go back and forth over several days/weeks incrementially getting more of them opened. We should have communicated better about what we were doing and the approach we were taking. It would have caused a lot fewer headaches.

Azure is big and complex enough that it's hard to fully understand for a person working full time with it. Imagine working full time on another project and then having to understand what some consultants are doing with it as well. Think of the client and what they must be thinking when you're going 10,000 mph and they're trying to keep up with what you're doing and their day to day tasks as well. One thing you can do to help out is...

## Use one common language and stick to it

With Azure changing so much and so fast it's hard to keep up. It's even harder when it's new enough that Microsoft is still trying to figure out their roadmap and the names of their offerings within Azure. The simple name change from "Hosted Service" to "Cloud Service" or "SQL Azure" to "SQL Database" is enough to confuse those on the same development team. Introduce another person(s) you have to communicate back and forth with on or about the project and you can easilly get some confused looks if you start changing the names around, or worse switch freely between names.

One way to combat the problem might be to use the first names that something is referred to as. I know Microsoft changed the name but internally it's easier to just use the same vocabulary. Maybe maintaining a dictionary of terms is easier for you. Figure out what works best for your team and stick with it.

## Get to Azure early and often

One of the things we realized is that things often aren't what they seem in the emulator. For simple projects the emulator works great and rarely hides any potential problems. But as soon as you start modifying the configs manually or messing around with nested sites or authentication/authorization, ssl, database and storage, etc, etc, you probably want to get your stuff into an actual Azure hosted environment ASAP. It's so cheap to have something out there for an hour while you bang away at it. Get it out there sooner than later and find any potential bugs early on.

## Make a deployment strategy

There are many many ways of deployment to different environments for Azure. Are you going to use Visual Studio to deploy or are you going to build packages and upload them to the portal manually? Are you going to use TFS, Team City or some other automated build strategy and use the powershell cmdlets to integrate with it? How are break-fixes going to work? Minor feature builds? Point is there are many different ways to get your stuff to the cloud, figure out what you're going to do early (it helps with the other sections!) and stick with it.

## Figure out your data persistance but don't be afraid to change it

One of the things we quickly learned was that for a high performance API like ours we couldn't rely on Azure SQL database to be there for us all the time. We were simply pushing it too hard for it to be reliable for us with its multi-tenant strategy. The fix for us was moving most of our data into table storage and using [eventual consistancy](http://en.wikipedia.org/wiki/Eventual_consistency). 

Choose a good data model that works for your domain. Just don't get to attached to it since it will most likely change with the requirements of your application. When those changes come re-evaluate your needs and what the current offerings of Azure are. You might find it's easier to change the model rather than shoving functionality into places it doesn't seem to fit.

## Get a thumbprint on the Azure community

You're going to be likely doing stuff that not many people have done before if at all. In those desperate times, use the community. Forums, blogs, twitter, etc. They're all there for you to use to your advantage. The cliche holds true, don't be afraid of asking a dumb question (mainly because someody might not have asked it before).

## The Azure Service Bus is a beast

The Windows Azure Service Bus is a godsend when you have to develop a hybrid application. The ability to simplify the networking needs and infrastructure makes it seem like magic. However with all that magical ability the price is that it hides it's complexity and along with it many errors.

It's very easy to assume it's as easy as WCF (and for the most part it is) but if you start to stray from the path be prepared to do some documentation diving. Easily one of the most frustrating parts was performance troubleshooting the relay. We found out that you can't use it *exactly* like WCF, you need to hold the connection open otherwise you'll pay a pretty heafty performance penalty. We ended up implimenting something similar to [this](http://www.wadewegner.com/2011/12/how-to-handle-a-faulted-channel-with-the-windows-azure-service-bus/).

## RTFM

Don't assume that because you can write the code to make Azure magic happen you know how exactly that magic is implemented. The [Windows Azure](http://www.WindowsAzure.com) website has a wealth of information. Go read it and fully understand what you're doing otherwise you'll likely find yourself down a path where you don't know what's wrong because you don't know how it works.

## Figure out your logging and error handling scheme

System Center, ELMAH, Azure Table Storage, log4net. There are so many different ways to log and use error handling in your web application. Pick one, make it abstractable so you can plug in something else when you need it, and you will. We changed logging frameworks and strategies 3 or 4 times. Be flexibile on this, you'll find you end up needing more or less than what you currently have.

## Don't skimp on the Azure

Have you seen how [cheap](https://www.windowsazure.com/en-us/pricing/calculator/) it is to use Azure lately? It's always getting cheaper too. We were developing along, already planning on using table storage when they announced a price **decrease**. Thing is they're dropping the prices like crazy to get more people using Azure and it's you that benefits from it. Don't go overboard but don't feel like you need to spend 100+ hours optimizing the CLR to eek out a minor performance improvement because you're gunning for a smaller cloud service role. 

## Use all that Azure has to offer

Azure has a ton of [features](https://www.windowsazure.com/en-us/home/features/overview/). When was the last time you read through all of them? We ended up using a distributed design for our application because Azure made it cheap and easy to get a queuing system set up. Don't be afraid of using an Azure feature because you haven't used it before. Azure makes it simple to try new things out. Who knows, it might benefit your design!

