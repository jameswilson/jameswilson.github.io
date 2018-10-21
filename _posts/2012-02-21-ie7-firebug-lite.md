---
layout: post
title: Firebug Lite for IE7
---

In cases where I need to debug dom or javascript on older browsers, I've used
Firebug Lite, which can be installed (in theory) on any browser with just a
bookmarklet.

However I found that neither of the latest versions 1.3 and 1.4 of Firebug
Lite work in Internet Explorer 7, but **version 1.2 does work**.

<p class="text-center">
<a href="http://getfirebug.com/wiki/index.php/Firebug_Lite_1.2" class="button">Firebug Lite version 1.2</a>
</p>

Also, the following bookmarklet can be used to roll your own, or just drag this link to your bookmark bar: [🚀](javascript:var%20firebug=document.createElement('script');firebug.setAttribute('src','http://getfirebug.com/releases/lite/1.2/firebug-lite-compressed.js');document.body.appendChild(firebug);(function(){if(window.firebug.version){firebug.init();}else{setTimeout(arguments.callee);}})();void(firebug);).

```javascript
javascript:var%20firebug=document.createElement('script');firebug.setAttribute('src','http://getfirebug.com/releases/lite/1.2/firebug-lite-compressed.js');document.body.appendChild(firebug);(function(){if(window.firebug.version){firebug.init();}else{setTimeout(arguments.callee);}})();void(firebug);
```
