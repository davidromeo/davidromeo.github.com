---
layout: post
tags: [Web Api, ASP.NET]
title: ASP.NET Web API Simple URL Versioning
---
{% include JB/setup %}

**Warning, what follows is a post on how to do URL versioning on a REST service. Many REST advocates hate URL versioning of a REST service and instead favor using http request headers. This is only for those that want/need to do URL based versioning.**

One of the simplest ways of versioning an API is to use URL versioning. You could have your URL to your latest api be **/api/Values/Get** and then support urls to have specific version numbers **/api/v1/Values/**. 

This isn't the hardest problem to solve, but it's also not the easiest. Let's say you're using the new ASP.NET Web Api and you wanted to implement the versioning I talked about above. One method is creating separate controllers for each version of your API. 

![Versioning Controllers]({{ BASE_PATH }}/assets/images/2012/versioningcontrollers.png)

This strategy while looking nice causes problems because the controller selector and dispatcher looks at the names of the controller when matching them up with the routes. It will compile fine but you'll end up getting this:

<p>
  <script src="https://gist.github.com/2932130.js"> </script>
  <noscript>
    <pre>
	   	"Multiple types were found that match the controller named 'values'. This can happen if the route that services this request ('api/{controller}/{id}') found multiple controllers defined with the same name but differing namespaces, which is not supported.
	
		The request for 'values' has found the following matching controllers:
		VersioningSample.Controllers.v1.ValuesController
		VersioningSample.Controllers.v2.ValuesController"
    </pre>
  </noscript>
</p>

If you were using the Web API beta you used a ControllerFactory to select which controller you wanted based on the API. With the Web API RC however they've changed this to use ControllerSelectors. Functionally they can perform the same things but fundamentally they're different.

