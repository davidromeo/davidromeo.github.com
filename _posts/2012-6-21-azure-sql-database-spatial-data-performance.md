---
layout: post
tags: [SQL, Windows Azure, Database, Performance, Spatial Data]
title: So your Azure SQL database spatial data queries suck?
---
{% include JB/setup %}

At my current client we're building an API that serves up spatial data for locations. We originally designed a query that utilized the [STDistance](http://msdn.microsoft.com/en-us/library/bb933952.aspx)  function on the SQL Server geometry data type. Each of our geometry columns on multiple tables had spatial indexes created.

On-premise this works great. It returned queries sub-second and was never an issue. Previously we had great luck with these queries in Azure SQL databases (formally SQL Azure) as well. As of the last few days however our queries started taking much longer than usual, average 8 seconds up to 40 seconds!!!

After some tuning of our stored procedure and not getting anywhere, I thought that the problem might be with the spatial indexes. Dropping and recreating them seemed to do the trick but after some time we ended up back where we were before, frustratingly long running queries.

Turns out that Microsoft knows about this issue and has an [MSDN](http://msdn.microsoft.com/en-us/library/windowsazure/hh352174) article about it that was rather difficult to find (Known Issues in Windows Azure SQL Database, go figure) . I believe my issues are directly related to the issues seen with spatial indexes. I'm not too surprised either since you can find [blog](http://social.msdn.microsoft.com/Forums/en-US/ssdsgetstarted/thread/77618325-ba1a-4af8-b5cb-171f13e09794) posts complaining about it from back when spatial data support was released. I'm guessing Microsoft has a few growing pains around Azure SQL databases.

For right now my mitigation plan is to move off of Azure hosted SQL and utilize table storage. I might even see better performance now since I'm able to scale my cloud services and Azure SQL database is capped at a single core. 

The more I look at it, a NoSQL solution is making more sense every day. For my applications I rarely need relational entities beyond a few degrees. If I need reporting then I'll dump my information into a SQL database. Until then I'll live in a world where I can (more) reliably predict the storage SLAs.
