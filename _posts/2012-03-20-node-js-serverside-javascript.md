---
layout: post
title: Node JS - Serverside javascript.
---


Server side javascript, in V8 -- Chromes javascript engine.


Jeff Micollis, got burned on:


## 1. Sending lots of email.

single emails, digests… notifications module.

clients want more: sms twitter, etc:   channel independent messages.

Problems:

- send email upon "save".
- 50 ms to send an email to one user.
- 28 users ==> 1.4 seconds.
- 600 users ==> 30 seconds.

Solution: send emai on cron run, e.g. every 5 minutes.
But, if one run doesn't complete…. more problems.


In node.js  you can queue up emails, send them… 600 emails in ~3 seconds.

Node allows asynchronous interaction with IO, managed by OS.



## 2.  Handling feeds.

the task: fetch a lot of rss feeds, fetch original article, tag items (calais)
tag items (watch list) tag items (wikipedia) geocode items

Thousands of feeds, millions of items, 4.5 Gigs of data.

Problems:  cron.php

before node js existed, they wrote "maggied" multi-threaded python daemon to
access drupal database and do stuff.

* 4 "retreiver" workers get batches of 50 items.
* fetch/tag/geocode each item

    retreive original story: 300ms
    tag: 100ms
    geocode: 150ms
    TOTAL 550ms  per story!

Nearly all of that time is spent idle on the server waiting on 3rd party
responses.

Replace the retrievers with a single hyperactive squid. (hamsters bunnies and
squids) ==> google it.

The squid runs up and down as fast as it can dealing with each item in turn. it
fires of any long running i/o operations and moves on to the next mite. When the
io operation reports progress.

Event Loop: 100% async.
The reason it can do this is that anything that leaves v8 takes a callback.
- filesystem, network, stdio, timers, child processes.

In node js these ^ look different than typical PHP processing.

```javascript
var fs = require('fs');
fs.readfile('/etc/passwd', function (err, data) {
if (err) throw err;
console.log(data);
});

var request = require('request');
request('http://example.com', function (err, ….
```

Limiting factors change: how many open sockets are you allowed, how much
bandwidth can you grab, how fast can you issue requests?

## 3. big data…

big file uploads in php:  upload_max_filesize, post_max_size max_input_time max_execution_time

This approach caps out around ~500mb

Opens the door to DoS, tolerates application bloat. problems in production can get really bad, never gonna achieve gigabyte uploads. PHP makes you look elsewhere for big uploads.

is streaming possible?  Deal with things bucket by bucket. and you don't need all that memory.
Write files to disk as it comes in. or stream it off to s3, so you don't worry about overloading your local disk.

In node js, this becomes a lot more possible with the "formidable" library (open sourced).


Sidenote: CouchDB: _changes

persistent HTTP connection to database…. which feeds you new data when it has some.


## 4. Package Management for Drupal

(drush make)
d.o - project namespace
d.o - inclusive project policy
a way to stay sane.

But, I'd been using drupal Drupal for YEARS by then.

pear: PHP extension and application repository.

what if pear was wildly inclusive, awesomely useful awesomely successful?

NPM: node package manager is wildly inclusive, awesomely useful, awesomely successful.

PEAR: 584,
D.o: 15,296 (~3,600 for D7)
NPM: 7976 (and is only 2 years old!)


## 5. Use with caution.

"javascript really?"

node.js is bad for:

*   computationally heavy tasks (e.g., crypto) things that tend to occupy all
    the memory.
*   databases

node.js is awesome for:

*   interacting with other services, like: databases, mail servers, web
    services, web clients…



many node js projects just handle a one single thing (small surface area) that handles all the details.

you can feed a callback to *anything*, any service, that gives you data back from the response.

all asynchronous by default

