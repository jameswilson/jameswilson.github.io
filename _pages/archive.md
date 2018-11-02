---
layout: page
title: Blog archive
permalink: /archive
---

This list of blog posts is sorted in reverse chronological order, with the most recent articles appearing first.

<ol>
{% for post in site.posts %}
  <li>
    {% include post/post-list-item.html %}
  </li>
{% endfor %}
</ol>
