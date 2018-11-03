---
categories:
    - Web development
tags:
    - frontend
layout: post
title: SVG Optimization Best Practices
description: Grab-bag of tips and tricks to improve SVGs for the web using Sketch, Adobe Illustrator, and SVGO.
---


This post is just a grab-bag of tips and tricks to improve and optimize SVGs for the web. It is divided into three sections based on the standard tooling available: Sketch, Adobe Illustrator, and SVGO.

<!--more-->

## 1. Optimizing SVGs from Sketch

Sketch is an amazing application for Mac that is vector-based, and therefore is easy to export content to SVGs, however the default SVG export settings leaves a lot of bloat and is not entirely web friendly.

To remedy, this drawback there are a few tricks that can be done to files produced from Sketch, but first and foremost, **you can avoid some of these problems by installing the [SVGO Compressor Sketch plugin by Ale Muñoz](https://www.sketchapp.com/extensions/plugins/svgo-compressor/)**.  The SVGO Compressor will do much of the hard work for you to remedy many of the issues mentioned further below automatically.  If however your designer provides you with SVGs from Sketch that are not optimized, you'll have to resort to the manual clean ups mentioned below, or [skip to section 3](#3-optimizing-with-svgo) to learn about using `svgo` on the command line.


### 1.a Kill the transforms in Sketch

Exporting an icon or logo inside a larger design comp or art board in Sketch leaves all paths with the original `x` and `y` offsets based on the relative location of the element inside the art board then uses negative values inside a`transform()` to pull things back into view. These transforms very often use floating point math with *excessive significant digits*. In addition, Sketch also exports often seemingly random values for the the `viewBox` parameter based on that same offset logic.  All of this amounts to extra digits and needless math to draw the elements.

Unfortunately the only way I know to remove the needless transform from an SVG file exported "in place" from a larger Sketch art board is to open the file in Adobe Illustrator and then re-save the image. This will simplify the positioning logic in the SVG file by removing the negative transform values and resetting the x and y offset points. This method however does not solve the problem of the viewBox.


### 1.b Use Symbols in Sketch to reset the viewBox to origin

SVGs elements inside a large Sketch art board for an entire site mockup will be exported with crazy viewBox values. The only way I've found to export icons and elements with a viewBox starting at the origin `0 0` is by using Symbols in Sketch. Designers can prevent this by converting all icons in a document to Symbols and then the developer or designer can export the Symbol to SVG.

If exporting a large set of similarly-sized icons ask the designers to create consistently sized art boards around each Symbol and center the elements appropriately. This will then translate to the viewBox starting at 0 0 and there will be no transforms.


### 1.c Remove fillrule=evenodd when possible

Most elements exported to SVG from Sketch will contain a `fillrule` attribute with a value of "[evenodd](https://www.sitepoint.com/understanding-svg-fill-rule-property/)". I've found however that the vast majority of elements do not need this attribute. If the element is simple enough then removing this rule may be possible and have no adverse effect. As with any manual SVG edits, be sure to test the results in a browser!




## 2. Optimizing SVGs inside Adobe Illustrator


### 2.a Simplify Paths

Often times Illustrator likes to make a LOT of points, particularly in curved paths.  If you remove points, you reduce the file size a lot. Select a shape in your artwork, then from the menu find: **Path > Simplify** to remove extraneous points.  Adobe has a decent averaging engine which you can tweak by changing the **angle** and **radius** sliders.  Enable "Preview" to see the before/after comparison.


### 2.b To stroke or not to stroke?

Decide whether a thin shape would be smaller as a single path with stroke or alternatively Expand the stroke and Unite the pieces.


### 2.c Make Compound Paths, reduce Groups

Select all shapes with similar colors, **Path > Compound Path > Make** then specify the color and stroke on the compound path.  Eeach <Compound path> layer will map to one single `<path>` tag in the resulting SVG, and will also rid of unnecessary Group (`<g>`) tags, and duplicate style attributes like fill and stroke.


### 2.d Manually reset viewBox to origin

Ensure the viewBox on the `<svg>` tag starts with the origin value of `0 0`. Please note however that x y values you set in the Illustrator Artboard is not always the same thing used to generate the SVG's viewBox, so modifying the Artboard in Illustrator to start at 0 0 on a document will result in a strange viewBox value on the exported SVG.

Steps to [remedy this WTF are discussed here on Stack Exchange](http://graphicdesign.stackexchange.com/questions/15401/change-viewbox-attribute-in-svg-exported-by-illustrator).  I generally just open the SVG file in a text editor and set the viewBox attribute to `0 0 X Y` where `X` is an arbitrary or ideal width, and `Y` is an arbitrary or ideal height, then reopen the SVG in Illustrator and resize/move the artwork into place above the Artboard, and re-save the file.


### 2.e Typography should be converted to paths

Depending on the type of SVG it is usually better to expand text into paths. The exception would be when you plan to inline the SVG inside HTML and the webfont you're using in the SVG is already expected to be loaded on the page.




## 3. Optimizing with SVGO

https://github.com/svg/svgo

The default options are usually good enough:

- Removes the needless `<?xml>` tag.
- Simplify the `<svg>` tag to retain only `xmlns`, `width`, `height` and `viewBox` attributes.  (Note: in some cases you can also manually later remove width and height for a truly scalable SVG.)
- Removes whitespace, indentation tab characters, new lines, etc.
- Removes / collapses useless groups (`<g>`` tags).
- Removes `<desc>` and `<title>` tags.  Note, if you're inlining your SVG it may be useful to retain the `<title>` tag to explain the image (which has a similar effect to the alt attriute on a normal image tag).
- Cleans up numerics: removes “px”, and fixes decimal precision consistently).
- Converts path definitions to either relative or origin-based positioning, based on which one generates a smaller string.

SVGO can be automated with "svgmin" for [grunt](https://github.com/sindresorhus/grunt-svgmin) or [gulp](https://www.npmjs.com/package/gulp-svgmin).




### 4. Further reading, tools and tips

Additional tools and tips for learning SVG can be read on [Web Designer Depot](http://www.webdesignerdepot.com/2015/01/the-ultimate-guide-to-svg/).


