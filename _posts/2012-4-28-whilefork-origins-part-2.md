---
layout: post
tags: [blog, jekyll, github, jekyll-bootstrap, How to build a blog using Jekyll-Bootstrap and Github]
title: How to build a blog using Jekyll-Bootstrap and Github (Part 2)
---
{% include JB/setup %}

So to recap last time I introduced [jekyll](http://jekyllrb.com/) and gave my reasons for using it. Let's roll up our sleeves and have some fun building out a basic blog without using this fancy bootstrapper that I keep talking about.

Since I'm using github to host this site I signed up for their [Micro](https://github.com/plans) plan. This is the base plan you need if you're going to want a custom domain for you're spiffy new site. 

You can always get away with their free plan as long as you're ok with them assigning your blog a ***username***.github.com url and that your site's repository will be wide open for the world to fork.

I'll take a little side break here and warn you that the next part is my opinion only mainly because I've only been using git for a little under a week now. Before that I've never really used a DVCS and had been using TFS and SVN for years, so I might be a little ingrained in my ways.

I used the wonderful [Git Extensions](http://code.google.com/p/gitextensions/) to get me started. I basically followed the help documentation on [github:help](http://help.github.com/win-set-up-git/) (so awesome for a newb like me). The part about generating the RSA SSH key has a few wrong pictures but don't let that throw you off. The words are spot on.

Trust me when I say that you really want to follow this to the letter. Because when I borked something, it broke. Hard. My biggest mistake was probably trying to use [TortiseGit](http://code.google.com/p/tortoisegit/) before I even really knew what Git was or how it worked. I'm sure it works all wonderful and great but for some reason it just made things worse. I eventually uninstalled it and ended up having to generate all new keys for my repository and losing several hours of my life. Lame.

Since then I've mainly been using the Git Bash shell that installs with the Git Extensions and recently [Console2](http://sourceforge.net/projects/console/) after I fixed some PATH issues in Windows. 

I'm sure this all would have been easier if I had tried it on my mac-mini but damnit I'm a .NET guy so I should be able to get this to work!

Last bit of setup before we get to the fun stuff is to create a repository with 1) either the name of the blog you want if you're using the \*.github.com or 2) whatever you'd like if you've got a Micro plan or better. It's really really [easy](http://help.github.com/create-a-repo/).

Now you've got all the boring bits out of the way you can go wild creating whatever static html/css/javascript content you want and putting it in you're repository for the world to see. For reference and more in depth magic the pages [help](http://help.github.com/pages/) site is the best. Also don't freak out the first time like I did, when they say it will take up to 10 minutes for the first time you push content to show up, they really do mean it.

Unless you bought a paid plan on github you're mostly going to be concerned with the first two sections, **User & Organization Pages** and **Project Pages With The Automatic Page Generator**. The last part there is crazy, you don't even have to go outside your browser to create beautiful pages! They even give you the option to have a Google Analytics Tracking ID inserted!

If you're planning on ever having a repository name different from your username and upgrading to a paid plan for domain name support, do the stuff mentioned in the **Project Pages Manually** section before you ever push code. I didn't and almost lost my entire site I had been working on.

So that finishes up Part 2. Sorry for stringing the pro's along with all this setup. If I didn't ask a co-worker how to even get started I would have been completely lost, gotten frustrated and this crazy experiment might not have happened. Next time I'll promise we'll get into jekyll and the fun stuff.