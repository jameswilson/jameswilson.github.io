---
categories:
    - Web development
layout: post
title: DreamHost satisfied customer
created: 1236893926
---

While [DreamHost](http://www.dreamhost.com/r.cgi?107284) certainly has its problems and detractors, I prefer them over a host of other shared web hosting providers for a variety of reasons, but it mainly boils down to turn around time. <!--more--> A colleague, [Matt Keith](http://twitter.com/matthewskeith), asked me why I prefer DreamHost over Verve hosting, and my response got so long I decided to just turn it into a blog post. It ended up not so much being a DreamHost versus verve comparison, but a statement on why I prefer to roll with DH.

*Full disclosure: As part of the DreamHost affiliate program I get a credit for the referral, if you end up registering after [clicking the DreamHost link](http://www.dreamhost.com/r.cgi?107284).*

I normally get my webmastering tasks done in a timely fashion with DreamHost, but when clients go with other shared website hosting service providers like Media Temple, Verve or Bluehost, I increasingly find myself confused and end up wasting time due to their quirky setups. Certainly these unique setups are part of the nature of shared server hosting and something you have to deal with between each different host,  as there is no *de-facto* or even industry standard way to provide affordable, shared services. Hosting servers configurations vary from the very bottom, up... starting at the hardware and OS version, and all the way up to the web server software (eg Apache) configurations and limitations, database configurations, and -- perhaps most importantly -- the control panel interface. It's cumbersome to administer client sites spread across various providers where the features, terminology, and navigation systems vary widely in structure, presentation and function. Sometimes functionality that I take as a 'given' (like administering ftp and ssh accounts), one company provides as standard  while another requires a tech support request. It's sad to realize this only after having scourged through the entire panel to find the functionality doesn exist.

Well, here's an up-close and personal look at some of the things I particularly like about DreamHost:

## 1. Less confusion → faster turn around

I think when picking a hosting provider to go with, especially if you expect to be managing a lot of client sites, it's best to pick and stick with one hosting provider.  I like DH because their account setups are logical, stuff just works, and I have a history with them now and am used to their system.  I know exactly what services and technologies DH provides, and know how to deal with their tech support, which is both email based and you can see the support history online as well.  If you have multiple clients on various hosting accounts at DH you can "see" them all from your control panel.  At the end of the day, I'd prefer to have clients unified in one place to lessen confusion.

## 2. Best control panel ever

It's quite possible that you could do a technical comparison of the services provided between Verve and DreamHost and possibly come to the conclusion that Verve is better. But to me, the real tangible selling point is that DreamHost has the most intelligent, useful, and all-encompasing control panel in the industry, period.  They've spent years tweaking and improving the user experience of their control panel. It is a homegrown solution and works exceedingly well.

The control panel setup is more logical and friendly from a linux-system-admin-slash-web-developer point of view on DH than on any other host I've ever seen. They pay attention to their clients' feedback and feature requests.  DreamHost is constantly rolling out new and often complex panel features that really save webmasters lots of time and they keep their software packages up-to-date.

**Test drive the DreamHost Demo Control Panel for yourself:**

* http://demo.dreamhost.com/  **demo link no longer works**
* User ID: demo
* Password: demo

## 3. DreamHost has a huge user base

Because of their large user base it is easy to find contributed solutions for non-standard configurations or cutting edge technologies that do not come pre-installed.  The [DreamHost knowledge base](http://kb.dreamhost.com) and an even [DreamHost wiki](http://wiki.dreamhost.com) are very helpful resources.

The wiki provides official and unofficial/unsupported contributions and solutions written by both employees as community members for the many problems you encounter in your life as a shared hosting client. If you cannot find it on the wiki, a web search for any issues that turns up during development and server configuration can be refined by adding the word '*dreamhost*' to your Google search terms. You'll be surprised to find the number of results -- typically from programmers' and web developers' personal blogs -- for just about any situation or error message imaginable. You'll often get the solution as well as some comments from other users encountering the same.

## 4. Beyond shared hosting

One thing I have not had a chance to try out yet are the virtual private servers ([DreamHost PS](http://dreamhost.com/hosting-vps.html)). It's a relatively new offering from DreamHost and I'm reluctant to take the plung for live sites that are doing just fine on their regular hosting. On the other hand, it's nice to know that if a client's site is setup at DreamHost and it becomes hugely popular, you have the chance to transparently migrate to DreamHost PS and then tweak your settings, mainly RAM, to justify the demands of the site.

For big clients that need super-duper response time / dedicated / managed servers, and can pay the premium associated with that, I currently like and recommend [CarpathiaHost.net](http://carpathiahost.net). They rock but are expensive. In the end you pay for what you get there.

## 5. It's not all rosy

Not to purposefully end on a bad note, but I thought it would be important to mention that DreamHost does have its problems.  The biggest drawback that I have experienced are occasionally slow responses to a support request. They have a 24 hour policy for the shared hosting which they do occasionally break if they are flooded with support requests. You can, however, pay extra if you need a phone call support response. I really don't have support requests very often as I can usually figure out my problems through the intelligent suggestions they provide while going through their ticket submission system, or by browsing the wiki and/or knowledge base.

Another hiccup that sometimes happens is you get bad luck when you register and they set you up on a machine that makes your site run just plain slow.  This is usually caused by either getting setup on an older/slow machine, or more often, due to the fact that MySQL databases do not sit on the same server as the Apache web server. Your fellow DreamHost customers sharing your database server are bogging down the shared resources and you might even end up seeing dropped db connections. I've had this problem twice with customer accounts but I've never had a problem requesting a move to another MySQL or hosting server (where your files live). It's a transparent and non-interruptive process and has always resolved the site slowness issues.

## 6. A word on Verve hosting

I have limited experience with Verve, but have helped a colleague manage accounts there and the things that I do not like with the minimal experience I've had include:

* the Verge control panel feels really basic and convoluted, it is just *another system to figure out*.

* each account you are in control of has its own isolated panel, theres not an apparent way to setup various accounts and manage them all / or switch between them easily that I could see directly.

* their default filesystem structure for multiple domains under one account is odd. You have one primary domain and the rest of the domains sit inside and  are thus accessible from the web of primary domain. It looks something like this:

<p class="text-center">http://primarydomain.com/sub.domain.com/  &lt;==&gt; http://sub.domain.com/.</p>

Some might argue that this kinda setup a good idea as backup / mock-up system while developing sites or something. But I think having this the default setup is odd. I could do this if I needed to easily on DreamHost with a symlink.

On a last positive note about Verve, I was actually able to get what I needed to get done fairly quickly in the verve panel, even though it's kinda clunky at times, and it took me a little bit of time to get familiar with the setup/layout/organization/link titles/terminology.  In fact, I'd say the turn around was much faster than for learning the Media Temple and Bluehost panels.  I also should mention dont have any long term experience with Verve hosting's technical support or with trying to install non-standard technologies, so cant really offer a comparison there.
