---
layout: post
title: 'Make your ruby classes Comparable and Enumerable'
date: 2011-7-27
wordpress-id: make-your-ruby-classes-comparable-and-enumerable
comments: true
categories: Ruby
---
Something very cool in ruby are mixins. As the word says mixin is a technique to mixed a module into a class using the statement "include".
<!--more-->
While including a module is a very large topic I focused on the opportunity to include module defined in the Ruby standard library into your class to take advantages of the methods and abilities that these modules provide.
The <a href="http://www.ruby-doc.org/core/classes/Comparable.html" target="_blank">Comparable</a> module in ruby define methods like  &lt;   &lt;=   ==   &gt;   &gt;=   between?  .
What if I want to achieve is making my class instances <strong>comparable</strong> so that I can ask to ruby if <strong>class_a &gt; class_b</strong>.<!--more--> Here an example:
{% gist 1075795 %}
The Person class include the module Comparable and implements one single method (&lt;=&gt;). This methods is used by the Comparable module to perform the logic of any of the operator that the module provide.In the example I say to the Person class to compare instances through the @name attribute. But we even gain more functionalities. Once that our classes are able to be compared they are also able to be sorted if placed inside an array. Amazing!!!

{% gist 1109218 %}

But what if I want to find Persons by name?? Wen can use for this purpose the <a href="http://www.ruby-doc.org/core/classes/Enumerable.html" target="_blank">Enumerable</a> module. What we can do is to create a custom PersonEnumerator class like this:

{% gist 1075798 %}

Including the Enumerable module and implementing the each method we gain most of the many methods that the module expose. In our example I <strong>find</strong> a person object passing a block that filters each Person by name.

The mixin technique applied to the ruby standard library  is very powerfull. Your code code gets more elegant and more <strong>Ruby Way</strong> for you to maintain and for your collaborator to read and understand

Ruby amazes me any day more!
