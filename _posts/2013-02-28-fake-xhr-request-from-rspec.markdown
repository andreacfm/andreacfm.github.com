---
layout: post
title: "Fake xhr request from rspec"
date: 2013-02-28 16:36
comments: true
categories:
---
I discovered today that I had no idea of how to fake an *xhr* request in an Rspec controller test. I need this cause some of my layout strategy behaves on the *request.xhr?* method.
<!--more-->
As expected *Rspec* solved the issue in a cool and elegant way.

{% highlight ruby %}

	# normal request
	get :show, id: 1  
	# exactly the same request, This time fake to be an xhr call. request.xhr? will be true
	xhr :get, :show, id: 1 

{% endhighlight %}








