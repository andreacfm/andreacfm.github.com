---
layout: post
title: 'Ses Url on railo and coldfusion on Jrun 4'
date: 2009-3-1
wordpress-id: ses-url-on-railo-and-coldfusion-on-jrun-4
comments: true
---
<p>Going on working with my new multiserver installation I falled into an issue that took me a bit of time to go throught.</p>
<p>I could normaly run my application using cf, railo and openbd but all the application was failing trying to call a ses url like:</p>
<!--more-->
<p>&lt;code class="coldfusion"&gt;http://railo/index.cfm/mypage/<br />&lt;/code&gt;</p>
<p>The server is simply not able to find the .cfm mapping and just do not invoke any cfm engine like .cfm mapping was not in the url.... what made me think is that this happen only with the instances I added to jrun but not to the main cfusion server ( the ones that I installed jrun with ; in my case cf8 ).</p>
<p>I started look around and especially in the web.xml ( placed under the web-inf folder of any server instance ) file where mapping and settings for the jrun server instance are placed ( In my case file is here : C:JRun4serverscf7cfusion.earcfusion.warWEB-INFweb.xml) . With my surprise I found that in any cf instance added to Jrun this code is commented by default:</p>
<p>&lt;code class="coldfusion"&gt;&lt;!--Start Ses <br />  &lt;servlet-mapping id="coldfusion_mapping_6"&gt;<br />     &lt;servlet-name&gt;CfmServlet&lt;/servlet-name&gt;<br />     &lt;url-pattern&gt;*.cfml/*&lt;/url-pattern&gt;<br />  &lt;/servlet-mapping&gt;<br />  &lt;servlet-mapping id="coldfusion_mapping_7"&gt;<br />    &lt;servlet-name&gt;CfmServlet&lt;/servlet-name&gt;<br />    &lt;url-pattern&gt;*.cfm/*&lt;/url-pattern&gt;<br />  &lt;/servlet-mapping&gt;<br />  &lt;servlet-mapping id="coldfusion_mapping_8"&gt;<br />    &lt;servlet-name&gt;CFCServlet&lt;/servlet-name&gt;<br />    &lt;url-pattern&gt;*.cfc/*&lt;/url-pattern&gt;<br />  &lt;/servlet-mapping&gt;<br />  End Ses --&gt;<br />&lt;/code&gt;</p>
<p>Basically if you uncomment this code and restart the server also a mapping like : .cfm/page make the server invoking the coldfusion engine while before the jrun server simply was not able to recognize the mapping and was answering that no application was setted up to answer to the request.</p>
<p>While I solved the cf issue I found more problems to set up railo mapping cause as we all know jrun is not the railo "first choice" and settings are a bit different as in the default railo installation under Resin .... After some testing I added this code to C:JRun4servers
ailoWEB-INFweb.xml , restared the server and also railo started to respond correctly...</p>
<p>&lt;code class="coldfusion"&gt;&lt;!--Start Ses --&gt;<br />  &lt;servlet-mapping&gt;<br />     &lt;servlet-name&gt;CFMLServlet&lt;/servlet-name&gt;<br />     &lt;url-pattern&gt;*.cfml/*&lt;/url-pattern&gt;<br />  &lt;/servlet-mapping&gt;<br />  &lt;servlet-mapping&gt;<br />    &lt;servlet-name&gt;CFMLServlet&lt;/servlet-name&gt;<br />    &lt;url-pattern&gt;*.cfm/*&lt;/url-pattern&gt;<br />  &lt;/servlet-mapping&gt;<br />  &lt;servlet-mapping&gt;<br />    &lt;servlet-name&gt;CFMLServlet&lt;/servlet-name&gt;<br />    &lt;url-pattern&gt;*.cfc/*&lt;/url-pattern&gt;<br />  &lt;/servlet-mapping&gt;<br />  &lt;!--End Ses --&gt;    <br />&lt;/code&gt;</p>
<p>Please note that I need to restart completely Jrun and not only the railo instance to make chanhges being recognized. I am not sure wht ( probbaly some kind of main config cache ) but after restarting jrun also Railo instance started to work fine with ses url.</p>
<p>I have not yet solved the matter with openBd but I plan to look into it soon.</p>
