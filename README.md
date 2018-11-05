---
title: README
---

Repository | Version | Build Status
---------- | ------- | ------------
{{site.repository}} | {{site.version}} | [![Build Status](https://travis-ci.org/jameswilson/jameswilson.github.io.svg?branch=master)](https://travis-ci.org/jameswilson/jameswilson.github.io)

## Installation

### 1. Fork the repository on GitHub

In the GitHub UI, fork this repsotory to your own account and rename it to `yourusername.github.io`

Then clone the repository locally.

```bash
$ git clone git@github.com:yourusername/yourusername.github.io.git mysite
```


### 2. Install dependencies

Jekyll depends on Ruby.  Use RVM to lock in the Ruby version and Bundler to install Jekyll and lock in the Ruby Gems that Jekyll depends on.

```bash
$ cd mysite
$ rvm install 2.3
$ rvm use 2.3
$ gem install jekyll bundler
$ bundle install
```


### 3. Perform a health check

Ensure that the github-pages ruby gem is installed and reporting no errors.

```bash
$ github-pages health-check
```


### 4. Test your site locally

Execute Jekyll using bundler:

```bash
$ bundle exec jekyll serve
```

Then open <http://127.0.0.1:4000> in your browser, and test your site.


### 5. Configure Jekyll

1. If hosting at a custom domain create a file in the repository root called `CNAME` and point it to your [custom domain name](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages). Otherwise, if you're not using a custom domain name, **modify the `baseurl` in `_config.yml`** to point to your GitHub Pages URL. Example: for a repo at `github.com/username/repo`, use `http://username.github.io/repo/`. **Be sure to include the trailing slash.**

3. Open `_config.yml` and modify the Jekyll configurations to match your repository.  You'll want to modify the repository, title, tagline, description, author, and url.  Optionally, create a Disqus account and configure / enable it in `_config.yml`. Change other settings at your own risk.

4. Review and enable/disable any of the [optional Jekyll plugins supported by GitHub](https://help.github.com/articles/configuring-jekyll-plugins/#optional-plugins) in your `_config.yml`.

5. See [Customizing GitHub Pages](https://help.github.com/categories/customizing-github-pages/) for further details.


### 6. Configure Travis CI

* Setup a [Travis CI](https://travis-ci.org/profile) account using Github credentials.
* Sync your repositories from Github.
* Enable Travis for the current repository.
* You can manuall trigger a build in Travis CI to ensure everything builds correctly.
* Update the Build Status icon in this README to match your repository.


## Maintenance


## 1. Ensuring previous year is displayed

This site design has custom logic to hide the year from archived posts
if the post was made in the current year. This means that Jekyll must be
regenerated at least once per year on January 1st for the previous year
to be visible on the "Related Posts" block and on the /archive page.


### 2. Staying up-to-date with github-pages

You may update the GitHub Pages gem on your local environment to stay in sync with the latest.

```bash
$ bundler update github-pages
$ github-pages health-check
```

Be sure to review, commit, and push the changes to `Gemfile.lock` if required.



## License

* The website's software—including the CSS, Javascript, and HTML/Liquid templates—is released under the open source [MIT license](/LICENSE#software-license).
* The website's content, including static page content and post content is licensed under [Creative Commons Attribution-ShareAlike (CC BY-SA)](/LICENSE#content-license).
