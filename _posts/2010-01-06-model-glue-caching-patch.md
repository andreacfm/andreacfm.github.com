---
layout: post
title: 'Model Glue Caching patch '
date: 2010-1-6
wordpress-id: model-glue-caching-patch
comments: true
---
<p><img style="border: 0; float: left; margin: 10px;" src="/images/posts/mgLogo.gif" alt="" width="125" height="117" />I started last week a very big project where we decided to use the MG framework as rendering engine. </p>
<p>The site will have a huge traffic and will need to display many 'heavy portlets' different by user or context etc... </p>
<!--more-->
<p>We started to make some test and investigations on how we could implement pur rendering architecture using the MG view caching system.  In short time we discovered that the cache declaration based on the include tag was not processed and considered by the framework. </p>
<p>The final result of our research job was that the only caching support "really" working was the once on the initial event object ( basically the first event called in a new request ).</p>
<p>This was a killer, not for the MG caching system per se ( we use an adapter to ehCache ) but because we completely needed to remove MG from the project. We then decided to make some more test and in a short time we could create a patch that allow  MG to cache views based on the declarations made in any single include xml tag.</p>
<p>So with this patch code like this :</p>
{% highlight xml %}
<include name="myview" template="pages/web/css_js.cfm" cache="true" cacheKeyValues="id" cacheTimeout="3600"/>
{% endhighlight %}
<p>will create a cache copy for 3600 seconds of the view based on the value of the id argument.</p>
<p>Please note that any keys looks for value into the event object  so, if you want to use sessionid as a cache key, you should push that into the event object on request start. Following a <a href="http://corfield.org/" target="_blank">Sean Corfield</a> suggestion the generate key now also consider the host where the view is processed, so If you run the same application from differents domains any domain generate a different cache.</p>
<p>We send code to Dan Wilson that is the MG maintainer for review and testing.</p>
<p>If you want to use and test ( do not use that in production cause is really not tested code ) <a href="/get/mg/cache/EventContext.txt" target="_blank">downlaod</a> the patch and replace the file /ModelGlue/gesture/eventrequest/EventContext.cfc. </p>
<p>Send your feedback ( or share on MG mailing list ).</p>
<p> </p>
<p style="padding-top: 0px; padding-right: 0px; padding-bottom: 15px; padding-left: 0px; margin: 0px;">Credits goes especially to <a style="color: #cc6600; text-decoration: none;" href="/www.millemultimedia.it" target="_blank">Cristian Costantini</a>.</p>
