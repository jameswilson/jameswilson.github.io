# The personal blog of James Wilson

[![Build Status](https://travis-ci.org/jameswilson/jameswilson.github.io.svg?branch=master)](https://travis-ci.org/jameswilson/jameswilson.github.io)


## 0. Fork it

In the GitHub ui, fork this repsotory and rename it to `yourusername.github.io`

Then clone the repository locally.

```bash
$ git clone git@github.com:yourusername/yourusername.github.io.git mysite
```


## 1. Install Ruby, Jekyll, and dependencies.

```bash
$ cd mysite
$ rvm install 2.3
$ rvm use 2.3
$ gem install jekyll bundler
$ bundle install
```

## 2. Confirm Github Pages gem is installed and reports no errors.

```bash
$ github-pages health-check
```


## 3. Confirm Jekyll is installed and runs locally.

```bash
$ bundle exec jekyll serve
```


## 4. Open <http://127.0.0.1:4000> in your browser, and test your site.


## 5. Configure Jekyll.

1. If hosting at a custom domain create a file in the repository root called `CNAME` and point it to your [custom domain name](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages). Otherwise, if you're not using a custom domain name, **modify the `baseurl` in `_config.yml`** to point to your GitHub Pages URL. Example: for a repo at `github.com/username/repo`, use `http://username.github.io/repo/`. **Be sure to include the trailing slash.**

3. Open `_config.yml` and modify the Jekyll configurations to match your repository.  You'll want to modify the repository, title, tagline, description, and url.  Optionally, create a Disqus account and configure / enable it in `_config.yml`. Change other settings at your own risk.

4. Enable optional plugins

Review and enable any of the [available optional plugins](https://help.github.com/articles/configuring-jekyll-plugins/#optional-plugins) in your `_config.yml`.

5. See [Customizing GitHub Pages](https://help.github.com/categories/customizing-github-pages/) for further details.


## 6. Configure Travis CI

* Setup a [Travis CI](https://travis-ci.org/profile) account using Github credentials.
* Sync your repositories from Github.
* Enable Travis for the current repository.
* You can manuall trigger a build in Travis CI to ensure everything builds correctly.
* Update the Build Status icon in this README to match your repository.


## 7. Staying up-to-date with github-pages

You may update the GitHub Pages gem on your local environment to stay in sync with the latest.

```bash
$ bundler update github-pages
```

Be sure to review, commit, and push the changes to `Gemfile.lock` if required.

## License

Open sourced under the [MIT license](LICENSE.md).
