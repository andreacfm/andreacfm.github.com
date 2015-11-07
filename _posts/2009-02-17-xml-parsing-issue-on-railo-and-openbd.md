---
layout: post
title: 'Xml parsing issue on railo and openbd. '
date: 2009-2-17
wordpress-id: xml-parsing-issue-on-railo-and-openbd
comments: true
---
<p><img style="float: left; border: 0; margin: 10px;" src="/images/posts/railo.gif" alt="Railo" width="82" height="52" /><img style="float: left; border: 0; margin: 10px;" src="/images/posts/bluedragon.gif" alt="Open bluedragon" width="270" height="55" /></p>
<p>As per my previous post I have installed Railo and Open BlueDragon on Jrun 4 as instances of a multiserver installation that also support cf8 and cf7.</p>
<!--more-->
<p>Starting my tests I noted that both Railo and OpenBd in this particular configuration shows issues performing xml parse operations. </p>
<p>I got errors on both servers running code like:</p>
<p>&lt;code class="coldfusion"&gt;<br />var xml = xmlParse(xml);<br />result = xmlSearch(xml,'/items/');<br />&lt;/code&gt;</p>
<p>Googling around I discovered that Jrun miss some classes/configurations that both Railo and OpenBd native installtion provide.</p>
<p>I added this line in the java.config file as java.args ( I cut it for making it readable  but you must add it all in one line with no spaces ).</p>
<p>&lt;code class="coldfusion"&gt;<br />-Djavax.xml.parsers.DocumentBuilderFactory=<br />com.sun.org.apache.xerces.internal.jaxp.DocumentBuilderFactoryImpl<br />&lt;/code&gt;</p>
<p>Restart the server and the xml functionalities will be regulary available.</p>
