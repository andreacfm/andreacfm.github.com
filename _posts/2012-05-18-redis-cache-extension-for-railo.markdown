---
layout: post
title: "Redis cache extension for Railo"
date: 2012-05-18 09:24
comments: true
categories: railo, coldfusion
published: true
---

I have recently had occasion to work with <a href="http://redis.io/" target="_blank">Redis</a> and I got really impressed by how is fast and reliable. Redis is a nosql key/value store quite commonly used in the Ruby world where I am digging these days.
<!--more-->
Many well known projects like Resque, Sidekiq and others make a wide use of Redis for storing any kind of data. What makes Redis really shining, over being so fast, is the ability to manage typed data like hashes, sets and lists. This feature makes the engine suitable to be used in many more situations than a plain key value store.

Looking around into the cfml community I discovered that Redis almost completely unknown in the coldfusion world. What a shame???

What a better occasion to make another cache extension for Railo. I have found in <a href="https://github.com/xetorthio/jedis" target="_blank">Jedis</a> a very well designed and fully featured Java client and well... here we are.

The result is an extension that you can easily install on your Railo server. Once you got it running creating a new cache and use is very easy.
You can find some more info on <a href="https://github.com/andreacfm/Redis-Cache-Extension" target="_blank">github</a>.

I made some fast test comparing with the Railo MongoDb cache extension that I have developed as well.

{% highlight xml %}
<cfloop from="1" to="10" index="j">
	<cfset start = gettickcount()>
	<cfloop from="1" to="5000" index="i">
		<cfcache action="put" id="a#i#" value="#i#">
		<cfcache action="get" id="a#i#" name="v">
	</cfloop>
	<cfset end = gettickcount()>
	<cfset time = end -start>
	<cfset total = total + time >
	<cfoutput>#time/1000# s<br/></cfoutput>
	<cfflush>
    <cfset cacheClear()>
</cfloop>
<cfoutput>Average sec: #(total/10)/1000#</cfoutput>
{% endhighlight  %}

This simple snippets runs 10 iterations with 5000 write/read operations each. ONn my machine MongoDb executes this in 3 secs average per iteration.
Redis will do the same job in 1 sec average so basically 66% faster. I have reporetd the same performance even launching the scripts from 4 concurrents threads.


###Resources
* <a href="https://github.com/andreacfm/Redis-Cache-Extension" target="_blank">github repository with installation details and more</a>
* <a href="http://redis.io/" target="_blank">Redis</a>
* <a href="https://github.com/xetorthio/jedis" target="_blank">Jedis</a>
