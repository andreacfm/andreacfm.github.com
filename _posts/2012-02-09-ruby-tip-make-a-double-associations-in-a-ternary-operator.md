---
layout: post
title: 'Ruby tip. Double association in a ternary operator'
date: 2012-2-9
wordpress-id: ruby-tip-make-a-double-associations-in-a-ternary-operator
comments: true
categories: Ruby
---
I found myself today in the opportunity to use a double association in a ternary operator. Basically I wanted to assign 2 variables based on a certain condition.
<!--more-->
Normal ruby double assignment works easy like this:

{% highlight ruby %}

#simple double assignment
a,b = 1,2
a  # 1
b  # 2

{% endhighlight  %}

Up to here no surprise. But what if I want to evaluate a condition and assigns both the variables??

{% highlight ruby %}

#double assignment . Wrong ways
a,b = true ? (1,2) : (3,4)
a,b = true ? 1,2  : 3,4

{% endhighlight  %}

Both this attempts ends in a syntax error. The right way:

{% highlight ruby %}

a,b = false ? [1,2] : [3,4]
a  # 3
b  # 4

{% endhighlight  %}

Easy and clean. Values comes in an array and are correctly assigned.
Of course this works for any number of variables you need to assign

{% highlight ruby %}

# triple assignment in ternary operator
a,b,c = false ? [1,2,3] : [4,5,6]
a   # 4
b   # 5
c   # 6

{% endhighlight  %}
