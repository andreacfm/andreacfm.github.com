---
layout: post
title: 'Replace CfDocument with Flying Saucer Xhtml renderer'
date: 2009-12-23
wordpress-id: replace-cfdocument-with-flying-source-xhtml-renderer
comments: true
---
As per my previous post about Xhtml <a href="http://www.getrailo.org/" target="_blank">Railo</a> capabilities I will post my firsts experiences using <a href="https://xhtmlrenderer.dev.java.net/" target="_blank">Flying Saucer</a> as enhancements of cfdocument tag.

Now, cfdocument is not bad but the rendering capabilities are quite limitated and when I discovered that cfdocument, up to cf9, do not support justified text alignment I decided to give a try with <a href="https://xhtmlrenderer.dev.java.net/" target="_blank">Flying Saucer</a>.
<!--more-->
The library works taking your xhtml and rendering that into a pdf processing your css.

What is good is that css2 and 3 are processed correctly so, for example, you can create a page header like:

{% highlight css %}
div.header {
display: block;
position: running(header);
}
@page {
  size: 8.5in 11in;
  margin: 18% 0%;
  @top-left {
   content: element(header);
  }
}
{% endhighlight   %}

The element in the body that is selected as .header is not rendered as normally you expect but is rendered into any page heading.

Of course same works for footer.  See more about css @page <a href="http://www.w3.org/TR/CSS2/page.html" target="_blank">here</a>.

Creating a page-break is a breath:

{% highlight css %}
div.break{
    page-break-after:always;
}
{% endhighlight   %}

Any div with class break will make a new page starts from the div position.

I also discovered that pdf needs fonts to be embedded into the file itself.

This is not supported in css spec but Flying Saucer added some extra css 'helper' so that embedding a font is easy like this:

{% highlight css %}
@font-face {
    src: url(file:///TradeGothicLTStd.ttf);
    -fs-pdf-font-embed: embed;
    }
{% endhighlight   %}

So far the possibilities looks immense and I think they are .

I have created a java class that the absolute path of the xhtml you need to convert and the path of where you want your pdf to be placed and does the job for you.

{% highlight java %}
package com.andreacfm.utils;
import com.lowagie.text.*;
import org.xhtmlrenderer.pdf.ITextRenderer;
import org.xhtmlrenderer.resource.XMLResource;
import org.w3c.dom.Document;
import org.xml.sax.InputSource;
import java.io.*;

public class PDFReader{
    public void createPDF(String url, String pdf)throws IOException, DocumentException {
        OutputStream os = null;
        try {
            os = new FileOutputStream(pdf);
            ITextRenderer renderer = new ITextRenderer();
            Document doc = XMLResource.load(new InputSource(url)).getDocument();
            renderer.setDocument(doc, url);
            renderer.layout();
            renderer.createPDF(os);
            os.close();
            os = null;
            }
         finally {
            if (os != null) {
                try {
                    os.close();
                    } catch (IOException e) {
                    // ignore
                }
             }
         }
     }
 }
{% endhighlight   %}

You can call it like :

{% highlight html %}
<cfset objPDFReader = createObject('java','com.andreacfm.utils.PDFReader').init()>
<cfset objPDFReader.createPDF(xhtmlPath,pdfPath)>
{% endhighlight   %}

<strong>To install the library</strong> download the <a href="https://xhtmlrenderer.dev.java.net/">source</a>.

Copy:
core-renderer.jar
iText-2.0.8.jar
<a href="/get/andreacfm.jar" target="_blank">andreacfm.jar</a> ( if you want to load also my util class )

into folder WEB-INF/lib

At this point flying saucer is ready to go but I found some more details to be fixed.

<strong>DO NOT MAKE THESE STEPS ON PRODUCTION ENVIRONMENT BEFORE  TESTING YOUR APPLICATIONS.</strong>

<strong>
</strong>

<strong>For cf8 users</strong>. I have been forced to replace the xalan library that ships cf8 with the latest xalan release due to a bug that prevent the correct namespaceevaluations.
I downlaoded the xalan source from <a href="http://apache.panu.it/xml/xalan-j/">here</a>. I then copied serializer.jar,xml-apis.jar,xalan.jar,xsltc.jar and xerceImpl.jar into

WEB-INF/cfusion/lib/updates

In this way when you restart cf server the new xalan version is loaded ( update folder is at the top of jrun classpath ). This worked for me but I cannot be 100% sure that any other xml implementation of cf server will have an impact.

<strong>For Railo Users</strong>. Flying Saucer works fine with itext 2.0.8. Version 2.1.2, that ships with Railo, brakes previous code. You will need to downgrade to 2.0.8 to make it works correctly. Due to the fact that Railo is often deployed on differents Application Server this can be done in differents ways. Contact me if you want to share yoru experience on this point.
I personally added a folder to the Tomcat classpath.
