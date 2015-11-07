---
layout: post
title: 'Railo tip: cffile action touch'
date: 2010-6-30
wordpress-id: railo-tip-cffile-action-touch
comments: true
---
<p>For linux/unix user is quite common to use the command <em><strong>touch</strong></em> (from the shell) to update the last modified date of a file (to the current time) or to create a new file.</p>
<!--more-->
<p>You can do that as well from Railo :</p>
{% highlight html %}
<cffile action="touch" file="whatever.cfm">
{% endhighlight   %}
<p><span style="font-family: arial, sans-serif; font-size: medium; "><span style="border-collapse: collapse; font-size: 15px;"><br /><br /></span></span></p>
