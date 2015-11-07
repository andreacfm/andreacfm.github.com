---
layout: post
title: 'Model Glue Caching - patch update'
date: 2010-1-8
wordpress-id: model-glue-caching-patch-update
comments: true
---
<p>Two days ago I have posted some code that solve ( in part )  an annoying bug regarding caching in Model Glue framework.</p>
<!--more-->
<p>As per MG docs the caching declaration can be used on any event-handler and include tag but, in practice. caching is only working if applied to the initial event-handler ( the first invoked by the url ). </p>
<p>Since we want to use MG on our project, and we absolutely need a granular caching system, we are implementing  what we think can be a good solution and we would like to share for feedback and testings ( of course the MG team is the first in receiving our code for review and possible inclusion in future releases ).</p>
<p>We have made a new review to the first patch and now MG can support the following instructions:</p>

{% highlight xml %}
<event-handler name="page.index">
    <broadcasts />
        <results>
            <result do="views.one"/>
            <result do="views.two"/>
            <result do="template.main" />
        </results>
        <views>
            <include name="three" template="pages/three.cfm" cache="true" />
            <include name="four" template="pages/four.cfm"/>
        </views>
</event-handler>
{% endhighlight   %}

{% highlight xml %}
<event-handler name="views.one" cache="true">
    <broadcasts />
    ....... 
    <views>
        <include name="one" template="pages/one.cfm" />
    </views>
</event-handler>
{% endhighlight   %}

{% highlight xml %}
<event-handler name="views.two">
    <broadcasts />
        ......
    <views>
        <include name="two" template="pages/two.cfm" />
    </views>
</event-handler></p>
{% endhighlight   %}

<p>As you  can see from this code MG can cache a single views but , and this is the best feature I guess , is also able to cache a full event.handler even if that is not the initial event handler.</p>
<p>This solution can really speed up yout MG app reducing dramatically the effort you ask to your server to what your page exactly needs. Any time you are able to cache an "inner request" event MG will just include a bunch of html skipping any broadcasting and this can really save a lot of unnecessary server stress.</p>
<p>Over that imagine you can easily cache a full page excluding just the single lines that ( for example ) are reserved to logged user info/panel ( and of course skipping any unnecessary message broadcasting ).</p>
<p>You can find the <a href="/get/mg/cache/EventContext.txt" target="_blank">patch here</a> ( replace file <span style="color: #4b4b4b; font-family: Verdana, Geneva, sans-serif; line-height: 20px;">/ModelGlue/gesture/eventrequest/EventContext.cfc)</span></p>
<p>Let me have your feedbacks and suggestions.</p>
<p>REMEMBER : THIS IS CODE SHARED FOR TESTING AND NOT FOR PRODUCTION USE.</p>
