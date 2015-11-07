---
layout: post
title: 'Railo WebSockets Gateway Extension'
date: 2011-1-24
wordpress-id: railo-websockets-gateway-extension
comments: true
categories: Railo
---
<p>I have just uploaded the Railo WebSockets Gateway Extension to the Railo preview extension provider.</p>
<!--more-->
<p>This extension enables you to launch a server that is capable to manage messaging from HTML <a title="http://dev.w3.org/html5/websockets/" rel="nofollow" href="http://dev.w3.org/html5/websockets/">WebSockets</a>.</p>
<p> The server runs on a dedicated port. Railo will receive notifications when a connection is opened, closed and any time a message is sent invoking a cfc listener class. The gateway can also being invoked via SendGatewayMessage so to allow your app to push message to all the connected clients.</p>
<p>While only few browsers natively support WebSockets up to now exists many libraries that mange the failover to flash sockets or other technologies like ajax long polling etc... WebSockets are a great way to implement messaging and data pushing using well known technologies like javascript. The gateway just makes it a breeze pushing data from your Railo application to any connected client.</p>
<p>You can find docs about the extension in the <a href="http://wiki.getrailo.org/wiki/Extensions:WebSockets_Gateway" target="_blank">Railo wiki</a> and some sample code cloning the following github repo https://github.com/andreacfm/websockets_example_apps.</p>
<p>Please post any feedback in the <a href="http://groups.google.com/group/railo" target="_blank">Railo Google Group</a> and any bug in the Railo Jira bugtraker.</p>
