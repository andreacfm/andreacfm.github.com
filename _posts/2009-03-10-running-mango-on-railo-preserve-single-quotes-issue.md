---
layout: post
title: 'Running Mango on Railo. Preserve single quotes issue.'
date: 2009-3-10
wordpress-id: running-mango-on-railo-preserve-single-quotes-issue
comments: true
---
<p><img style="border: 0pt none; margin: 10px; float: left;" src="/images/posts/one_sweet_mangoblog_150x75a.png" alt="mango blog" width="150" height="75" />Trying mangoblog on my Railo installation I found at once a bug that invole the different way that railo and cf have to preserve the single quotes in sql syntax where the sql statement is represented by variables.</p>
<p>Mango Blog use a class called QueryInterface where most of the query devoted to collect data ara executed and cached so to speed up teh next identical request.</p>
<!--more-->
<p>The used method is this:</p>
<p>&lt;code class="coldfusion"&gt;</p>
<p>&lt;cffunction name="makeQuery" access="public" output="false" returntype="any"&gt;        <br />        &lt;cfargument name="query" required="true" type="string"&gt;<br />        &lt;cfargument name="cacheMinutes" required="false" type="numeric" default="-1"&gt;<br />        &lt;cfargument name="returnResult" required="false" type="boolean" default="true"&gt;<br />        <br />        &lt;cfset var customQuery = queryNew('id')/&gt;<br />        &lt;cfset var queryStatement = trim(arguments.query)&gt;<br /><br />        &lt;cfif arguments.cacheMinutes GT -1 AND arguments.returnResult&gt;<br />            &lt;cfquery name="customQuery" datasource="#variables.datasource.name#"  username="#variables.datasource.username#" password="#variables.datasource.password#" cachedwithin="#createtimespan(0,0,arguments.cacheMinutes,0)#"&gt;<br />            #toString(queryStatement)#<br />            &lt;/cfquery&gt;<br />        &lt;cfelse&gt;<br />            &lt;cfquery name="customQuery" datasource="#variables.datasource.name#" username="#variables.datasource.username#" password="#variables.datasource.password#"&gt;<br />            #toString(queryStatement)#<br />            &lt;/cfquery&gt;<br />        &lt;/cfif&gt;<br />        <br />        &lt;cfif arguments.returnResult&gt;<br />            &lt;cfreturn customQuery /&gt;<br />        &lt;/cfif&gt;<br />        <br />    &lt;/cffunction&gt;<br /><br />&lt;/code&gt;</p>
<p>As you see the sql syntax is represented by the variable queryStatement.</p>
<p>To be sure that the essential sinqle quotes are preserved Railo add an psq attribute:</p>
<p>&lt;code class="coldfusion"&gt;<br />&lt;cfquery name="q" datasource="dsn" psq="true"&gt;<br />.................</p>
<p>&lt;/code&gt;</p>
<p>Since from cf8 this code is accettable also in coldfusion due to the added ability to pass an argumentcollection to most of the tags where only the recognized attributes are evaluated while the others are skipped. </p>
<p>But I didn't want to loose cf7 compatibility ( this will crash trying to evaluate the psq attributes )  so i tried to use, also for Railo ,the preserveSingleQuotes() function and surprise....is working just fine. Following Railo docs "psq" attributes should be the safest way but after about 2 weeks of runnign Mango with this change I am now convinced that preserveSingleQuotes() will server us ok in this case.</p>
<p>&lt;code class="coldfusion"&gt;&lt;cfif arguments.cacheMinutes GT -1 AND arguments.returnResult&gt;<br />            &lt;cfquery name="customQuery" datasource="#variables.datasource.name#"  username="#variables.datasource.username#" password="#variables.datasource.password#" cachedwithin="#createtimespan(0,0,arguments.cacheMinutes,0)#"&gt;<br />            #preserveSingleQuotes(queryStatement)#<br />            &lt;/cfquery&gt;<br />        &lt;cfelse&gt;<br />            &lt;cfquery name="customQuery" datasource="#variables.datasource.name#" username="#variables.datasource.username#" password="#variables.datasource.password#"&gt;<br />            #preserveSingleQuotes(queryStatement)#<br />            &lt;/cfquery&gt;<br />        &lt;/cfif&gt;</p>
<p>&lt;/code&gt;</p>
<p>In this way we keep a full compaitbility from on cf7, cf8 and Railo too.</p>
<p> </p>
