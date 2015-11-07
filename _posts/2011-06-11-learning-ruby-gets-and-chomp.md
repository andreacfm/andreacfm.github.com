---
layout: post
title: 'Learning Ruby: gets and chomp'
date: 2011-6-11
wordpress-id: learning-ruby-gets-and-chomp
comments: true
categories: Ruby
---
Playing with the ruby console I am wondering how I can read some input from the console.
<!--more-->
Ruby ships with the method <strong>gets</strong> that makes easy to read console input. Just try the following code:

{% highlight ruby %}

print "What is your name? "
$stdout.flush
name = gets
puts 'Hi ' + name + '!!!'

# => Hi andrea
# !!!

{% endhighlight  %}


When the console asks for your name just type it. The ruby program will read the console input and will welcome you. You will note that  a new line is added after that the variable<em> name</em> is  printed out. This is the default behaviour of the gets function. Gets add a new line after any variable that memorize. If this is not desired  you can call the method <strong>chomp</strong> on the gets result and the newline is suppressed.

Change your code as follows and the new line will not be printed anymore:

{% highlight ruby %}

print "What is your name? "
$stdout.flush
name = gets.chomp
puts 'Hi ' + name + '!!!'

#=> Hi andrea!!!

{% endhighlight  %}
