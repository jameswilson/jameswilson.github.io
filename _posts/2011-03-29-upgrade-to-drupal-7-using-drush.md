---
categories:
    - Web development
tags:
    - Drupal
layout: post
title: Upgrade Drupal 6 to Drupal 7, a practical example with Drush.
---

These instructions work with updating a real production site, namely our
Bluespark.com public website, first locally on a development environment,
using Subversion as our source control management tool.  In this case, we
develop (and test the upgrade) from svn trunk, locally, and have production
on a tag.  We use drush (version 4.4) to do much of the heavy lifting.  In
order to use drush during the upgrade procedure, you will need to have access
to an internet connection.

<!--more-->

I partially followed the instructions here:

(http://drupal.org/node/938430#comment-4250344)

## Step 1: Update Drupal 6 modules.

First thing's first. We need to ensure all our D6 site's modules (including
core and contrib modules) are up-to-date.  In our case we're runing the -dev
version of cck and mobile_tools, and so these were the only modules that
were updated:

```bash
$ cd /path/to/local/d6
$ drush up -y
```

Commit these changes to your source control repository,  take a database
snapshot, and tag them (we use subversion).

```bash
$ svn ci -m "Updated modules XYZ to latest -dev snapshot".
$ svn /// tag command here ... fill this out later
```

We want to run the upgrade using drush, let's see if drush can tell us how
to do that:

```bash
$ drush help
```

I see that there is a command  `drush site-upgrade`  (or `drush sup` for
short). Let's try that.

```bash
$ drush sup
  Missing argument: target
```

Hrm.... ok,  RTFM:  `drush help sup` shows me that I need to specify a @target, and I can do this using a drush alias. Let's copy the example alias file provided by drush to our webroot and implement a simple alias like the one they recommend.  I'm going to put it in a different folder to start with than the current d6 folder.


```bash
$ sudo cp /path/to/drush/examples/example.aliases.drushrc.php aliases.drushrc.php
$ sudo chmod 777 aliases.drushrc.php
$ vim aliases.drushrc.php
```

I uncomment the lines that define the "dev"  alias (near the very bottom of the file), and duplicate them, creating an "onward"  alias:

```php
$aliases['dev'] = array(
 'uri' => 'd6.local',
 'root' => '/path/to/local/d6',
);
$aliases['onward'] = array(
  'uri' => 'd7.local',
  'root' => '/path/to/local/d7',
);
```

Ok, let's try it:

```bash
$ cd /path/to/local/d6
$ drush sup @onward
```

The drush output was the following:

```
The project admin has no releases in version 7                        [warning]
The project admin_menu has no releases in version 7                   [warning]
The project  has no releases in version 7                             [warning]
The project bot has no releases in version 7                          [warning]
The project cck has no releases in version 7                          [warning]
The project link has no releases in version 7                         [warning]
The project ctools has no releases in version 7                       [warning]
The project context has no releases in version 7                      [warning]
The project imagecache_actions has no releases in version 7           [warning]
The project jcarousellite has no releases in version 7                [warning]
The project nodewords has no releases in version 7                    [warning]
The project mobile_tools has no releases in version 7                 [warning]
The project backup_migrate has no releases in version 7               [warning]
The project bueditor has no releases in version 7                     [warning]
The project globalredirect has no releases in version 7               [warning]
The project imce has no releases in version 7                         [warning]
The project mollom has no releases in version 7                       [warning]
The project page_title has no releases in version 7                   [warning]
The project path_redirect has no releases in version 7                [warning]
The project pathauto has no releases in version 7                     [warning]
The project search404 has no releases in version 7                    [warning]
The project seo_checklist has no releases in version 7                [warning]
The project site_map has no releases in version 7                     [warning]
The project skinr has no releases in version 7                        [warning]
The project token has no releases in version 7                        [warning]
The project droptor has no releases in version 7                      [warning]
The project google_analytics has no releases in version 7             [warning]
The project imce_wysiwyg has no releases in version 7                 [warning]
The project jquery_plugin has no releases in version 7                [warning]
The project wysiwyg has no releases in version 7                      [warning]
The project views has no releases in version 7                        [warning]
The project xmlsitemap has no releases in version 7                   [warning]
The following contrib modules were enabled in your Drupal site,            [ok]
but are now standard in core: adminrole, filefield, imagefield,
imageapi, imageapi_gd, imageapi_imagemagick, imagecache,
imagecache_ui, poormanscron.  These modules may need to be
reconfigured after the upgrade is complete.
You are using the project cck, which requires data migration          [warning]
or other special processing.  Please see
http://drupal.org/project/cck and http://drupal.org/node/895314
for more information on how to do this.
You are using the project filefield, which requires data migration    [warning]
or other special processing.  Data migration for this module will
be provided by the Content Migrate submodule of cck.  Enable
content_migrate after upgrading; see http://drupal.org/node/781088.
You are using the project imagefield, which requires data migration   [warning]
or other special processing.  Data migration for this module will be
provided by the Content Migrate submodule of cck.  Enable
content_migrate after upgrading; see http://drupal.org/node/781088.
You are using the project token, which requires data migration or     [warning]
other special processing.  In Drupal 7, the contrib token
module handles UI, as well as field and profile tokens; all other
functionality has been migrated to core.
Based on the contrib modules enabled in this site, it is possible     [warning]
that the site-upgrade command might fail.  See warnings above.

Drupal site already exists at ~/Sites/Bluesparklabs/d7.  Would you like to:
 [0]  :  Cancel
 [1]  :  Delete the existing site and start over.
 [2]  :  Re-use the existing code, re-import the database from the source
         site and run updatedb again.
1

Install location ~/Sites/Bluesparklabs/d7 already exists.
Do you want to overwrite it? (y/n): y

Project drupal (7.0) downloaded to ~/Sites/Bluesparklabs/d7.          [success]
Project drupal contains:                                              [success]
 - 3 profiles: testing, standard, minimal
 - 4 themes: stark, seven, garland, bartik
 - 47 modules: drupal_system_listing_incompatible_test,

drupal_system_listing_compatible_test, user, update, trigger, translation,
tracker, toolbar, taxonomy, system, syslog, statistics,simpletest, shortcut,
search, rdf, profile, poll, php, path, overlay, openid, node, menu, locale,
image, help, forum, filter, file, field_ui, text, options, number, list,
field_sql_storage, field, dblog, dashboard, contextual, contact, comment,
color, book, blog, block, aggregator

You will destroy data from onwarddb and replace with data from bluesparklabs.

You might want to make a backup first, using the sql-dump command.

Do you really want to continue? (y/n): y

ERROR 1044 (42000) at line 1: Access denied for user
'bluesparklabs'@'localhost' to database 'onwarddb'
ERROR 1044 (42000): Access denied for user 'bluesparklabs'@'localhost'
to database 'onwarddb'

Command site-upgrade-prepare needs a higher bootstrap level to run      [error]
- you will need invoke drush from a more functional Drupal environment
to run this command.

The drush command 'site-upgrade-prepare admin adminrole admin_menu      [error]
bsp_tools bot bot_factoid bot_karma bot_log bot_seen bot_tell
bot_agotchi content content_copy filefield imagefield link
nodereference number optionwidgets text ctools context context_ui
imageapi imageapi_gd imageapi_imagemagick imagecache
imagecache_canvasactions imagecache_ui jcarousellite
jcarousellite_views nodewords nodewords_basic nodewords_extra
nodewords_verification_tags mobile_tools backup_migrate bueditor
globalredirect imce mollom page_title path_redirect pathauto
poormanscron search404 seochecklist site_map skinr token
path_alias_cache droptor googleanalytics imce_wysiwyg
jquery_plugin wysiwyg views views_ui xmlsitemap xmlsitemap_node
adaptivetheme_mobile iwebkit spark_2010 spark_new_media
spark_portfolio_dark spark_portfolio_lite' could not be executed.

Drush was not able to start (bootstrap) the Drupal database.            [error]
Hint: This error often occurs when Drush is trying to bootstrap a site
that has not been installed or does not have a configured database.

Drush was attempting to connect to :
  Drupal version    : 6.20
  Site URI          : onwarddb
  Database driver   : mysql
  Database hostname : localhost
  Database username : bluesparklabs
  Database name     : onwarddb
  Default theme     : garland
  Administration theme: garland
  PHP configuration : /Applications/MAMP/conf/php5.3/php.ini
  Drush version     : 4.4
  Drush configuration:
  Drush alias files : ~/.drush/aliases.drushrc.php
~/Sites/BluesparkLabs/public/aliases.drushrc.php
  Drupal root       : ~/Sites/BluesparkLabs/public
  Site path         : sites/onwarddb
  Modules path      : sites/all/modules
  Themes path       : sites/all/themes
  %paths            : Array
```


You can select another site with a working database setup by specifying the
URI to use with the `--uri` parameter on the command line or `$options['uri']`
in a `drushrc.php` file.

The first time you run through you may want to cancel the procedure in order
to read all the text that flew by, spit out by Drush.  It is likely that it
won't be able to complete the upgrade anyway because we haven't specified
a "db-url" for our new site.  Not to worry!  Drush site-upgrade has been
written in a way that allows you to iteratively make changes to re-run the
upgrade as many times as you like.

I see that drush is telling me that there are various contributed modules that
either:

a) aren't supported by Druapl 7 yet,
b) have been subsumed into Drupal 7 core, or
c) will require additional steps in order to ensure correct update.

Drush provides me with some links for further information so Let's check that
out first.

http://drupal.org/project/cck -- upgrade procedures for cck.
http://drupal.org/node/895314 -- upgrade procedures for filefield.
http://drupal.org/node/781088 -- upgrade procedures for imagefield.

There is a growing list of modules no longer needed after Drupal 6 on
http://drupal.org/node/895314 read about them, before updating and maybe
we can disable them, before the upgrade.

Note: `drush pml | grep Enabled` will show you the list of modules currently
enabled on your site.

After reading up, you should retry the upgrade procedure.  This time, I want to
specify the correct database,  so I'll create a database called "d7" and I'm
going to add a `db-url` entry to `my aliases.drushrc.php`

```php
$aliases['onward'] = array(
  'uri' => 'd7.local',
  'root' => '/path/to/local/d7',
  'db-url' => 'mysqli://d7:d7@localhost/d7'
);
```

With a correct database setting you may see an error message like this:

```
ERROR 1044 (42000) at line 1: Access denied for user 'd6'@'localhost' to
database 'd7'
```

This is a known issue for drush may be disregarded.

At various points throughout the update, you may be required to choose a
specific module version, if there are not a single recommended version. For
example, the imagecache_actions module prompts you with the following:

```
There is no recommended release for project imagecache_actions.
Choose one of the available releases:
 [0]  :  Cancel
 [1]  :  7.x-1.x-dev  -  2011-Mar-15  -  Supported, Development
 [2]  :  7.x-0.0      -  2011-Feb-03  -  Supported
```

I've decided to go with the latest greatest, so I'm going to type '1' and hit
enter here.

Also note, if you happen to be running the upgrade procedure multiple times or
have specified a folder where you've already downloaded Drupal 7, you may be
promted about what you want to do to continue the upgrade:

```
Drupal site already exists at ~/Sites/d7.  Would you like to:
 [0]  :  Cancel
 [1]  :  Delete the existing site and start over.
 [2]  :  Re-use the existing code, re-import the database from the source site and run updatedb again.
```

After the update completed.  I went to the site and got a very obscure error:

[[image]]

I looked in the watchdog table to see if anything was logged.  Nothing.

I also checked the php and apache log files, nothing there either.

Finally, I proceeded to check the `update.php` in a browser to ensure the
updates had actually executed, and found that there were still 22 pending
updates. So I ran them, and got the following error:

> The update process was aborted prematurely while running update #6201 in
imagecache_canvasactions.module. All errors have been logged. You may need to
check the watchdog database table manually.

The actual error message was:

```
Fatal error: Call to undefined function imagecache_presets() in ~/Sites/d7/sites/all/modules/imagecache_actions/canvasactions/imagecache_canvasactions.install on line 37
```

I also encountered two additional failed database update errors during the
update procedure.

```
backup_migrate module

Update #2001
Failed: DatabaseSchemaObjectDoesNotExistException: Cannot add field
backup_migrate_profiles.filters: table doesn't exist. in
DatabaseSchema_mysql->addField() (line 321 of
~/Sites/d7/includes/database/mysql/schema.inc).

skinr module

Update #7002
Failed: DatabaseSchemaObjectDoesNotExistException: Cannot add field
skinr_rules.rule_type: table doesn't exist. in DatabaseSchema_mysql->addField()
(line 321 of ~/Sites/d7/includes/database/mysql/schema.inc).
```

I proceeded to search for the errors in the module issue queues on drupal.org,
starting with the imagecache_actions module, which turned up nothing. So then
proceeded to dig into the actual error, by reading the module code.

*   The error seemed to have happened because the imagecache_actions module
    assumes (probably correctly) that the imagecache module is enabled already,
    so that it can use the function imagecache_presets().  I need to look at
    why imagecache is disabled.

*   Another thing to consider is do I really need this module anymore?

In this case, I took a look at the d6 site, and realized that the only reason
the imagecache_actions existed was to put a 4 pixel grey (#595959) border
around a 'thumbnail'  preset (via the imagecache_canvasactions sub-module).
(Hey, who the heck built this site anyway!?!)  Borders can be easily done in
CSS! Perfect! Modify the preset, disable "Imagecache Canvas Actions" on the D6
site and potential problem resolved!  The theming will be handled later.


I'll mention here quickly that yesterday while running through upgrades, I found and submitted a patch to fix an error in the upgrade procedure for backup_migrate module:

After disabling imagecache_canvasactions module in d6 and re-running the site-upgrade, I am now getting another error from backup migrate:

```
Base table or view not found: 1146 Table                               [error]
'bluesparklabs_d7.backup_migrate_destinations' doesn't exist:
SELECT * FROM {backup_migrate_destinations}; Array() in
backup_migrate_item->all_items() (line 632 of
~/Sites/d7/sites/all/modules/backup_migrate/includes/crud.inc).
```

Not sure whats this about, but scanning the issue queue for the Backup &
Migrate module suggest that there are still issues revolving around update.

I could take time to try to investigate the issue and fix it, but based on the
low probability that a fix for this single issue will be enough to result in a
successful migration, I've decided to simply disable the module, and
reconfigure it from scratch in D7.

The next re-upgrade was met with the following errors:

```
Do you wish to run all pending updates? (y/n): y
^@The external command could not be executed due to an application      [error]
error.
WD php: Warning: Invalid argument supplied for foreach() in           [warning]
views_update_6011() (line 482 of
~/Sites/d7/sites/all/modules/views/views.install).
WD php: Warning: Invalid argument supplied for foreach() in           [warning]
skinr_update_7001() (line 266 of
~/Sites/d7/sites/all/modules/skinr/skinr.install).
WD php: Warning: Invalid argument supplied for foreach() in           [warning]
skinr_update_7001() (line 266 of
~/Sites/d7/sites/all/modules/skinr/skinr.install).
Cannot add field skinr_rules.rule_type: table doesn't exist.            [error]
Drush command terminated abnormally due to an unrecoverable error.      [error]
Error: Call to undefined function context_load() in
~/Sites/d7/sites/all/modules/context/context.install, line 292
Output from failed command :                                            [error]

Fatal error: Call to undefined function context_load() in
~/Sites/d7/sites/all/modules/context/context.install on line 292
```

I decided to disable the skinr module. The project page on d.o says that the
7.x branch is under heavy development, and furthermore, though the D6 site
depended on this for some sidebar block tweaks, we probably will not even need
this module going forward, due to the re-theming that will have to take place
anyway. Farewell skinr, thanks for the ride.

The views error is slightly more harrowing, because currently there is no
supported views upgrade path! Essentially, this means we'll need to rebuild the
views by hand in D7, a potentially disastrous step if your site depends heavily
on views!  Consider this step wisely.

The final error there is for the context module. We happen to be running the
6.x-3.x code which is the latest, greatest version, and the Drupal 7 branch is
also at 3.x which is essential. There were no mentions of this error in the
module's issue queue so I'm going to have a look at fixing it.

After a bit of digging, it turned out that this was a drush error in the site-
upgrade, which created some condition where the module wasn't loaded while
running the module's update script.  I ran drush updatedb by hand and did not
get this error again, and after disabling the skinr module on the D7 install,
was able to get through a drush updatedb cleanly and the site finally loaded
for the first time in D7!  Yay!


Visiting the D7 site public pages, some notable things are missing:

*   imagefield cck field data did not get migrated.
*   all the views have broken/missing handlers.
*   the page_title module breaks page titles on all pages, because of the
    changes in the Token module
*   path aliases will have to be reconfigured and rebuilt.

Everything looks good on /admin/reports/status.

I proceeded to set up a new branch for Drupal 7 <!--at
https://svn.bluesparklabs.com/bluespark/branches/drupal7 --> and checked that
out to the folder where drush downloaded and created the Drupal 7 site locally.

```bash
$ cd /path/to/d7
$ svn co https://svn.bluesparklabs.com/bluspark/branches/drupal7 .
```

(The period at the end is required).

Before committing everything, I decided I needed to clean up the modules that
were downloaded by drush automatically, to restructure the folder using the
convention we had in place for Drupal 6: placing custom modules in
sites/all/modules/custom  and contrib modules from drupal.org in
sites/all/modules/contrib.


```bash
$ mv sites/all/modules sites/all/contrib
$ mkdir -P sites/all/modules/custom
$ mv sites/all/contrib sites/all/modules
```

At that point, I added all the core Drupal files and folders...

```bash
$ svn add *.* profiles/ misc/ modules/ themes/ includes/ scripts/ .htaccess
$ svn add -N sites
$ svn add -N sites/all
$ svn add -N sites/all/modules
$ svn add -N sites/all/modules/contrib
$ svn add -N sites/all/modules/custom
$ svn add -N sites/all/themes
$ chmod 775 sites/default && svn add sites/default
$ svn add sites/example.sites.php
$ svn add all/README.txt all/themes/README.txt all/modules/README.txt
$ svn commit -m "D7 Upgrade: initial commit of Drupal 7 core codebase."
```

Previously I had replaced a couple of the modules downloaded by drush with a
version straight out of the git.drupal.org, so I decided to look first for any
git repos to make sure those dont get committed.  That needs special handling
during the `svn add` step.

```bash
$ cd sites/all/modules/contrib
$ find . -name '.git'
./backup_migrate/.git
```

Backup & Migrate was the only module that I ended up submitting a patch for
(so far) so I'll handle this special case first.  I should have set this up
before working on patches.

```bash
$ svn add -N backup_migrate
$ svn propset svn:ignore ".git" backup_migrate
$ svn add backup_migrate/*
$ svn commit -m "Added Backup_Migrate latest 7.x dev snapshot."
```

Then, one by one I began adding in each module, noting the version in the
commit statement.


```bash
$ svn add admin
$ svn commit -m "Added Admin 7.x-2.0-beta3"
$ svn add admin_menu
$ svn commit -m "Added Admin_Menu 7.x-3.0-rc1"
```
[...]

I also re-created the BSP_Tools module,  adding in a few update scripts to
update the Tokens to fit the changes made in D7.

```php
variable_set('page_title_default', '[current-page:title] | [site:name]');
variable_set('page_title_front', '[site:name] | [site:slogan]');
variable_set('page_title_pager_pattern', '[current-page:title] (page [current-page:page-number]) | [site:name]');
```


Some of the Patterns for pathauto also need to change:

## Step 2: Migrate CCK Fields

As we all know,  many concepts that were wrapped up in Content Construction Kit
(including 'fields') have been added to Drupal 7 core. However, only a few of
the fields from CCK in Drupal 6 will migrate out of the box.  In order to
migrate to Drupal 7, some fields require specific migration scripts to update
the data to the new format for Drupal 7.  First, you need to download and
enable the content_migrate module (which comes packaged inside the CCK project
for Drupal 7). Most general CCK fields like text fields and lists are
upgradable without any add-on modules.  However, some may require you to
obtain and enable extra modules to complete the migration.  Visit the Content
Migration administration page: /admin/structure/content_migrate  to see which
fields are available and unavailable for upgrade, and download the necessary
add-on modules.

In our case I had to download and enable the link module,  and enabling the new
core 'image' module.

```bash
$ cd path/to/d7
$ drush en content_migrate
$ drush dl link
$ drush en link
$ drush en image
```
Upon clicking through the migration I recieved the following error:

```
  Field migration has encountered an error.
  Please continue to  the error page

  An AJAX HTTP error occurred. HTTP Result Code: 200 Debugging information
  follows. Path: /batch?id=31&op=do StatusText: OK ResponseText:
  Fatal error: Unsupported operand types in
  ~/Sites/BluesparkLabs/d7/modules/field/field.crud.inc on line 601

  The field that was not upgraded was:

  field_portfolio_short_desc text_long Portfolio
```

On the second try,  the remaining field did migrate successfully.

Some notable things that were migrated:

* field order (aka weight)
* some field display settings.
* content type comment settings.


Some notable things that were not migrated:

*   "Basic" field label display settings were confusingly not migrated to
    the 'Default' display for Drupal 7, however, the Teaser label display
    settings were.

After playing around a while between the D7 and D6 site, I had figured out the
display settings and replicated them as best I could in Drupal 7.

## Step 3: Tweak Imagecache  (Image Styles)

Image styles were not migrated from the Drupa 6 imagecache module.  But this
could be because we had exported the imagecache presets to code in the
bsp_tools module before hand.  Honestly this is ok, because we'd need to
probably modify the sizes anyway for the new theme. And potentially we could
get rid of some of the presets.

User profile images were not migrated to a field (from core profile module
image support).

Upon enabling the profile module, I got the following PHP warning from drush.

```
Warning: Invalid argument supplied for foreach() in                   [warning]
profile_token_info() (line 768 of
~/Sites/d7/sites/all/modules/contrib/token/token.tokens.inc).
```

## On to theming....

I decided to try again with the fusion theme as the base theme from which to
build the Drupal 7 custom theme. The fusion theme doesnt have an official
release, and this is supposedly only because of the missing skinr module
functionality.

```bash
$ drush dl fusion
```

After consideration, I ended up starting from a custom Bartik subtheme, since
it was stable, part of core, and will be easy to override and customize.
