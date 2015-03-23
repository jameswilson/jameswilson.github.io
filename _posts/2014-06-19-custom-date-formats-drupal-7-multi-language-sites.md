---
layout: post
title: Custom Date Formats for Drupal 7 Multi-language sites
---

One of the neat features of Drupal 7 is the integration between the date and
time handling, and the multi-language configurations.

If you enable the locale module, then you will be able to localize date strings
into the various languages enabled on your Drupal installation.

Custom date formats like the ones listed below may be added directly into the
Administrative interface in Drupal, but this requires in-depth knowledge of how
the PHP date formatting codes work.  Therefore, developers can save their
clients’ time and head scratching by providing the most common date formats
used around the world in code,  and non-technical client administrators may then
simply select the date format for a given language through the UI.

Out of the box Drupal provides three date formats “Long”, “Medium”, and “Short”,
all of which include the date and time. So here, we’ll provide a new custom date
format called “Post date” that we can use to exclude the time, and show only the
date.

{% gist d5cf9c14b9d112017c65 %}
