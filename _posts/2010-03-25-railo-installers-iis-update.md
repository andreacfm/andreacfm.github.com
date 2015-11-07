---
layout: post
title: 'Railo Installers IIS update'
date: 2010-3-25
wordpress-id: railo-installers-iis-update
comments: true
---
<p>Jordan Micheals has posted a great update to the <a href="http://trac.getrailo.org/installers/" target="_self">Railo Installers</a> project. </p>
<!--more-->
<p>Read more <a href="http://groups.google.com/group/railo-beta/browse_thread/thread/d0087715afb042a0" target="_blank">here</a>.</p>
<p>Some of the bugs fixed/enhancements:</p>
<p><span style="color: #000000; font-family: arial, sans-serif; line-height: normal;">3.1.2.001-pl1 Patch Notes: <br />-------------------------- <br />- [NEW] IIS6 Is now fully supported on Windows Server 2003 <br />- [NEW] IIS7 Is now properly supported on Windows 7 machines <br />- [NEW] IIS7/IIS6 now set "index.cfm" as a default document option <br />- [NEW] Windows 64-bit is now available <br />- [BUGFIX] Windows 32-bit Installer will now auto-detect 64-bit machines <br />and will install the 64-bit connector when being installed on a 64-bit <br />version of Windows. This is true for both IIS6 and IIS7. This avoids the <br />  "LoadLibraryEx" failure in IIS if a 32-bit connector has been <br />installed on a 64-bit version of IIS. <br />- [UPDATE] The Tomcat connector has been upgraded from version 1.2.28 to <br />1.2.30 (latest as of this release) <br />- [UPDATE] The Tomcat Engine has been upgraded from version 6.0.20 to <br />6.0.26 (latest as of this release) <br />- [UPDATE] Source code in the Java JDK has been removed in order to <br />reduce the size of the installers by approximately 20 MB. The installers <br />now hover around the 100MB range. More rarely-used aspects of the JDK <br />that ships with the installer may be removed at a later date in order to <br />reduce the download size even more. </span></p>
