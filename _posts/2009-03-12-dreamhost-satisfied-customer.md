---
categories:
    - Web development
layout: post
title: Dreamhost satisfied customer
created: 1236893926
---
While <a href="http://www.dreamhost.com/r.cgi?107284">DreamHost</a> certainly has its problems, I prefer them over a host of other web hosting providers for a variety of reasons, but it mainly boils down to turn around time. A colleague of mine, <a href="http://twitter.com/matthewskeith">Matt Keith</a>, had emailed me asking why I prefer DreamHost over Verve hosting, and my response got so long I decided to just turn it into a blog post. It ended up not so much being a DreamHost versus verve comparison, but a statement on why I prefer to roll with DH.

*Disclaimer: I'm part of the DreamHost affiliate program and if you end up registering after clicking one of my links, then I get a credit for the referral.*

<!--more-->

I normally get my webmastering tasks done in a timely fashion with DreamHost, but when clients go with other shared website hosting service providers like Media Temple, Verve or Bluehost, I increasingly find myself confused and end up wasting time due to their quirky setups. Certainly these unique setups are part of the nature of shared server hosting and something you have to deal with between each different host,  as there is no *de-facto* or even industry standard way to provide affordable, shared services. Hosting servers configurations vary from the very bottom, up... starting at the hardware and OS version, and all the way up to the web server software (eg Apache) configurations and limitations, database configurations, and -- perhaps most importantly -- the <strong>control panel </strong>interface. Its cumbersome to administer client sites spread across various providers where the features, terminology, and navigation systems vary widely in structure, presentation and function. Sometimes functionality that I take as a 'given' (like administering ftp and ssh accounts), one company provides as standard  while another requires a tech support request. Its sad to realize this only after having scourged through the entire panel to find the functionality doesn exist.

Well, here's an up-close and personal look at some of the things I particularly like about DreamHost:

<strong>1) Less confusion... faster turn around.</strong>

<strong></strong>I think when picking a hosting provider to go with, especially if you expect to be managing a lot of client sites, its best to pick and stick with one hosting provider.   I like DH because their account setups are logical, stuff just works, and I have a history with them now and am used to their system.  I know exactly what services and technologies DH provides, and know how to deal with their tech support, which is both email based and you can see the support history online as well.  If you have multiple clients on various hosting accounts at DH you can "see" them all from your control panel.  At the end of the day, I'd prefer to have clients unified in one place to lessen confusion.

<strong>2) Best control panel ever.</strong>

<strong></strong>Its quite possible that you could do a technical comparison of the services provided between Verve and DH and possibly come to the conclusion that Verve is better. But to me, the real tangible selling point is that DH has the most intelligent, useful, and all-encompasing control panel in the industry, period.

[caption id="attachment_159" align="aligncenter" width="440" caption="The Dreamhost Control Panel"]<a href="/files/images/dreamhost-control-panel.png"><img class="size-full wp-image-159 " title="dreamhost-control-panel" src="/files/images/dreamhost-control-panel.png" alt="The Dreamhost Control Panel" width="440" height="80" /></a>[/caption]

The control panel setup is more logical and friendly from a linux-system-admin-slash-web-developer point of view on DH than on any other host I've ever seen. They pay attention to their clients' feedback and feature requests.  DreamHost is constantly rolling out new and often complex panel features that really save webmasters lots of time and they keep their software packages up-to-date.

*Test drive the Dreamhost Demo Control Panel for yourself:*

<a href="http://demo.dreamhost.com/" target="_blank"> http://demo.dreamhost.com/</a>

Web ID: demo

Password: demo

<strong>3) Dreamhost has a huge user base.</strong>

<strong></strong>There are tons of people using DreamHost and therefore developers and sys admins can find lots of contributed solutions for non-standard configurations or cutting edge technologies that do not come "pre-installed".  <strong>DreamHost provides an excellent but suometimes dated </strong><a href="http://kb.dreamhost.com" target="_blank"><strong>knowledge base</strong></a><strong> and an even better </strong><a href="http://wiki.dreamhost.com" target="_blank"><strong>community-driven wiki</strong></a><strong>.</strong> 

The wiki provides both employee contributions as well as officially approved and some unofficial/unsupported community contributed solutions to MANY problems you encounter in your life as a shared hosting client. If you cant find it on the wiki, a web search for any issues that turns up during development and server configuration can be refined by adding the word '*dreamhost*' to your Google search terms. You'll be surprised to find the number of results -- typically from programmers' and web developers' personal blogs --  for just about any situation or error message imaginable. You'll often get the solution as well as some comments from other users encountering the same.

<strong>4) "Beyond" shared hosting...?</strong>

<strong></strong>One thing I have NOT had a chance to try out yet are the virtual private servers (<a href="http://dreamhost.com/hosting-vps.html" target="_blank">Dreamhost PS</a>). Its a relatively new offering from Dreamhost and I'm reluctant to take the plung for live sites that are doing just fine on their regular hosting. On the other hand, its nice to know that if a client's site is setup at Dreamhost and it becomes hugely popular, you have the chance to transparently migrate to Dreamhost PS and then tweak your settings, mainly RAM, to justify the demands of the site.

For big clients that need super-duper response time / dedicated / managed servers, and can pay the premium associated with that, I currently like and recommend <a href="http://carpathiahost.net" target="_blank">CarpathiaHost.net</a>. They rock but are expensive. In the end you pay for what you get there.

<strong>5) And now the kool-aid killer...</strong>

Not to purposefully end on a bad note, I thought it would be important to mention that DH does have its problems.  One of the downfalls that I have experienced are occasionally slow responses to a support request. They have a 24 hour policy for the shared hosting which they do occasionally break if they are flooded with support requests. You can, however, pay extra if you need a phone call support response. I really dont have support requests very often as I can usually figure out my problems through the intelligent suggestions they provide while going through their ticket submission system, or by browsing the wiki and/or knowledge base.

Another hiccup that sometimes happens is you get bad luck when you register and they set you up on a machine that makes your site run just plain slow.  This is usually caused by either getting setup on an older/slow machine, or more often, due to the fact that MySQL databases do not sit on the same server as the Apache web server. Your fellow DH customers sharing your database server are bogging down the shared resources and you might even end up seeing dropped db connections. I've had this problem twice with customer accounts but I've never had a problem requesting a move to another MySQL or hosting server (where your files live). Its a transparent and non-interruptive process and has always resolved the site slowness issues.

<strong>6) A word on Verve hosting.</strong>

<strong></strong>To be frank, I do not have THAT much experience with Verve. I've managed the accounts that another colleague, <a href="http://twitter.com/riversedge" target="_blank">Michael Tucker</a>, has with them, and the things that I DONT like with the minimal experience I've had include:

<ul>

	<li>their control panel feels really basic, just another system to 'figure out'.</li>

	<li>each account you are in control of has its own isolated panel, theres not an apparent way to setup various accounts and manage them all / or switch between them easily that i could see directly.</li>

	<li>their default filesystem structure for multiple domains under one account is waaay wacky (you have one 'main' domain and the rest of the domains sit inside and thus are accessible from the web of main domain)</li>

</ul>

To elaborate on that last point a little bit,  what you end up getting on your browser is essentially this:

<p style="text-align: center;">http://maindomain.com/sub.domain.com/   &lt;==&gt; http://sub.domain.com/.</p>

Some might argue that this kinda setup a good idea as backup / mock-up system while developing sites or something. But I think having this the default setup is odd. I could do this if I needed to easily on dreamhost as will with a symlink.

On a last positive note about Verve, I *was* actually able to get what I needed to get done fairly quickly in the verve panel, even though its kinda clunky at times, and it took me a little bit of time to get familiar with the setup/layout/organization/link titles/terminology.  In fact, I'd say the turn around was much faster than for learning the Media Temple and Bluehost panels.  I also should mention dont have any long term experience with Verve hosting's technical support or with trying to install non-standard technologies, so cant really offer a comparison there.
