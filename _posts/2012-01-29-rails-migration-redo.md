---
layout: post
title: 'Rails migration redo'
date: 2012-1-29
wordpress-id: rails-migration-redo
comments: true
categories: [Ruby, Rails]
---
A very good practice, when writing a rails migration, is to be sure that the down methods works as expected. Once the migration is ready you should make it run and, if anything is fine, you should  rollback it and run it again. In this way you are sure that both the up and down migration works as you planned.
<!--more-->
To make it faster you can use the following command

{% highlight ruby %}

rake db:migrate:redo

{% endhighlight  %}

This will run a rollback of the lates migration and will run it again.

You can even say how many steps you want to rollback and the re apply using the steps attributes as you do in a normal roll back command:

{% highlight ruby %}

rake db:migrate:redo step=2

{% endhighlight  %}
<div></div>
