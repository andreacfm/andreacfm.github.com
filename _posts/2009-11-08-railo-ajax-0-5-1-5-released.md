---
layout: post
title: 'Railo Ajax 0.5.1.5 released'
date: 2009-11-8
wordpress-id: railo-ajax-0-5-1-5-released
comments: true
---
<p>A new version has been released.</p>
<!--more-->
<p>The most interesting news is the complete refactor of the UI tags. RailoAjax library now provide bridges classes that need a speficic adapter to perform the action required. This allows to switch between one library support to another with no need to change the core code.</p>
<p>An example can be found <a href="http://projects.getrailo.org/RailoAjax/tests/index.cfm?template=cfwindow/ext.cfm" target="_blank">here</a>.</p>
<p>Once the concrete implementation is done ( the Ext cfwindow is already done ) you can choose the library using the cfajaximport tag.</p>
{% highlight html %}
<cfajaximport library="ext />
{% endhighlight %}
<p>Having implemented a bridge pattern for any UI implementation has also allowed us to provide a set of new events provided directly by the Railo.Events engine that do not rely on the specific implementation making code even more portable. The following event has been added :</p>
<ul>
<li>Window.beforeCreate</li>
<li>Window.afterCreate</li>
<li>Window.beforeShow</li>
<li>Window.afterShow</li>
<li>Window.beforeHide</li>
<li>Window.afterHide</li>
<li>Window.beforeClose</li>
<li>Window.afterClose</li>
<li>Layout.afterTabSelect</li>
<li>Layout.beforeTabInit</li>
<li>Layout.afterTabInit</li>
<li>Layout.beforeTabCreate</li>
<li>Layout.afterTabCreate</li>
<li>Layout.beforeTabRemove</li>
<li>Layout.afterTabRemove</li>
<li>Layout.beforeTabSelect</li>
<li>Layout.afterTabSelect</li>
<li>Layout.beforeTabDisable</li>
<li>Layout.afterTabDisable</li>
<li>Layout.beforeTabEnable</li>
<li>Layout.afterTabEnable</li>
</ul>
<p>What is usefull is that these events will always be usable in the same way not depending by the the tag concrete implementation. So If I need to listen to a window hide event and I have choosed the ext implementation I can use both the following syntax:</p>
{% highlight javascript %}
Railo.Events.subscribe(callback,'Window.beforeHide')
//or
Railo.Window.getWindowObject('mywin').addListener('beforeclose',callback,this);
{% endhighlight %}
<p>The RailoLayout.js package has already been rewritten with the default jquery implementation.</p>
<p>Version 0.5.2 will allow ui tags to receive an options arguments called 'args'. This struct will be converted into json and pushed into the implementation init method. In this way any config defined by the jquery or ext apis will become available. I am also working on a start for cfmap implementation.  </p>
<p> </p>
