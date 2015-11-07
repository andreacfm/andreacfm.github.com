---
layout: post
title: 'Git rebase --onto to the rescue ( part 1 )'
date: 2011-11-3
wordpress-id: git-rebase-onto-to-the-rescue-part-1
comments: true
categories: Git
---
I am now using git since more than a year as my primary scm. I tend to use it also against svn repo,  I can so focusing on git  becoming always more comfortable using it.
<!--more-->
To be honest up to now my git use has always been quite basic, while projects I was working on never needed more that a master/develop/topic branches workflow. Recently I faced a more complex issue related to the necessary  support for proper <strong>support branch</strong> that was going to diverge for a long time from the develop branch.

We have a develop branch where is done the job for new version 2.0 while we still have a stable branch where we support version 1.0. The issue comes from the fact that version 1.0 is not going to receive only simple hotfixes but will also be improved with new feature that need to be ported to version 2.0..

For the first month or so we still were able to merge the 2 branches but not they have diverged too much. Merge is not an option and so we had to find a new strategy.

Our goal was to carry all the changes made on a topic branch borned by the 2.0 branch into the same 2.0 and also to the 1.0 without merging 2.0 into 1.0. This can be solved cherry-picking any single commit from the topic branch to the 2.0 and then merge topic into 1.0. While this works fine we faced situations where the topic branch were actually getting too long and cherry picking many commits can be buggy and tricky.

<!--more-->

We finally solved our issue using a git feature called rebas --onto.

An example (you can clone example code here https://github.com/andreacfm/git-test):
<p style="text-align: center;"><img class="size-full wp-image-210 aligncenter" src="/images/posts/Screen-Shot-2011-11-03-at-10.02.06-AM1.png" alt="" width="700" height="234" /></p>
Our repo has a develop branch checked out  from a master branch. Both master and develop have commits made after they diverged. A topic branch is also borned by develop and some job was made on it.

Rebase onto helps us cause it allows us to say to git to rebase the topic branch on master <strong>VIA</strong> develop. Basically git makes a diff between master and topic excluding all the job that was made on develop after that devlelop diverged from master. This diff gets applied to master.

Our goal is to bring the 2 commits made on topic branch to master and to develop branch without having to merge develop into master. Topic needs to be rebased --onto master and merged into develop. To make this we need a temporary copy of topic.

{% highlight sh %}

$ git checkout topic
$ git checkout -b temp

{% endhighlight %}

The temp branch allows us to perform the 2 different actions (merge on develop and rebase onto master) leaving git calculate the diff for us. More on this in the next post.

{% highlight sh %}

$ git rebase --onto master develop topic
$ git co master
$ git merge topic
$ git checkout develop
$ git merge temp
$ git branch -D topic
$ git branch -d temp
{% endhighlight %}

Before we rebase --onto topic to master via develop. We need then to go to master and to fast-forward master to topic by merging. We can now merge the temp branch into develop
and delete both topic and branch.
Here is what we obtain:

<img class="size-full wp-image-218 aligncenter" src="/images/posts/Screen-Shot-2011-11-03-at-10.33.08-AM.png" alt="" width="724" height="518" />

As you see both develop and master branch has received just the commits made on the topic branch but still develop has not been merged into master.
Rebase --onto saved our day cause avoid us to make very long cherry picking session on many different branches (forgot to say our project is much more complex that this example). Respect to the cherry picking technique rebase --onto is also less error prone cause let git calculate the commits you need to apply. Sometimes reading the git tree commits is very hard on big projects and this increase the possibility to loose some commits around.

More on this to come.
