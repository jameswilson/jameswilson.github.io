---
categories:
    - Web development
tags:
    - Drupal
layout: post
title: Contributing the Drupal 7 Navbar Dashboard icon
description: >-
  How I contributed an icon for the Dashboard module in the  Navbar module
  backported to Drupal 7.
---

For a recent client project at Bluespark, we’re using Drupal 7 with the Navbar module, also known as the [Mobile friendly navigation toolbar][1].  This module is a backport of the administration menu used in core Drupal 8.

Drupal version 8 has dropped support for the “Dashboard” module, which means there wasn’t an icon for this top-level menu item in the Drupal 7 version, leaving the main menu with an unsightly empty white space.

<!--more-->


<figure markdown="1" class="text-center">
![Screenshot of the original monotone dashboard icon we used from IconsDB](https://user-images.githubusercontent.com/243532/47868955-999f6c00-ddd3-11e8-84da-ebff3cc256a3.png)
<figcaption>
    The public domain dashboard icon from IconsDB.
</figcaption>
</figure>

So, for this client project our lead designer, Rusty Segars, found this [Public Domain dashboard icon from IconsDB.com][2]. The only problem then was that the site did not provide the image file in SVG format which is required by the Navbar module.

I was able to convert the PNG version of the icon to an SVG using a great little application called [VectorMagic][3] which started its life as a Stanford project and now has a grown up web version. The resulting SVG file worked but it needed to be resized to fit the 16 by 16 pixel dimensions needed by the Navbar menu.

I opened the resulting file in Adobe Illustrator, and resized it to fit onto a 16 by 16 canvas and saved the output. Unfortunately though, I wasn’t done there, because Adobe’s SVG output is quite bloated.  I opened the SVG file in a text editor and cleaned up the file by hand to strip out needless header tags and attributes, whitespaces and convert tabs to single spaces, etc.


<figure markdown="1" class="text-center">
<svg xmlns="http://www.w3.org/2000/svg" width="256" height="256" viewBox="0 0 16 16"><path d="M5.165,4.094c0.992-0.393,2.067-0.564,3.132-0.535c1.059,0.023,2.109,0.256,3.07,0.699 c1.036,0.475,1.971,1.168,2.713,2.033c0.901,1.055,1.534,2.342,1.783,3.714c0.09,0.481,0.13,0.972,0.137,1.464 c-0.035,0.098-0.033,0.202-0.07,0.301c-0.133,0.385-0.519,0.686-0.935,0.672c-1.487-0.008-2.976,0.006-4.459-0.008 c1.031-1.33,2.079-2.647,3.114-3.977c0.257-0.348,0.363-0.796,0.285-1.219c-0.075-0.463-0.398-0.889-0.838-1.062 c-0.568-0.221-1.258-0.097-1.7,0.322c-1.201,1.179-2.396,2.356-3.599,3.534c-0.246,0.044-0.496,0.094-0.729,0.195 c-0.852,0.377-1.479,1.262-1.469,2.203c-1.383,0.014-2.769,0-4.152,0.004c-0.212-0.004-0.432,0.026-0.635-0.054 c-0.266-0.101-0.489-0.321-0.59-0.589c-0.043-0.104-0.039-0.221-0.08-0.326c0.008-0.955,0.171-1.91,0.51-2.802 c0.363-0.959,0.915-1.851,1.613-2.603C3.072,5.202,4.071,4.527,5.165,4.094 M7.432,6.482c0.426-0.002,0.854-0.002,1.285,0 c0.016-0.664-0.004-1.334,0.01-2c-0.434-0.017-0.865,0-1.299-0.006C7.422,5.143,7.422,5.814,7.432,6.482 M4.26,5.811 C3.977,6.107,3.667,6.384,3.383,6.677C3.375,6.721,3.428,6.74,3.448,6.77c0.446,0.445,0.89,0.89,1.334,1.336 c0.299-0.293,0.597-0.59,0.897-0.877c-0.013-0.057-0.062-0.086-0.1-0.123C5.154,6.677,4.725,6.251,4.299,5.822 C4.29,5.818,4.27,5.811,4.26,5.811 M2.188,9.049c-0.051,0.424-0.113,0.846-0.16,1.271c0.662,0.082,1.32,0.18,1.982,0.257 c0.061-0.423,0.11-0.849,0.189-1.265C3.528,9.227,2.856,9.133,2.188,9.049z"/><path d="M11.405,7.943c0.203-0.18,0.545-0.238,0.767-0.053c0.155,0.127,0.186,0.359,0.123,0.543 c-0.037,0.127-0.131,0.223-0.211,0.322c-0.925,1.198-1.877,2.376-2.806,3.577c0.127,0.672-0.452,1.368-1.136,1.384 c-0.678,0.061-1.305-0.545-1.293-1.221c-0.03-0.648,0.545-1.238,1.19-1.245C9.172,10.164,10.28,9.042,11.405,7.943z"/></svg>
<figcaption>
    The final SVG for the dashboard icon contributed to Drupal.
</figcaption>
</figure>

If you plan to be doing this kind of PNG-to-optimized-SVG conversions frequently, the [svgo][4] command line application can speed up the optimization process, but for my needs this time, it was easy enough to clean up by hand.

Finally, I grabbed a copy of the Navbar module from Drupal.org’s git repository and [contributed the icon as a patch][5] back to the community.

The new icon using Drupal 7’s administration theme, and the Mobile friendly navigation toolbar module looks like this:

![navbar vertical orientation](https://user-images.githubusercontent.com/243532/47868742-06fecd00-ddd3-11e8-9d6a-7f57d5e30043.png)


[1]: https://drupal.org/project/navbar
[2]: https://www.iconsdb.com/black-icons/dashboard-icon.html
[3]: https://vectormagic.com/
[4]: https://github.com/svg/svgo
[5]: https://www.drupal.org/project/navbar/issues/2164529
