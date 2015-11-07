---
layout: post
title: 'Speed up your eclipse'
date: 2009-4-7
wordpress-id: speed-up-your-eclipse
comments: true
---
<p><img style="border: 0; float: left; margin: 10px;" src="/assets/content//logos/eclipse.png" alt="" width="171" height="91" />I think that any eclipse users has experimented  the fact that  eclipse tends to slow down. In the past I had to reinstall the whole environment especially after loading new plugins that was probably breaking something down. Btw I always followed as best practice to clen up eclipse any 6 months and I learned fast how to export preferences to be able to push them into the new install. In this way to pass to a new and clean eclipse install is quite painless.</p>
<p>In the last period I tried to reduce the number of opened projects in my workspace to the really important ones, and I  also experimented the solution of mantaining many workspaces but I do not feel very compofortable with that. </p>
<!--more-->
<p>I then got the idea to check what kind of settings eclipse was passing to the jvm and blogging around I found a great post of <a href="http://www.henke.ws/post.cfm/Turbo-charging-Eclipse" target="_blank">Mike Henke</a>.</p>
<p>I added the following arguments to my eclipse.ini file:</p>
<p>&lt;code class="coldfusion"&gt;<br />-vm <br />C:Program FilesJavajre1.6.0_12injavaw.exe<br />-vmargs<br />-Xms512m<br />-Xmx512m<br />-XX:PermSize=128m<br />-XX:MaxPermSize=128m<br />-Xverify:none&lt;/code&gt;</p>
<p>The vm path depends on what do you have available in your machine, but I suggest you to update at least to version 1.6 update 12. Be carefull do not leave extra white spaces and .... look your turbo eclipse start to fly...</p>
