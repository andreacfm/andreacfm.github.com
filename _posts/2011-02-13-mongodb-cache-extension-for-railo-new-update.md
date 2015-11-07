---
layout: post
title: 'MongoDb Cache Extension for Railo - New Update'
date: 2011-2-13
wordpress-id: mongodb-cache-extension-for-railo-new-update
comments: true
categories: [Railo, MongoDB]
---
<p>A new update the the MongoDB Cache extension for Railo is on the extension provider.</p>
<!--more-->
<p>Some bug was fixed and performance improved by a better tuning of the query that respects the cache expiration timeout. In my tests I could reach 400 interactions ( put and get of 400 items ) in in average time of 1200ms. Pretty awesome!!!!</p>
