---
layout: post
title: 'StructNew takes arguments'
date: 2010-6-2
wordpress-id: structnew-takes-arguments
comments: true
---
<p>During last Sotr I was talking with <a href="http://www.markdrew.co.uk/blog/" target="_blank">Mark Drew</a> and <a href="http://getrailo.org" target="_blank">Micheal Offner-Streit ( the Railo cto )</a>  and we discovered one of the many gems hidden into Railo engine.</p>
<!--more-->
<p>Any cf developer has always fight with the missing support for a linked hash map in cfml. This lack has made a task  keeping a struct in a defined order. In railo you can simple do this:</p>
{% highlight html %}
<cfset str = structNew('linked') />
{% endhighlight %}
<p>What you have now is a struct 100% similar to a normal struct that has the whole capabilities of a linked hash map. For example the map keep the elements into an ordered stack.</p>
<p>You can read more in the <a href="http://wiki.getrailo.org/wiki/FUNCTION:STRUCTNEW" target="_blank">railo wiki docs</a>.</p>
