---
layout: post
tags: [blog, jekyll, github, jekyll-bootstrap, How to build a blog using Jekyll-Bootstrap and Github]
title: How to build a blog using Jekyll-Bootstrap and Github (Part 1)
---
{% include JB/setup %}

I have a mental backlog of the items that I'd eventually like to put on this blog but one of the first things that comes to mind is the origins story of how this blog was built and what I have on my task list to implement next.

Initially when I set out to make my spot on the internet I started looking at all the different blogging engines. Did I want to go WordPress? Nah too clunky and not my cup of tea. Did I want to go to the other extreme and get a VPS, install my own blogging engine and customize the hell out of it? Maybe, but it's too expensive for me right now to justify. 

And then through some deliberation I decided to pull the trigger and go with Google's Blogger. But it sucked. Bad.

Don't get me wrong. I love what Google is trying to do with Blogger. The new dynamic views are downright sexy. It's also super easy to get it integrated with your Google+ account, analytics, email and everything else Google owns. The problem for me was that 1) it wasn't easy enough to customize, especially with the aforementioned dynamic views I wanted to use and 2) it just felt plain wrong. 

Here I am an experienced programmer using a blogging engine with a funky CMS engine feel to it. No way. I had to change.

Then I saw the light. A fellow co-worker and blogger recommended github to me. Whaaaa? A DVCS that I've never really used as a blogging platform? Full control over my layout, content and whatever the hell else I wanted to do with it (within reason)? Nerd factor through the roof? Sold.

So back to today. Currently this blog is hosted on [github pages](http://pages.githb.com) using [jekyll](http://jekyllrb.com/) for all the heavy lifting. Github makes it really easy to commit an index.html file and any other html source and host it based on your repository name. You can even do this for free if you're ok with keeping your stuff open source! Crazy awesome right?

So wait, what's this jekyll thing then? Jekyll is essentially a static file generator for blogs. It'll take whatever my blog template is that I've committed to github, parse it, and spit out a bunch of static html files for you all to enjoy. And it's fast. Stupid fast. It also scales like nobodies business.

See under the covers of any big website there's a bunch of server side code generating html/javascript to be served up to the hordes of people visiting their site. And with that code there's usually a database back-end serving up all the data needed to generate that delicious content. This takes lots of horsepower, time and money to do. So what's the quickest way to short circuit our servers and just get to content? A big ole cache. And what is that cache doing? Essentially serving up the same static content to the same people if the given input parameters are the same.

For me (and the purpose of this blog) I don't need a bunch of dynamic server side functionality. I'm all about serving up blog posts and content here. Why do I need a fancy server and database to do all of that? The input parameters are always the same, a static permalinked URL. Even if I wanted some rich functionality I could just use some javascript and css. HTML 5 is badass ya know.

Back to the current implementation then. What's this Jekyll-Boostrap thing then? Why wouldn't I just use jekyll to create my blog with my uber design skills? Well that my friends is for the next post.