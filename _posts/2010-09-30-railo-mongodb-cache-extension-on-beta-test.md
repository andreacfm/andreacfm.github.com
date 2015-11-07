---
layout: post
title: 'Railo MongoDB Cache Extension on Beta Test '
date: 2010-9-30
wordpress-id: railo-mongodb-cache-extension-on-beta-test
comments: true
categories: [Railo, MongoDB]
---
<p><img style="border: 0; float: left; margin-left: 10px; margin-right: 10px; margin-top: 5px; margin-bottom: 5px;" src="/images/posts/mongodb-logo.png" alt="" width="256" height="117" />In these days I am really interested in <a href="http://it.wikipedia.org/wiki/NoSQL" target="_blank">nosql</a> tools and especially in the  <a href="http://www.mongodb.org/" target="_blank">MongoDB</a>  document databse. </p>
<p>What amazes me about mongo is that is much more than a key value pair storage while it expose a quite complete query api, a full indexes support and an atomic Fast-In-Place data update.</p>
<!--more-->
<p>Over this MongoDB supports asynchronous replication of data between servers for failover and redundancy. This makes really easy to share and replicate data between a cluster.</p>
<p>The result is that Mongodb is an incredibly fast and flexible document database. </p>
<p>Following what <a href="http://www.markdrew.co.uk/blog/post.cfm/couchdb-cache-extension-beta-for-railo" target="_blank">Mark Drew</a> was  doing for CouchDb I thought was a good idea to implement a <a href="http://www.getrailo.org/" target="_self">Railo</a> Cache plugin that bring into Railo world the power of MongoDB used as cache engine. </p>
<p>The extension implements the Railo Cache interface at 100%. This means that you can switch from any other cache that Railo support to MongoDb cache with safety. The driver serialize  any object ( or queries or templates etc... ) you want to cache and will reinflate them up when you need to read them. An index is created over the key of your cache objects so that reading them will be a breeze. The plugin also support the <a href="http://www.mongodb.org/display/DOCS/Replica+Sets" target="_blank">mongodb replica Sets</a> ( cluster )  and makes your application wait if a failover is in place.</p>
<p>Many thanks to <a href="http://www.markdrew.co.uk/blog/post.cfm/couchdb-cache-extension-beta-for-railo" target="_blank">Mark Drew</a> that made the installation docs over the Railo wiki. You can find more info, installation step by step and details here: </p>
<p><a href="http://wiki.getrailo.com/wiki/extensions:mongodb" target="_blank">http://wiki.getrailo.com/wiki/extensions:mongodb</a></p>
<p><a href="http://wiki.getrailo.com/wiki/extensions:mongodb" target="_blank"><br /></a></p>
<p> </p>
