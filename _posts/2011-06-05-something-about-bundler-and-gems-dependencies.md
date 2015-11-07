---
layout: post
title: 'Something about bundler and gems dependencies'
date: 2011-6-5
wordpress-id: something-about-bundler-and-gems-dependencies
comments: true
categories: [Ruby, Rails, Bundler]
---
Since some months I have started to programm in Ruby and especially using the Rails framework. I have to say I find Rails so great that I realized, that after some months, that I can be quite productive knowing very little about Ruby itself. This tells you how powerfull can be a dsl written in Ruby and talks about the nice job Rails developers did but is not going to make me shine as a Ruby developer.
<!--more-->
I have decided to step back and I am finally going to open a Programming Ruby book seriously. I will go throught my Ruby discovering writing here my tests and anything I will discover in my learning Ruby travel. This will help me to fix some concept in my mind and hopefully someone else will learn from my mistakes.

For the moment I discovered something about bundler I really didn't know before and I 'd like to share. I have just ended reading a post of Yehuda Katz about <a href="http://yehudakatz.com/2011/05/30/gem-versioning-and-bundler-doing-it-right/?utm_source=rubyweekly&amp;utm_medium=email" target="_blank">Bundler and Gems dependencies</a> that really opened my eyes.

Something from Yehuda post:

<!--more-->
<h2><em>Basic Versioning Rules for Apps</em></h2>
<em>
</em>
<ol>
	<li><em>After bundling, always check your Gemfile.lock into
version control. If you do this, you do not need to specify exact
versions of gems in your Gemfile. Bundler will take care of ensuring
that all systems use the same versions.</em></li>
	<li><em>After updating your Gemfile, always run bundle install first. This will conservatively update your Gemfile.lock. This means that except for the gem that you changed in your Gemfile, no other gem will change.</em></li>
	<li><em>If a conservative update is impossible, bundler will prompt you to run bundle update [somegem]. This will update the gem <strong>and any necessary dependencies</strong>. It will not update unrelated gems.</em></li>
	<li><em>If you want to fully re-resolve all of your dependencies, run bundle update. This will re-resolve all dependencies from scratch.</em></li>
	<li><em>When running an executable, <strong>ALWAYS</strong> use bundle exec [command]. Quoting from the bundler documentation: <em>
In some cases, running executables without bundle exec may work, if the
executable happens to be installed in your system and does not pull in
any gems that conflict with your bundle. However, this is unreliable and
is the source of considerable pain. Even if it looks like it works, it
may not work in the future or on another machine.</em> See below, “Executables” for more information and advanced usage.
</em></li>
	<li><em>Remember that you can always go back to your old Gemfile.lock by using git checkout Gemfile.lock or the equivalent command in your version control.</em></li>
</ol>
<em>
</em>
<h2><em>Executables</em></h2>
<em>
</em>

<em>When you install a gem to the system, Rubygems creates wrappers for
every executable that the gem makes available. When you run an
executable from the command line <strong>without bundle exec</strong>,
this wrapper invokes Rubygems, which then uses the normal Rubygems
activation mechanism to invoke the gem’s executable. This has changed in
the past several months, but Rubygems will invoke <strong>the latest version of the gem installed in your system</strong>, even if your Gemfile.lock specifies a different version. In addition, it will activate the <strong>latest (compatible) installed version of dependencies of that gem</strong>, even if a different version is specified in your Gemfile.lock.</em>

<em>
</em>

<em>This means that invoking executables as normal system executables
bypasses bundler’s locked dependencies. In many cases, this will not
pose a problem, because developers of your app tend to have the right
version of the system-installed executable. For a long time, the Rake
gem was a good example of this phenomenon, as most Gemfile.locks declared Rake 0.8.7, and virtually all Ruby developers had Rake 0.8.7 installed in their system.</em>

<em>
</em>

<em>As a result, users fell into the unfortunate belief that running
system executables was compatible with bundler’s locked dependencies. To
work around some of the remaining cases, people often advocate the use
of rvm gemsets. Combined with manually setting up application-specific
gemsets, this can make sure that the “system executables” as provided
via the gemset remain compatible with the Gemfile.lock.</em>

<em>
</em>

<em>Unfortunately, this kludge (and others) sufficiently reduced the pain
that most people ignored the advice of the bundler documentation to
always use bundle exec when running executables tied to gems in the application’s Gemfile.lock.</em>

<em>
</em>

<em>It’s worth noting that typing in rake foo (or anyexecutable foo) in the presence of a Gemfile.lock,
and expecting it to execute in the bundler sandbox doesn’t make any
sense, since you’re not invoking Bundler. Bundler’s sandbox relies on
its ability to be present at the very beginning of the Ruby process, and
to therefore have the ability to ensure that the versions of all loaded
libraries will reflect the ones listed in the Gemfile.lock.
By running a system executable, you are executing Ruby code before
Bundler can modify the load path and replace the normal Rubygems loading
mechanism, allowing arbitrary unmanaged gems to get loaded into memory.
Once that happens, all bets are off.</em>

I have to say I learn new things about Ruby  every day and I really have to thank devs like Yehuda that keep posting so interesting topics.
