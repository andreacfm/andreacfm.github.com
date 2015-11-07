---
layout: post
title: 'Ruby instance_eval'
date: 2011-7-2
wordpress-id: ruby-instance_eval
comments: true
categories: Ruby
---
Working on one of my first ruby gem I have started to learn more about ruby meta programming and ruby core language.
<!--more-->
My gem needs a sort of singleton class that needs to be configured when the application starts. I have choosed to use a Module as singleton cause a ruby module cannot be initialized and so it just fits my needs.
I will then include the configured module into the model that will need it.
<!--more-->
What I wanted to achieve was something like:
{% gist 1059936 %}
I created my module and added 2 class methods one called configure that is planned to take care of the block and a method called set that is going to apply the requested configurations.
Something like this:
{% gist 1059940 %}
If you run this code you get an exception saying to you that:<strong>
undefined method ‘set’ for main:Object</strong>
This was a bit confusing at first. The error is thrown cause the block is created outside of the module scope and is executed in the scope where it was created. In this special case the scope is the general Object scope.
What I need is that the block passed to the configure method is executed in the scope of My_module. This can be achieved using the instance_eval method.
Passing the block as argument to instance_eval this is executed in the current self scope. Exactly what I need.
{% gist 1060794 %}
In conclusion instance_eval is one of the important topic in ruby meta programming allowing blocks to be sent around and executed in the calling instance scope.



﻿



