---
layout: post
title: "ruby alias vs alias_method"
comments: true
categories: ruby
---
While *alias* and *alias_method* looks very similar at first they hide a substantial different behaviour. Look
at the following code.

<!--more-->

{% highlight ruby %}

### Basic alias behaviour

class Boss
  def name
     p "Andrea"
  end
  alias :full_name :name
end

Boss.new.name # => Andrea
Boss.new.full_name # => Andrea
{% endhighlight %}

This is the the basic behaviour we could expect from the *alias* method. *#full_name* is perfectly aliased to #name.
But what happens if we subclass Boss?

{% highlight ruby %}

### Alias in subclass

class Employee < Boss

    def name
       p "Bob"
    end

end

Employee.new.name # => Bob
Employee.new.full_name  # => Andrea
{% endhighlight %}

Looks like *Employee#full_name* points to the superclass *#name* method and not at *Employee#name*! And this is the truth.

*alias* is a ruby keyword and is executed when source code gets parsed. When Boss class is parsed *Boss#full_name* is aliased to *Boss#name*
and this will be truth for any Boss instance as per any Class instance that subclass Boss.

*alias_method* is instead, as the word says, a method and is executed in the current self scope.

{% highlight ruby %}

### Using alias_method

class Boss
  def name
     p "Andrea"
  end
  def self.apply_alias
      alias_method :full_name, :name
  end
  apply_alias
end

class Employee < Boss
    def name
       p "Bob"
    end
    apply_alias
end

Boss.new.name # => Andrea
Boss.new.full_name # => Andrea
Employee.new.name # => Bob
Employee.new.full_name # => Bob
{% endhighlight %}

*alias_method* is executed the first time in the self scope of Boss and then the self scope of Employee and apply the method aliasing
in the way we expected.
While this looks like a tiny difference using *alias_method* grant more flexibility and may avoid unpredictable code behaviour.
