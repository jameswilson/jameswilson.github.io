---
layout: post
title: Notes from Faster Frontend Drupal, Presentation by Matt Farina
---

Notes taken from presentation at DrupalCon 2012 given by Matt Farina.
([Slideshare](http://www.slideshare.net/mattfarina))

<!--more-->

## Slideshows for mobile?

* [Flexslider](https://www.drupal.org/project/flexslider) module.

## Responsive Images

* [responsive_images](https://www.drupal.org/project/responsive_images) module.
* [adaptive image style](https://www.drupal.org/project/ais) module.
* [adaptive_image](https://www.drupal.org/project/adaptive_image) module.

Remove image styles metadata

*   The [ImageMagick](https://www.drupal.org/project/imagemagick) advanced
    module has an option to strip out metadata/


## Gzip Everything

* mod_deflate (for Apache)
* IIS (has Gzip built in)
* HttpGzipModule (for nginx)


## RoundTrip Time (RTT)

Length of time it takes to send a request and for it to come back.


## CDNs
Mobile networks have 2 to 10x longer latency than wired connections.

Cut down on parallel connections:

1.  Use CSS Imagesprites.
    *   [Glue](http://glue.readthedocs.org)
    *   [Compass](http://compass-style.org)
    *   [SpriteCow](http://spritecow.com)
    *   [SpritePad](http://spritepad.wearekiss.com)

2. Enable CSS and JavaScript aggregation

3. Adding an Expires header to components. Drupal 7 core does this already.

Go a step further and add it to scripts and stylesheets too.  Use cache busting
techniques like query string to force new downloads.

Warning: while desktop browsers have large caches, mobile browsers have a
small cache.


## Mobile Performance limitations

**Javascript can take unto 10 times longer to execute on mobile.**

* 300 ms on desktop == 3 seconds on mobile!
* 512 MB of ram on iPhone 4s (to help with battery life).
* High end: 1gb of ram on iPad 2.

Mitigating Mobile Performance issues:

1. Nothing fancy with JavaScript.

2. !!!Simpler DOM!!!  (cure divitis) A simpler dom has less objects in memory.

3. Mobile Optimized Images, use responsive images, to use less ram to render.


## Advanced concepts and configs

Use browser "local storage".

Minify HTML  (htmlcompressor)  hook_page_delivery_callback_alter,
drupal_deliver_html_page.

mod_pagespeed: Apachemodule to optimize web pages

Delayed JavaScript Evaluation:  all js icnluded must be parsed and evaluated
before it becomes avail. Jquery on iphone 4, takes 320ms to parse and evaluate.
Lazy Evaluation waits until JS is needed to evaluate it.

Update Linux Kernel to 3.3 increases TCP initial congestion window to 10. This
can cut down the number of round trips to get data: google and microsoft already
do this.


## Tools & Resources

* [Google Pagespeed](http://developers.google.com/pagespeed/)
    alternative to YSlow! See also:
    [Google articles on speed](http://code.google.com/speed/articles)

* [Mobile Perf Bookmarklet](stevesounders.com/mobileperf/mobileperfbkm.php):
    Analyze on mobile and store data to analyze on desktop.

* [webpagetest.org](http://webpagetest.org):
    tests performance from various places in the world, with comparisons and
    videos over time.

* [HTML5 Mobile Boilerplate](http://github.com/h5bp/mobile-boilerplate)

* **Chrome Developer Tools**: Network tab.

