---
layout: post
title: 'Cf Event Manager'
date: 2009-6-5
wordpress-id: cf-event-manager
comments: true
---
<p>I have now released a first version of a tool that I am implementing and using since a while.</p>
<p>CfEventManager is exactly what the word say. An EventManager tool for cfml programming.<br />Some of the features:</p>
<!--more-->
<ul>
<li>Very light with a simple API to use/implement.</li>
<li>Flexible to allow registering of events / listeners from cfml syntax, xml file and programmatically on runtime.</li>
<li>Ability to cache the listeners objects.</li>
<li>Use the built in event object or create your own in few easy steps.</li>
<li>Ability ti stop event propagation.</li>
<li>Order the listeners with a customized priority order.</li>
<li>Autowire events object via coldspring by using the Brian Koteks beanInjector class.</li>
</ul>
<p>On next releases to 1.0:</p>
<ul>
<li>Dispatching of async events.</li>
<li>addEventListener based on regex match.</li>
</ul>
<p><a href="http://code.assembla.com/cfEventManager/subversion/nodes" target="_blank">Download and Svn<br /><br /></a><a href="http://www.assembla.com/wiki/show/bwB6IEtdar3QLXeJe5afGb" target="_blank">Docs ( not completed yet )<br /></a></p>
<p><a href="http://www.andreacfm.com/page.cfm/open-source/cf-event-manager" target="_blank">Project Page on this Blog</a></p>
