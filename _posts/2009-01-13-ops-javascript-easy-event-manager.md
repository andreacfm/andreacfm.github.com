---
layout: post
title: 'OPS javaScript easy event manager.'
date: 2009-1-13
wordpress-id: ops-javascript-easy-event-manager
comments: true
---
<p>At this step is just an idea.</p>
<p>How many times did you find to deal with many objects and to start loosing control over the events flow of teh applications.</p>
<!--more-->
<p>I use many times different libraries ( I always try to follow the
best practice ) implementing his own way to manage events. it works but
many times is not a very efficient way of desgin your applications.
It's a long time I have in mind to build a centralized event manager
framework-agnostic to be used as external support for :</p>

<ul>
    <li>create new custom events</li>
    <li>resgister events in a respository</li>
    <li>being able to subscribe to these events</li>
    <li>dispach teh eevnt from any place in my application</li>
</ul>

<p>I finally started to build OPS as a simple events manager.</p>
<p>Here a fast example of a very very alpha release, just to post the concept:</p>

{% highlight js %}

/* Craete e new event using the OPS factory.
I also pass a callback that will receive the full event like argument.
*/
var myEvent = new OPS.Factory.Event('myEvent', function(ev){
        alert(ev.getData());
    });

/*
register the event in the OPS.Events repository
*/
OPS.Events.addEvent(myEvent);

/*
my observer is an object that fill up an input filed when something happen
*/
var observer = function(ev){
    document.getElementById('div_Foo').value = ev.getData();
}

/* subscribe the observer to run when myEvent is dispatched */
OPS.Events.subscribe( observer , myEvent );
$(document).ready(function(){

    $('#select_Foo').change(function(){

    /* on select change I add data to myEvent */
        myEvent.setData($(this).val());
        /* dispatch the event from the OPS repository passing the event itself ( with data added ) as argument */
        OPS.Events.dispatchEvent(myEvent);
    });

});

{% endhighlight %}

<p>As you see in the example I before create e new event using the
internally OPS.Factory.Event class giving a name and optionally a
callback.<br />The event is then added to repository that store it by name.<br />An
observer method is subscribed to the event that is then dispatched
passing event object itself as argument with a dynamic data argument
that can store anything.<br />As you see teh event is dispached as answer to a change attached with jquery but could dispatched in any other postion.</p>
<p>
I will add a sort of api and more examples/ test quite soon.</p>
