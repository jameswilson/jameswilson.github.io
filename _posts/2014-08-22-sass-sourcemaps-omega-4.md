---
layout: post
title: How to add Source Maps to Omega 4.x projects
---

SASS 3.3 introduced support for Sourcemaps and just recently, Chris Eppstein
has created an initial Release Candidate as a lead up to a full 1.0.0 release
version of Compass — which now also supports Sourcemaps.

However, the Omega 4.x theme for Drupal 7 is running on older “stable” versions
of Sass, Compass, and their respective dependencies — none of which support
source maps.

<!--more-->

<p class="pullquote">
UPDATE: fubhy (the Omega theme maintainer) has committed code to the Omega
7.x-4.x branch that adds Source Maps functionality.  Just grab the latest dev
release, create a sub theme from the starter kit and test! Leave your feedback
on [Issue #2311593](https://www.drupal.org/node/2311593).
</p>

While source maps are not “bleeding edge” like they were about a year ago, they
are relatively new technology only really being supported in the latest
versions of a few browsers like Chrome and Firefox. I consider sourcemaps to
be an important tool for distributed larger projects with  many components and
partials, particularly for teams with multiple front-end developers.

The steps below are the ones I took to get Omega updated to work with
sourcemaps. I’ve provide a patch to the [Omega issue #2311593](https://www.drupal.org/node/2311593#comment-9020173).

The assumption here is that you’re already following Omega’s best practices and
using bundler and RVM to manage your ruby-version, and the gem set that the
Omega sub theme depends on. The way to confirm this is to just run `bundle
install` from inside your theme folder and follow that up with a
`bundle show sass`, which should give you a path that looks something
like `~/.rvm/gems/ruby-[version]@omega.themename/gems/`.

If you’re not using RVM, that’s o.k., but I highly recommend you start using it
to control which ruby version you’re using in any given project.



## 1. Update to SASS 3.3 and Compass 1.0.0.rc.0

Go to your theme folder and change the sass gem to `~>3.3`  and compass gem to
`~>1.0.0.rc.0` in the Gemfile file. The _spermy_ operator `~>` effectively
means *the last digit on the right may be equal to or greater than the value
specified* and is sometimes pronounced as “approximately greater than”.

In your theme's Gemfile, replace: `gem 'sass'` with: `gem 'sass', '~>3.3'`,
and then replace `gem 'compass'` with: `gem 'compass', ‘~>1.0.0.rc.0'`.



## 2. Use bundler to update the SASS and Compass gems.

```bash
bundle update
```

This has the effect of downloading new Ruby gems and updating the Gemfile.lock
file. New versions of the SASS and Compass gems will be installed into the
theme’s gemset — typically found inside
`~/.rvm/gems/ruby-[version]@omega.themename/gems/` folder (if you’re using RVM).



## 3 Remove add_import_path from config.rb.

The line `add_import_path 'sass'` in the config.rb file was causing problems
after upgrading compass because it was generating css files twice -- so I had
to remove this line.

(via https://github.com/Compass/compass/issues/1737 and https://www.drupal.org/node/2177397)



## 4. Compile your CSS.

```bash
bundle exec compass compile
```

You’ll probably run into a handful of errors trying to compile the CSS due to
other outdated and deprecated functions.  In my case I got a series of compile
errors that I was able to remedy one-by-one, by searching for the error message
in Google and following the instructions to remedy accordingly.

**Error 1:**

```
WARNING: The compass/css3/shared module has been deprecated.

You can silence this warning by importing compass/css3/deprecated-support instead.

on line 1 of compass-core-1.0.0.rc.0/stylesheets/compass/css3/_shared.scss
from line 1 of singularitygs-1.1.2/stylesheets/singularitygs/helpers/_box-sizing.scss
from line 8 of singularitygs-1.1.2/stylesheets/singularitygs/_helpers.scss
from line 36 of singularitygs-1.1.2/stylesheets/_singularitygs.scss
from line 4 of sites/all/themes/themename/sass/themename.styles.scss
from line 5 of sites/all/themes/themename/sass/themename.no-query.scss
```

This happens because singularity.gs version 1.0.0 that comes with Omega is
incompatible with Sass 3.3.



## 5. Update to Singularity.gs 1.2.1

In the Gemfile, update singulartygs gem to `~>1.2.1` and also add `require
'singularitygs'`to the config.rb file. Then run `bundle update`, and  `bundle
exec compass compile`.  This results in another error.

**Error 2:**

```
Line 3 of sass/themename.styles.scss: File to import not found or unreadable: breakpoint.
```



## 6. Update to breakpoint 2.4.0

In the Gemfile, update breakpoint gem to `~>2.4.0` and also add `require
'breakpoint'`  to config.rb ([more info](https://www.drupal.org/node/2232431)).



## 7. Update to Sass Globbing 1.1.0

In the Gemfile, update Sass Globbing gem to `~>1.1.0` in Gemfile. Re-run
`bundle update` and `bundle exec compass compile` ([more info](http://stackoverflow.com/questions/22213053)).

This results in yet another error:

**Error 3:**

```
Line 8 of sass/themename.normalize.scss: File to import not found or unreadable: toolkit/border-box.
```



## 8. Update to Toolkit 2.5.2 and fix import statements in SCSS files

This requires three changes ([more info](https://www.drupal.org/node/2259101)):

1.  In Gemfile update the toolkit gem to `~> 2.5.2`.
2.  In sass/themename.styles.scss change from `@import "toolkit-no-css"`
    to `@import "toolkit"`.
3.  In sass/themename.normalize.scss change from `@import "toolkit/border-box"`
    to `@import "toolkit/kickstart"`.



## 9. Update to Susy 2.1.2

Update the susy gem to `~>2.1.2` in the Gemfile.

I just did this because there was another error related to susy, and wanted to
be sure we were on the latest version. Unfortunately, I don’t remember the error
message now.



## 10. Run and re-run `bundle exec compass compile` until there are no more errors.

Following the methodology in the previous steps above to troubleshoot and
upgrade libraries as necessary, as you hit errors.



## 11. Enable Compass Sourcemap configuration in config.rb.

Once there are no more errors, you can finally enable the source map
configuration. On the line for `sass_options` in config.rb, add `:sourcemap =>
true`  inside the curly braces.

My setup looks like this:

```ruby
sass_options = {
  :debug_info => false,
  :line_comments => false,
  :sourcemap => true
}
```

I have `output_style = :expanded` and `debug_info` hardcoded to false for two
reasons:

We don’t use the `:development` or `:production` configurations provided by
ruby and available to Compass to distinguish between how compressed the css
output is. Drupal has built in functionality to aggregate and minify all the
CSS, which we turn on only on testing and production environments.

We commit the compiled CSS to our repository, because we don’t run compass or
bundler on our production servers. Thus it is far better to store compiled css
in an expanded format so that diffs and commit history from other front-end
developers can easily be read by a human.



## 12. Generate source maps!

Run `bundle exec compass compile` once more to compile the css again and
generate the source maps.

You will end up with new files in your theme’s css/ directory that look like
`css/themename.style.css.map` etc.



## 13. Commit the changes.

Commit all the changes in your theme, including in the Gemfile, the
Gemfile.lock, the config.rb,  the changes to your SASS files, and the newly
generated your new CSS map files into your version control repository.

```bash
git commit .  -m "Added sourcemaps!”
```
