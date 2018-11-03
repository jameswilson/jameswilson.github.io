---
categories:
    - Web development
tags:
    - frontend
layout: post
title: Right-To-Left Theming in Drupal with Directional SCSS
---


Directional SCSS is a useful set of SASS functions and mixins created by Tyson
Matanich in 2013 that facilitates theming multi-language sites with both left-
to-right (LTR) languages such as English, French, German, and Spanish, as well
as right-to-left (RTL) languages such as Arabic, Hebrew, and Persian (Farsi).

<!--more-->

Before we get started with Directional, it’s important to understand a bit
about Drupal’s built-in RTL mechanism. The standard Drupal site-building
workflow assumes that when you want a site that supports both LTR and RTL,
the LTR styles will be the default [see footnote 1].

When you add an RTL language the entire design is expected to be essentially
flipped horizontally.  If the menu was floated to the left, then in an RTL
language the menu should be floated to the right.

In terms of implementation, the site's default stylesheets will contain the
left-to-right styles. Then, any styles that break the site’s RTL mirror-image
design must be copied into a similarly named stylesheet with the “-rtl.css”
suffix added to the filename.

On RTL pages, Drupal automatically scans the directory structure looking for a
RTL stylesheet counterpart for every normal LTR CSS file present on the site
and when one is found it is added to the page request.

The menu styles as found on an RTL language page might include code that looks
something like the following example, which has been stripped down to the bare
essentials, for brevity and clarity:

```css
/* styles.css - Default LTR styles */
.menu {
  float: left;
  margin-left: 15px;
}
.menu li {
  display: inline-block;
}

/* styles-rtl.css - Override rules from styles.css */
.menu {
  margin-left: 0;
  margin-right: 15px;
  float: right;
}
```

There are a couple drawbacks to note with this implementation. The first and
most obvious is that any LTR styles that may bleed into the RTL must be
overridden and “nulled”. For example, the `margin-left: 0` inside
styles-rtl.css of the example above does exactly this — it removes the
`margin-left: 15px` required for LTR only.

The second less obvious drawback is that you have write duplicate code in two
separate files and then maintain these two files in sync by hand as your design
evolves.

Maintaining the LTR and RTL files in sync, to me is a deal breaker.  When
design or layout changes require that margin to be adjusted, better not forget
to change it in both places!  If the margin is removed altogether, you better
not forget to clean up that `margin-left: 0` too!

Ultimately, this methodology of inheriting LTR styles reinforces a development
strategy that makes it easier on the themer to think about RTL *after* the
design is finished.  Drupallers have come up with a methodology to help them
remember which lines need to be kept in sync using a comment in the LTR
stylesheet:

```css
  float: left;  /* LTR */
  margin-left: 15px;  /* LTR */
```

But this still leaves a lot to be desired.  Fortunately, if you’re already
using SASS in your own theme, then you can do better and hopefully save
yourself some time while developing your theme.

With Directional SCSS, we can take Drupal’s RTL methodology one step further,
to let you write all your styles once and use SASS to compile the output to two
separate stylesheets.

After downloading the “directional.scss” file from Github into your theme’s
“sass” folder, and rename it to a partial: “_directional.scss”, placing an
underscore at the front of the file name so that SASS doesn’t generate an empty
stylesheet for it in the “css” output folder.  Some themes like the Omega 4.x
framework organize custom mixins into subfolders, eg "sass/abstractions/"
folder. Next, just include the partial into your main stylesheet, and rewrite
your LTR-specific rules using the tools available rules that are compatible
with Directional SCSS.

```scss
/* styles.scss */
@import "abstractions/directional";
.menu {
  float: $left;
  margin-#{$left}: 15px;
}
.menu li {
  display: inline-block;
}

/* styles-rtl.scss */
$dir: rtl;
@import "styles";
```

The above code will generate the following CSS stylesheets:

```css
/* styles.css */
.menu {
  float: left;
  margin-left: 15px;
}
.menu li {
  display: inline-block;
}

/* styles-rtl.css */
.menu {
  float: right;
  margin-right: 15px;
}
.menu li {
  display: inline-block;
}
```

Watch out for a major caveat here: All of the code from the LTR stylesheet is
added to the RTL stylesheet, including those that are not related to RTL.  By
itself, this is not a big deal, but the problem is compounded by Drupal because
the RTL files are added but the LTR files are not removed — which has two big
effects:

RTL language pages will download both `styles.css` and `styles-rtl.css`,
effectively imposing a tax of twice the bandwidth! Styles from LTR are not
nulled out in RTL. This would produce the unwanted effect of having `padding-
left:15px` be present on the RTL version, when in reality, we only wanted and
expected the inverse: `padding-right: 15px`. Thanks Drupal!  Well, fortunately,
this is super easy to mitigate by adding the code in the following gist to your
Drupal theme’s template.php file.

{% gist 33c1f5d405119a508ceb %}

This snippet of code searches through the list of stylesheets and removes the
original LTR CSS files on pages whose language is RTL.  It is careful to only
remove those provided by your theme, leaving the rest of the stylesheets from
other modules and Drupal core alone.

That is pretty much all there is to it.  I recommend you dive into Directional
SCSS and read up about its helpful mixins and functions that help make your
Sass-based design right-to-left-friendly with [Tyson Matanich’s blog post
introduction to Directional](http://www.matanich.com/2013/09/06/rtl-css-with-sass/.

One nice feature I like to use is the `side-values` function:

```scss
/* styles.scss */
.sidebar-first {
  float: $left;
  padding: side-values(10px 5px 60px 20px);
  border-#{$left}: 1px solid #ccc;
}
```

It swaps the 5px with 20px and vice-versa for the RTL layout producing:

```css
/* styles.css */
.sidebar-first {
  float: left;
  padding: 10px 5px 60px 20px;
  border-left: 1px solid #ccc;
}

/* styles-rtl.css */
.sidebar-first {
  float: right;
  padding: 10px 20px 60px 5px;
  border-right: 1px solid #ccc;
}
```

-----

<small>footnote 1. It’s certainly debatable if Drupal’s assumption about RTL
inheriting LTR styles a good one or not, but that’s neither here nor there.
I’ve written this post from my own point of view, as a westerner implementing
a site designed for researchers of topics about the Middle East, who may speak
English, Arabic, Persian, or Hebrew. English in this case IS the default
language. I presume that for Middle Easterners who are implementing a site in
Arabic, having LTR as the default is probably a large inconvenience to them
when they want to go add English to their site.</small>
