---
layout: post
title: 'jdk1.6.0_11 speed up coldfusion createObject'
date: 2009-1-28
wordpress-id: jdk1-6-0-11-speed-up-coldfusion-createobject
comments: true
---
<p> During 2008 many posts in the cf community proved how a bug in the java 1.6 jdks was slowing down the creation of coldfusion objects. </p>

<!--more-->
<p>I personally realized that starting using more frameworks like <a href="http://www.coldspringframework.org/" target="_blank">coldspring</a>, <a href="http://www.transfer-orm.com/" target="_blank">transfer</a> and in general due to the fact that cf8 gives to developers ( finally!! ) the ability to code more tight to a really OO architecture. I started noting that applications with a large use of coldspring became very slow on start up ( also 20/30 seconds ) and in some case I had to give up with Transfer framework cause the performance were degrading to a very low level (I could use some shortcut and implement the framework but I do not like to use a feature at 50% ! I prefer to use a completely new road and implementing that at 100%).</p>
<p><img style="border: 0; float: left; margin-left: 10px; margin-right: 10px;" src="/assets/content//logos/322px-java-logo.svg-1.png" alt="" width="66" height="96" />Btw the bug was found in the 1.6 jdks versions and last jdk release solve it. From the first test look like performance relly speed up. The same application that was starting in 20/30 sec is now loading in 5/6 seconds that is a reasonable time due to the high number of object generations.</p>
<p>You can <a href="http://java.sun.com/javase/downloads/index.jsp" target="_blank">donwload jdk from here</a> and change default jdk in the cf admin ( for standalone instance ) or in jrun admin panel for multiserver installs.</p>
