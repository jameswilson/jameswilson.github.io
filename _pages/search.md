---
layout: page
title: Search James' Blog
permalink: /search
---

<link rel="stylesheet" href="/assets/css/google-custom-search.css">
<script>
  (function() {
    var cx = '{{ site.google.search_engine_id }}';
    var gcse = document.createElement('script');
    gcse.type = 'text/javascript';
    gcse.async = true;
    gcse.src = 'https://cse.google.com/cse.js?cx=' + cx;
    var s = document.getElementsByTagName('script')[0];
    s.parentNode.insertBefore(gcse, s);
  })();
</script>
<gcse:search></gcse:search>
