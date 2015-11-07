---
layout: post
title: 'Monitor resque workers via upstart'
date: 2012-1-11
wordpress-id: monitor-resque-workers-via-upstart
comments: true
categories: [Resque, Upstart]
---
Resque is a Redis-backed Ruby library for creating background jobs, placing them on multiple queues, and processing them later. Resque works firing up a set number of workers than will coninuously look for job to be processed and will execute them following the rules defined when the workers are launched. You can have a single worker process any queue or having a single worker processing a single queue or even fire up more workers that will look forward to a single queue. Read more about <a href="https://github.com/defunkt/resque" target="_blank">resque</a>.
 <!--more-->
A very important topic is to be sure that the workers are always available and that any time your application is deployed also the workers are restarted. This is crucial cause the worker load an instance of your application and will then process the jobs against this application instance. If you deploy a new version of your application but you do not restart your workers the jobs will be run on an outdated code version and this is clearly something you do not want!<!--more-->

I have solved both the issues using upstart to monitor the workers deamon and a rake task that kill all the workers any time the application is deployed. Basically the idea is that any time a worker is killed upstart will restart it with the most up to date application version.

Here is a sample of the upstart script I use to monitor the workers for my application:

{% gist 1259382 resque_worker_upstart.sh %}

If you are not familiar with upstart you can read more <a href="http://upstart.ubuntu.com/" target="_blank">here</a>.
<p style="text-align: left;">What this script does is  launching the workers in a defined rails environment using a passed namespace ( I use namespace to ensure that I can safely use the same Redis engine for different applications/environments ). You can also note that the script execute the command from the application directory using an unpriviledged user. This trick was due to the fact that I run the application and the workers using a specific user ( 'my_user' in the example) and not as root as upstart attempt to do. The rest of the script load in the shell rvm with ruby 1.9.2 before executing the script.</p>
<p style="text-align: left;">Once this conf script has started upstart will monitor the processes and will restart it something gets killed or does not respond.</p>
<p style="text-align: left;">Great! I know need a task to be runned via capistrano when a new deployment gets completed. Killing the worker will invoke upstart to restart them with the lastest deployed codebase.</p>
<p style="text-align: left;">{% gist 1259382 restart_workers_task.rb %}</p>
<p style="text-align: left;">Invoking the task will kill any workers that is registered with the Resque instance running in your application. Be sure to run the task just before to restart your application. In this way you are sure that the task will attempt to kill the correct pids.</p>
{% gist 1259382 restart_workers_cli %}

Et voila! Any feed bask is welcome.
