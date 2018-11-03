---
categories:
    - Web development
tags:
    - Drupal
layout: post
title: Drupal 7 multilingual investigation
---

List of modules and step-by-step configurations to get a multi-lingual setup working with *Content Translation (locale) module*.  For installation with *Entity Translation* see [the other post](/2014-10-23-los-abc-de-multi-idioma) (in Spanish).

<!--more-->

First I installed the Locale module.

This is the base of what you need to define the languages for your site, and
define how/when to choose a language to display to the end user.  More details
can be found on [Gabor's first installment on his blog][gabor].

After reading Gabor's write-up, I realized that I'll be needing quite a few
more modules to get a fully multi-lingual site working. So I decided to start
making a list of multilingual modules and what they are needed for:


**Localization update** ([l10n_update][l10n_update]) - Figures out which
modules your site uses, and keeps the translations up to date with
localize.drupal.org.

**Localization client** ([l10n_client][l10n_client]) - A module that lets you
create interface translations on the fly, and contribute them back to
localize.drupal.org

**Content translation** (locale) - Core Drupal module for translating content.

**Internationalization** ([i18n][i18n]) - This is a collection of modules to
extend Drupal core multilingual capabilities and be able to build real life
multilingual sites. Some features:

*   _Taxonomy translation_, both per language terms and translatable terms.
*   _Multilingual variables & Multilingual blocks_ to control visibility per
    language and translate title and content
*   _Language selection_ when you switch the site language you'll see only
    the content for that language.

**Variable** -  the i18n module for Drupal 7 depends on the variable module.

After having a basic list of modules, I found it helpful to write down the
steps needed to setup a real multi-lingual site in Drupal 7:

### Step 1: Setup languages.

In order to have an international site, you must *first determine the languages
you want to support*, and the rules for *language mitigation* (eg session,
path-prefix / domain name, user setting, etc). All of this can be done with
Drupal's core Locale module.


### Step 2: Update Drupal core and contrib modules.

Before you start translating a bunch of strings, it would be beneficial to have
the latest-greatest version of Drupal modules, so that your time is not wasted
translating potentially outdated strings.


### Step 3: Translate the interface.

Before you start translating the content on the site, you'll definitely get a
lot farther if you import existing translations that others have made based on
strings of text provided in the Drupal interface.  *Install the Localization
update module.*

Once installed, a new tab is added to `admin/config/regional/language` called
_Translation Updates_ where you can administer these updates. You need to
specify the location to store downloaded files, typically
 `sites/all/translations`.

Additionally, _Home » Administration » Configuration » Regional and language
» Translate interface_ will now have a tab titled _Update_ which lets you
review your localization update status and perform outstanding updates.
Visit the update page, and update all the strings, to download the most recent
translations from localize.drupal.org.


### Step 4: Translate content.

This is probably the most complex step, and it requires a veritable concert of
contributed modules to get the job done.  The Internationalization (i18n)
module will be the basis for content translation workflows on the site.

The [i18n project page][i18n] lists a plethora of other translation modules
available that can be installed & configure according to the site's needs.

Enable multi-lingual support on various content types.


### Step 5: Update existing content.

All existing content on the site will have their language setting set to
"Language Neutral". Even if you've specifically disallowed this setting in the
administrative panels. You must update the language for all content from
Language Neutral to the default language, in  our case, "English".  This ensure
that the Translate tab  appears for translators on the node's page.


### Step 6: Translate Contact form.

Install tcontact module to translate the different categories (to potentially
send inquiries to different people). To enable translation of the "Additional
Information" text (Contact Form Settings), add the following line to your
site's settings.php file (requires Internationalization):

```php
$conf['i18n_variables'][] = 'contact_form_information';
```

### Step 7: Translate Blocks

Some blocks need to be translated, others simply will be out of context on
foreign language translations. Use the i18n_block (depends on i18n,
i18n_string, and variable api modules) to add an extra 'Language' tab under
visibility settings on all blocks.


[gabor]: http://hojtsy.hu/blog/2011-jan-19/drupal-7039s-new-multilingual-systems-part-1-basics
[i18n]: https://www.drupal.org/project/i18n
[l10n_update]: https://www.drupal.org/project/l10n_update
[l10n_client]: https://www.drupal.org/project/l10n_client
