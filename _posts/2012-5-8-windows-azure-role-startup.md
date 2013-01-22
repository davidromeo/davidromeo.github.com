---
layout: post
tags: [Windows Azure, WIF, Microsoft.IdentityModel, Startup Tasks]
title: Windows Azure Unable to Find Assembly 'Microsoft.IdentityModel'
---
{% include JB/setup %}

My blogging friend Robert Greiner had a [post](http://creatingcode.com/2012/04/windows-azure-role-instances-are-taking-longer-than-expected-to-start/) a few weeks ago talking about a fix for an issue I introduced as a result of a completely unrelated problem I was encountering in our Windows Azure environment. 

Before I go explaining why and how I introduced this <strike>bug</strike> feature we should probably talk about the title of this post and how to fix it.

## Windows Azure Assemblies (or lack of)

Windows Azure installs surprisingly very little when you deploy to a web or worker role. This can be a problem for developers who are used to deploying on an environment where they can just install whatever runtimes or software dependencies they need. So to counteract this you need to set the Copy Local property to true on any .dll you have a dependency on that is not part of the base .NET 4 framework. This will push the .dll into the bin directory and will get packaged and published to Azure as a result.

![Copy Local]({{ BASE_PATH }}/assets/images/2012/copylocal.png)

Get used to doing this because depending on your project size you might find some strange omissions from the Azure GAC. Heck even Microsoft knows this because when you create a default Azure project, the Microsoft.WindowsAzure.* .dlls are marked Copy Local = true.

## Enter the Identity

So you're deving along and everythings awesome and you've even integrated some Windows Azure ACS into your app. As a part of that you've downloaded and installed the Windows Identity Foundation SDK and runtime. Go you!

But now you've published to Azure, you hit your application and everything breaks with this nonsense: 

<p>
  <script src="https://gist.github.com/2640716.js"> </script>
  <noscript>
    <pre>
       Could not load file or assembly 'Microsoft.IdentityModel, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.
    </pre>
  </noscript>
</p>

You even marked the Microsoft.IdentityModel .dll Copy Local = true! Lame. What happened?

It seems as though there are some parts of the Windows Identity Foundation that expect their dependencies to be in the GAC. So what a dev supposed to do when you can't reliable modify the Azure environment in case of a role recycle?

## Windows Azure Startup Tasks to the Rescue

To register the Microsoft.IdentityModel in the GAC .dll I used what Microsoft calls a [Startup Task](http://msdn.microsoft.com/en-us/library/windowsazure/hh180155.aspx). This essentially runs anything you can pack into a .cmd file on the startup and provisioning of the Azure role.

Let's take a look at the IdentityGac.cmd I use to register the .dll:

<p>
  <script src="https://gist.github.com/2641027.js"> </script>
  <noscript>
    <pre>
       	@echo off
		sc config wuauserv start= demand
		wusa.exe "%~dp0Windows6.1-KB974405-x64.msu" /quiet /norestart
		sc config wuauserv start= disabled
		e:\approot\bin\startup\gacutil /if e:\Approot\bin\Microsoft.IdentityModel.dll
    </pre>
  </noscript>
</p>

- Line 1: Duh
- Line 2: This turns on the Windows Update Service so we can install the WIF runtime
- Line 3: This actually install the WIF .msu package
- Line 4: Turn off the Windows Update Service
- Line 5: Install the Microsoft.IdentityModel.dll into the GAC

I included along with this a copy of [gacutil.exe](http://stackoverflow.com/questions/3397479/where-is-gacutil-exe) in my project in a folder called "Startup". The important thing to remember here is that all of this runs relative to your bin directory (though we can cheat with this a bit since Azure always installs our application in the same location). This combined with the startup task did the trick.

## Bringing it home

 Now back to circle back around the beginning of this post, make sure you're running your task as a background task UNLESS you have a specific reason to run it as a simple task. The important thing to remember here is that the simple task executes SYNCHRONOUSLY so that your Azure emulator might take a very long time to start depending on what your task does, or it might not start at all as in our case. 


We were able to set it to a background task and use it the same in our local and other deployed environments. The best option is to probably do something like [this](http://blog.smarx.com/posts/skipping-windows-azure-startup-tasks-when-running-in-the-emulator) though.

So there you go, a crash course in Windows Azure startup tasks and how to fix an annoying <strike>bug</strike> feature of the Azure role environment.
