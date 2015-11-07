---
layout: post
title: 'RailoAjax core is jquery free.'
date: 2009-9-18
wordpress-id: railoajax-core-is-jquery-free
comments: true
---
<p>To make library lighter, especially for core usage, I have removed the jQuery dependency from the core RailoAjax library. What does this mean ??</p>
<!--more-->
<p>Core tags like cfajacproxy or cfdiv do not use any UI lib and they rely on the lonely RailoAjax library. Up to version 0.5.1 some task like binding and xhr calls where made with the jQuery help and we were forced to load jQuery in any page.</p>
<p>From version 0.5.1.1 ( already available ) RailoAjax is free from jquery dependency:</p>
### XHR
<p>You can now use RailoAjax as a XHR utility:</p>
{% highlight js %}
<p>var x = new Railo.XHR() ;<br />x.request({<br />url : url,<br />success:....<br />});<br />{% endhighlight   %}</p>
### DOM Events
<p>Dom event binding can be added like this:</p>
{% highlight js %}
Railo.Util.addEvent(dom element, event, callback );
{% endhighlight   %}
<p><a href="http://sizzlejs.com/" target="_blank"><img style="border: 0; margin-top: 0px; margin-bottom: 0px; float: left; margin-left: 10px; margin-right: 10px;" src="/assets/content//logos/sizzle.png" alt="" width="180" height="131" /></a>Btw I decide to keep one dependency in RailoAjax that is <a href="http://sizzlejs.com/" target="_blank">Sizzle.js</a>. </p>
<p>Sizzle is the most powerfull selector engine out there. Sizzle is fast, flexible and come from jQuery core.</p>
<p>Check out docs if you like. </p>
<p>You can use sizzle just as you were used to use jQuery selector:</p>
{% highlight js %}
<p>var element = Sizzle('#myId');</p>
{% endhighlight   %}
<p>Of course Sizzle return array of dom elements and not jQuery Objects.</p>
