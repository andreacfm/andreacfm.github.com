---
layout: post
title: 'Railo MongoDB cache extension updated'
date: 2010-11-13
wordpress-id: railo-mongodb-cache-extension-updated
comments: true
categories: [Railo, MongoDB]
---
I have uploaded yesterday a main update of the MongoDB Cache extension for Railo. See installation details <a href="http://wiki.getrailo.org/wiki/extensions:mongodb" target="_blank">here</a>
<!--more-->
I have improved the management of timespan and timeidle expiring using some incredible feature that MongoDB offers.

1) Any time you ask for a key the plugin attempts to delete it running a MongoDB query ( optimized using index on any relevant field ) and then fetch it. If key is still there means that is a still valid entry.

2) Any 20 seconds a clean process is runned so to keep the db more updated as possible and making the the flush operation on cacheGet() more efficient.

In my test this has improved speed of about 30% delegating more operation to the db itself.

The following code makes 2000 read/write operation in an average of 1500/1600 ms.

{% gist 1035561 %}

Amazing !!!!!
