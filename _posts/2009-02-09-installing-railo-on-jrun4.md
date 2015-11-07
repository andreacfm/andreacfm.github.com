---
layout: post
title: 'Installing Railo and Open BlueDragon with ColdFusion 8 Multiserver on JRUN4'
date: 2009-2-9
wordpress-id: installing-railo-on-jrun4
comments: true
---
<p><img style="border: 0pt none; margin: 10px; float: left;" src="/images/posts/railo.gif" alt="Railo" width="82" height="52" />In the last meeting of the <a href="http://www.cfmentor.com/" target="_blank">Italian CFUG </a>we
got
a very interesting speach about the ability to install coldfusion
as multiserver ( Jrun 4 platform )  and the convenience to deploy under
it more instances of coldfusion or  of any other JAVA J2EE
Web or Enterprise Application.
<!--more-->
I so started my tests for setting up my
personal test environment with Adobe cf, Railo and Openbd all deployed
under the same multiserver installation.</p>
<p>I started my test installing Cf8 as multiserver and the process ended succesfully. Cf8 is now installed in c:\jrun4serverscfusion </p>
<p>At this poit Jrun 4 is installed and is reachable through port 8000. </p>
<p>I use IIS 7 locally so I decided to let coldfusion installer take care  of the appropriate settings over my default web site. Up to here nothing really changed in the ways I use cf: iis is correctly mapped, cf admin is always reachable through cfide an so on. What change is the fact the cf8 is now a single instance of a JRUN multiserver installation ready to receive and manage more applications. </p>
<p><img style="border: 0; margin: 10px;" src="/images/posts/jrun.jpg" alt="Jrun 4" width="746" height="356" /></p>
<p>I downloaded Railo War file from <a href="http://www.railo-technologies.com/en/index.cfm?treeID=213" target="_blank">here</a>. </p>
<p>Back to the Jrun4 administrator I created e new server ( I called it Railo ) and this was confirmed on port 8302. </p>
<p><em>On the Pictures you see my Jrun4 with many instances already deployed so just keep them as example.<br /></em></p>
<p>Follow the next steps:</p>
<p>1) Change the Railo.war file extension to .zip and unzip that.</p>
<p>2) Go to your {jrun4 folder}/servers/Railo/ and delete the default-ear folder. ( Optional but recomended )</p>
<p>3) In the Jrun4 admin panel select the railo server ( if is not running switch it on ) .Go to the J2EE Componenets tab and click on deploy in the Web Application Area . </p>
<p><img style="border: 0; margin: 10px;" src="/images/posts/railo_jrun_1.jpg" alt="Railo on jrun" width="670" height="316" /></p>
<p>4) Search the folder where you unzipped the war file and confirm. Wait the time jrun need to deploy railo and....maybe looks too easy but.....you are done. Railo is deployed and ready to serve your cfm pages.</p>
<p>You can now reach your railo installation like
http://localhost:{installation port}/{server name - railo in my
case}/railo-context/admin/server.cfm.</p>
<p><img style="border: 0; margin: 10px;" src="/images/posts/railo_jrun_2.jpg" alt="Railo on jrun" width="618" height="352" /></p>
<p> </p>
<p>Now I have Railo installed and working but I want to set up a real test suite that gives me the ability to test the same code with different engine with no files copy or syncro.</p>
<p>1) Craete a new site in IIS ( I have IIS 7 on Vista ). Point it to your webroot ( in my case d:wwwroot ) and add a custom header like 'railo'. </p>
<p>2) In the Jrun administrator go in the J2EE components tab and click on the server name. In the <strong class="h3">Web Application Overview</strong>where change your context root to "/" and point the document root to the position of your IIS wwwroot  ( d:wwwroot for me). </p>
<p><img style="border: 0; margin: 10px;" src="/images/posts/jrun_railo_3.jpg" alt="Railo on jrun" width="764" height="358" /></p>
<p>3) Now we need to set up our web server. In your jrun installation folder go in the bin folder and open the wsconfig file. A java tool will open up.<br />Click on Add. Select railo as jrun host, IIS as web server and railo as the site name we want to configure. Click on advanced and add <em>.cfm</em> and <em>.cfc</em> as mimtypes. Confirming the  tool will add the correct mapping to your IIS 7 so that the railo web site will use railo engine and not cf8 for processing cfm and cfc files.</p>
<p>4) As last step open your host file . <br />On vista should be something like : C:WindowsSystem32driversetchosts </p>
<p>Add this 2 line :</p>
<p>127.0.0.1        railo<br />127.0.0.1        cf8</p>
<p>Save and close the file.</p>
<p>Now if you open your browser and try to call<strong> http://cf8/</strong> the call will be directed to 127.0.0.1 and in my case will call the IIS default web site. </p>
<p>But if I call http://railo/ my IIS is setted to recognice <em>railo</em> as railo web site header and process cfml using railo engine.</p>
<p>For testing it I simply put an index.cfm file under wwwroot with this call inside:</p>

{% highlight html %}

    <cfdump var="#server#" />

{% endhighlight %}

<p><strong>http://cf8/index.cfm</strong></p>
<p><img style="border: 0; margin: 10px;" src="/images/posts/cf8-dump.jpg" alt="" width="799" height="255" /></p>
<p><strong>http://railo/index.cfm</strong></p>
<p><img style="border: 0; margin: 10px;" src="/images/posts/railo-dump.jpg" alt="" width="854" height="413" /></p>
<p> </p>
<p>So our test suite is ready. Following the same step you can easily deploy <a href="http://openbluedragon.org/" target="_blank">Open BlueDragon</a> (  you can fin ethe war file <a href="http://www.openbluedragon.org/download.cfm" target="_blank">here</a> ) as well as more instnaces of cf8 or previous version like cf7 or 6.1 ( be carefull to your jre version for previous cf version support ). </p>
<p>I find this solution really effective to test exactly the same code versus more engine without too many troubles.</p>
<p>And from here ..... clustering deploying more web application in the same server instance....many  new possibilities to explore.</p>
<p>I am now seriously starting playing with railo and openbd and I will go on posting  about them as on our beloved cf8 as well.</p>
