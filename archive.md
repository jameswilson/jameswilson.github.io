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
        <small><time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date_to_string }}</time></small>
      </a>
    </h3>
  </li>
{% endfor %}
</ul>
