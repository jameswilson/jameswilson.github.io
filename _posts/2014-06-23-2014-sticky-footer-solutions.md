---
categories:
    - Web development
tags:
    - frontend
layout: post
title: 2014 Sticky Footer Solutions
---

While working on a Drupal distribution of sorts that offers a number of
different themes included, I needed to look for a clean, generic, reusable and
inheritable Sticky Footer to be packaged in a base theme. The feature needed
to be toggleable on or off in sub-themes as necessary.

Searching Google always turns up a number of competing solutions, so I've
consolidated the research here in a list of 4 basic options presenting the
pros and cons of each.

<!--more-->

## 1. The Classic CSS Sticky Footer  (html5 version here):

Pros:

* CSS/HTML only.
* No javascript or extra HTTP requests needed.

Cons:

*   Requires the footer height be known, and set to a fixed value in CSS.
*   Requires non-semantic HTML code structure changes.
*   Doesn't work well when using dynamic content such as from a CMS.
*   Doesn't work well for responsive designs, where height may change
    dynamically based on contents and width of screen.

## 2. A Responsive Sticky Footer CSS solution using `display:table-row`

Pros:

*   Don't need to know the height of the footer.
*   Is a responsive solution.

Cons:

*   Could be considered a hack, due to CSS use of `display:table-row`.
*   Can cause layout/display issues or break the site design of some sites,
    requiring more time and attention to fix.

## 3. The CSS Flexbox solution.

Pros:

*   Zero HTML code changes required.
*   Very little CSS code (5 or 6 lines).
*   Snappy response time and no display issues (requires no JS event
    listeners or processing).
*   Could be the best choice as a _progressive enhancement_ if stakeholders
    are willing to accept limited browser support.

Cons:

*   Flexbox still has rather [poor browser support][1],, many current browsers
    still require vendor prefixes.
*   Would require a fallback solution for supporting IE9 and below.

## 4. A Javascript-based responsive solution.

Pros:

*   Encapsulated solution - contained in a single javascript file, may be
    placed in the base Casa theme, and then automatically inherited (or
    specifically disabled) by any sub-theme.

Cons:

*   Performance -  extra HTTP requests.
*   Maintainability - Adds more jQuery/javascript bloat.
*   Hacky - Requires extra code to listen for screen resize, and to restrict
    itself from overloading the browser.

Here is the above information condensed into a table format:

<table border="1" width="100%" cellspacing="0" cellpadding="2" style="width: 100%;">
<tbody>
<tr>
<td valign="top"><b>Solution</b></td>
<td valign="top"><b>Responsive</b></td>
<td valign="top"><b>Browser Support</b></td>
<td valign="top"><b>Pure CSS</b></td>
<td valign="top"><b>Clean (No hacks)</b></td>
</tr>
<tr>
<td valign="top">
<div><strong><a href="http://ryanfait.com/sticky-footer/" target="_blank">Classic CSS Sticky Footer</a></strong></div>
</td>
<td valign="top">No</td>
<td valign="top">Yes</td>
<td valign="top">Yes<br></td>
<td valign="top">No; some non-semantic html is required.</td>
</tr>
<tr>
<td valign="top">
<div><strong><a href="http://galengidman.com/2014/03/25/responsive-flexible-height-sticky-footers-in-css/" target="_blank">Responsive Sticky Footer CSS solution using display:table-row</a></strong></div>
</td>
<td valign="top">Yes</td>
<td valign="top">
<div>Yes</div>
</td>
<td valign="top">Yes</td>
<td valign="top">Maybe; some consider using display:tables-row is not good use of CSS.</td>
</tr>
<tr>
<td valign="top">
<div><strong><a href="http://philipwalton.github.io/solved-by-flexbox/demos/sticky-footer/" target="_blank">CSS Flexbox solution</a></strong></div>
</td>
<td valign="top">Yes</td>
<td valign="top">No</td>
<td valign="top">Yes</td>
<td valign="top">Yes</td>
</tr>
<tr>
<td valign="top">
<div><strong><a href="http://blog.mojotech.com/responsive-dynamic-height-sticky-footers/" target="_blank">A Javascript-based responsive solution</a></strong></div>
</td>
<td valign="top">Yes</td>
<td valign="top">Yes</td>
<td valign="top">No</td>
<td valign="top">Maybe; requires extra code to listen for screen resize and to restrict itself from overloading  the browser.</td>
</tr>
</tbody>
</table>


[1]: http://caniuse.com/flexbox
