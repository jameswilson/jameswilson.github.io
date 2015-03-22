---
layout: page
title: Blog archive
---

Posts sorted in reverse chronological order.

<ul class="related-posts">
{% for post in site.posts %}
  <li>
    <h3>
      <a href="{{ page.baseurl }}{{ post.url }}">
        {{ post.title }}
        <small>{{ post.date | date_to_string }}</small>
      </a>
    </h3>
  </li>
{% endfor %}
</ul>
