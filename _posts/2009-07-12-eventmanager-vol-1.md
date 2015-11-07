---
layout: post
title: 'EventManager Vol 1'
date: 2009-7-12
wordpress-id: eventmanager-vol-1
comments: true
---
<p>I start today a series of post on the usage and documentation of my EventManager for coldfusion. <a href="http://www.assembla.com/wiki/show/cfEventManager/bwB6IEtdar3QLXeJe5afGb" target="_blank">You can find more docs and svn code here.</a></p>
### Initialize The EventManager
<p><em>EventManager is done to work standalone or to be easily integrated with Coldspring. Both examples will be provided.</em></p>
### Standalone
<!--more-->
<p><code class="coldfusion"><br /><!--- normally saved as singletone on application start ---><br /><cfset application.em = craeteObject('component','EventManager.EventManager').init() /><br /></code></p>
<h3><em>Init( Events:Array , Listeners:Array , XmlPath:String , AutowireEvents:Boolean , Debug:Boolean , Scope:String )</em></h3>
<p>The init method takes the following arguments.</p>
<ul>
<li>Events:Array - default arrayNew(1) - Array of structs representing the events to register.</li>
<li>Listeners:Array - default arrayNew(1) - Array of structs representing the listeners to register.</li>
<li>XmlPath:String - default "" - Relative Path to an xml file containing events and listeners to be registered.</li>
<li>AutowireEvents:Boolean - default false - If true any event create for being dispatched is autowired using beanInjector.</li>
<li>Debug:Boolean - default false - If true force Em to save a trace of any operation executed.</li>
<li>Scope:String - default 'request' -  Says to Em how to save the tracing info if debug mode is true. <em>Request</em> use the request scope and clean up the trace memory any time the request die. <em>Instance</em> persists the informations into the EventManager instance itself.</li>
</ul>
<p>
<code class="coldfusion"><!--- events array ---><br /><cfset events = arrayNew(1) /><br /><!--- events  --->	<br /><cfset event = structNew() /><br /><cfset event.name = 'myevent' /><br /><cfset event.type = 'evapp.events.myevent' /><br />.....add more events....<br /><br /><!--- listeners array --->	<br /><cfset listeners = arrayNew(1) /><br /><!--- listener  --->	<br /><cfset listener = structNew() /><br /><cfset listener.event = 'myevent' /><br /><cfset listener.listener = 'evapp.listeners.mylistener' /><br /><cfset listener.method = 'manageData' /><br /><cfset listener.priority = 10 /><br /><cfset listener.initMehod = 'setUp' /><br /><cfset listener.cache = true /><br />.....add more listeners....<br /><br /><cfset eventManager = createObject('component','EventManager.EventManager')<br />.init(events,listeners) /></code></p>
### Xml Syntax via xmlPath
<p>You can setUp your events/listeners using xml notation. The xmlPath
argument you can pass to init mode represent the relative path to the
xml config file.
</p>
<p><code class="coldfusion"><cfset eventManager = createObject('component','EventManager.EventManager')<br />.init(xmlPath='/myapp/config/eventmanager.xml') />	</code></p>
<p>In init method using the xmlPath
attribute will not overwrite or stop the eventManager from loading
arrays of events and listeners if provided.</p>
{% highlight html %}
<code class="coldfusion"><cfset eventManager = createObject('component','EventManager.EventManager')<br />.init(events,listeners,'/myapp/config/eventmanager.xml') />	<br /></code><br />
{% endhighlight html %}
<p>The previuos example will load all the events from array and xml and
then will register listeners from array and from the xml too.</p>
<p>See <a href="http://www.assembla.com/wiki/show/cfEventManager/xml" target="_blank">xml for schema details</a>. In teh resource folder are present both .dtd and .xsd to validate your xml.</p>
###
Coldspring Tip
<p>If laoded via coldspring you can use the great syntax tool to create arrays and struct from xml that coldpring shipd for free</p>
<p>
<code class="xml"><bean id="Events" class="coldspring.beans.factory.config.ListFactoryBean"><br />
<property name="sourceList">
<list><br />
<map><br />
<entry key="name"><br />
<value>myEvent</value><br />
</entry><br />
<entry key="type"><br />
<value>EventManager.Event</value><br />
</entry><br />
</map><br />
....... more events here ...
<br />
</list>
<br />
</property>
<br /></bean>
<br /><bean id="Listeners" class="coldspring.beans.factory.config.ListFactoryBean"><br />
<property name="sourceList">
<br />
<list><br />
<map><br />
<entry key="event"><br />
<value>myEvent</value><br />
</entry><br />
<entry key="listener"><br />
<value>evapp.listeners.mylistener</value><br />
or<br />
<bean ref="listenerBeanID"/><br />
<br />
</entry><br />
<entry key="method"><br />
<value>methodToFire</value><br />
</entry><br />
</map><br />
.................... more listeners	<br />
</list><br />
</property><br />
</bean> 	<br />
<bean id="eventManager" class="EventManager.EventManager" lazy-init="false"><br />
<constructor-arg name="events"><br />
<ref bean="Events"/><br />
</constructor-arg><br />
</bean><br /><br /></code></p>
