# The personal blog of James Wilson

[![Build Status](https://travis-ci.org/jameswilson/jameswilson.github.io.svg?branch=master)](https://travis-ci.org/jameswilson/jameswilson.github.io)

## 1. Install Ruby, Jekyll, and dependencies.

```bash
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

Optionally, resolve the *No GitHub API authentication* warning message with workaround described [here](https://idratherbewriting.com/documentation-theme-jekyll/mydoc_install_jekyll_on_mac.html#githuberror).

## 4. Open <http://127.0.0.1:4000> in your browser, and test your site.

## 5. Configure the domain.

1. Modify the `CNAME` file to point to your [custom domain name](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages),

2. If you're not using a custom domain name, **modify the `baseurl` in `_config.yml`** to point to your GitHub Pages URL. Example: for a repo at `github.com/username/repo`, use `http://username.github.io/repo/`. **Be sure to include the trailing slash.**

3. See [Customizing GitHub Pages](https://help.github.com/categories/customizing-github-pages/) for further details.

## 6. Configure Travis CI

* Setup a [Travis CI](https://travis-ci.org/profile) account using Github credentials.
* Sync your repositories from Github.
* Enable Travis for the current repository.
* You can manuall trigger a build in Travis CI to ensure everything builds correctly.
* Update the Build Status icon in this README to match your repository.

## 7. Enable optional plugins

Review and enable any of the [available optional plugins](https://help.github.com/articles/configuring-jekyll-plugins/#optional-plugins) in your `_config.yml`.


## License

Open sourced under the [MIT license](LICENSE.md).
