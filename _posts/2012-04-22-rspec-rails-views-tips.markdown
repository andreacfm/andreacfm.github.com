---
layout: post
title: "Rspec rails views tips"
comments: true
categories: ruby, rails, rspec
---
In the last days I faced some new challenge in testing rails views with rspec.
Here is what I learned.
<!--more-->
I am useing the veru handy rails controller [prepend_view_path](http://api.rubyonrails.org/classes/AbstractController/ViewPaths/ClassMethods.html#method-i-prepend_view_path) helper to be able to choose dynamically what views to use to render the actual request.
A sample code is the following:

{% highlight ruby %}

#controller
before_filter :prepend_view_path_if_required

private
def prepend_view_path_if_required
    prepend_view_path "views/custom_view_path" if my_condition
end

{% endhighlight  %}

When my_condition returns true, the passed path will placed on top of the views_path rails controller stack. Rails will then look into this location as first choice when looking for a view to render. This technique allows me to choose what view to render in different conditions without the need to hacks into my routes. Is a nice tool. You just say to rails: "if this condition is true looks for views here as a first choice. If nothing is found go on and check into the rest of the views locations stack"

What was a bit challenging was the view testing when prepend_view_path plays a role into the rendering process.
Testing a single view placed for example in "views/custom_view_path/view_to_test" is not a big deal.

{% highlight ruby %}

  # rspec view test
  it ....
    render "custom_view_path/view_to_test"
    rendered.should match/"text to match"/
  ....

{% endhighlight  %}

But what if the view you are testing has code that render a partial?

{% highlight ruby %}

#custom_view_path/view_to_test
render :partial => "users/login"

{% endhighlight  %}

When you run it rspec creates a fake controller for you that will not know nothing about the 'views path prepending' that your application is expecting to use.
The users/login partial will be looked for in "app/views/users" folder but not in "app/views/custom_view_path/users" where you may expect it is looked for.
While a was trying to stub/mock things I then dicovereed that I could simply call the prepend_view_path method on the controller that rspec creates in views specs.
My spec is looking like this:

{% highlight ruby %}

# rspec view test
before do
    prepend_view_path "views/custom_view_path"
end

it ....
    render "custom_view_path/view_to_test"
    rendered.should match/"text to match"/
....

{% endhighlight  %}

When I run my test the correct views path is added to the controller and my spec runs as expected.
Simply and clean.

I then faced a new task.
The application I am building uses an helper method called is_mobile_request? that check if the call comes from a mobile. A view I was testing is rendering a partial that isa actually using this same helper method. While this is a smell of a not perfect design I needed a way to stub the result of this helper method call so that my view was able to render as expected.
My solution was to declare the spec of type helper and to stub the method on the helper scope.

{% highlight ruby %}

# rspec view test
describe "custom_view_path/view_to_test.html.erb", type: :helper do

before do
    .....
    stub(helper).is_mobile_request?{false}
    ....
end

end

{% endhighlight  %}

What happens here is that declaring the spec as type helper I can use/stub the helper scope in my spec.

###Conclusion
While I use rspec every day I often find ways to learn new things about it. My advise is to look into rspec code/docs/groups before trying to create hacks to test things. Most of the times a clean and elegant solution is already baked into rspec just to solve your issue.
