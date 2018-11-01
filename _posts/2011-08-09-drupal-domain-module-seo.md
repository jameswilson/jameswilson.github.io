---
layout: post
title: Domain module investigation
description: a brief investigation about viability of the Domain module for Drupal 7.
---

The following is a brief investigation about viability of the Domain module for Drupal 7.

<!--more-->

### 1) Sharing / Restricting views:

The Domain Views module will let us specify access restrictions for each view,
to restrict access to a single domain.  This will be used to block almost all
the views from being shared (eg the dealer search view, the blog view, etc).
The products views will be shared on the two domains, so no change is needed
there, but I will need to write logic into a custom tpl file for the uc_product
view, to remove the link to the actual product page.

### 2) SEO impact of domain module.

We need to be weary of negative impacts of SEO from the domain module, there
are two potential ways I can see the module negatively impacting SEO:

*   no canonical urls are shown for content that is published to both domains.
*   no canonical urls are shown for views that are accessible on both domains.
*   the xmlsitemap module may be publishing a LOT more duplicate information than
    we may be aware. Each entry in the sitemap needs to be reviewed, page by
    page to ensure there is a solution for every case of duplicate content.
*   we must double check how a canonical url solution affects the <front> page.

### 3) Potential solutions:

Canonical URLs support in Domain Access D7 has inbuilt canonical url support,
there is a patch for D6 version, but it only works with nodes/regular content,
and apparently nothing else.

Canonical_URL deprecated in favor of nodewords 1.2

Use NodeWords (6.x-1.x-dev) and Domain_Meta module, to integrate Nodewords with
Domain Access.
