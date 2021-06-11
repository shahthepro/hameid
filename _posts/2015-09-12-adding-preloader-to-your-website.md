---
id: 17
title: Adding Preloader To Your Website
date: 2015-09-12T06:30:00+00:00
author: Shah
layout: post
guid: http://hameid.net/2015/09/12/adding-preloader-to-your-website/
permalink: /adding-preloader-to-your-website/
categories:
  - Programming
tags:
  - CSS
  - JavaScript
  - jQuery
  - Preloader
  - Website Development
published: false
---
Believe it or not, Adding preloader to websites has become a new web design trend. Almost all the latest themes on [Themeforest](http://themeforest.net/?ref=shah1012) come with preloaders. Adding preloader will display a loading animation until the page has been completely loaded.

In this tutorial, I’ll show you the simplest way for adding preloaders to a website using only jQuery and CSS.

  1. Before you can add preloader to your website, Make sure that you have added jQuery to your webpage. If you haven’t already then place the following code within your `<head>` tag.
    
    * * *
    
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
        
    
    * * *

  2. Immediately after the above placed line of code, copy-paste the following code.
    
    * * *
    
        <script>
            jQuery(window).load(function(){
                jQuery(".hameid-loader-overlay").fadeOut(500);
            });
        </script>
        
    
    * * *
    
    The above code is to fade out the preloader animation once the page has been completely loaded.

  3. Now, add the following CSS code in your stylesheet. Make sure that the path to the background image is set correctly.
    
    * * *
    
        .hameid-loader-overlay {
            width: 100%;
            height: 100%;
            background: url('images/preloader.gif') center no-repeat #FFF;
            z-index: 99999;
            position: fixed;
        }
        
    
    * * *
    
    If you want a transparent background, You can use the `opacity` CSS property.

  4. Just after your `<body>` tag, Place the following piece of code.
    
    * * *
    
        <div class="hameid-loader-overlay"></div>
        
    
    * * *

  5. Refresh your page now. You should now see the preloader animation while your page is loading. We’re done, right? Not really. Disable Javascript in your browser, The preloader screen will stay forever. Not everyone has JavaScript enabled in their browser. To fix that we disable the preloader if JavaScript is disabled by adding the following within the 
    
    <head>
      tag.</p> 
      
      <hr />
      
      <pre><code>&lt;noscript&gt;
    &lt;style&gt;.hameid-loader-overlay { display: none; } &lt;/style&gt;
&lt;/noscript&gt;
</code></pre>
      
      <hr />
      </li> </ol> 
      
      <p>
        That’s it. Now, You have added preloader to your website. Also, If JavaScript is disabled in the browser, The preloader is not shown at all.
      </p>
      
      <p>
        Do share it if you like it and let me know in the comments.
      </p>
      
      <p>
        <strong>ALSO READ:</strong> <a href="https://kirukku.com/adding-page-load-progress-bar-to-website/">Adding Page Load Progress Bar To Your Website</a>
      </p>