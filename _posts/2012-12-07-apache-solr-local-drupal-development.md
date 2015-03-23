---
layout: post
title: Installing Apache Solr for local multi-project Drupal development on a Mac
---

Solr is an open source enterprise search platform from the Apache Lucene project.

Its major features include powerful full-text search, hit highlighting, faceted
search, dynamic clustering, database integration, and rich document (e.g., Word,
PDF) handling. Providing distributed search and index replication, Solr is
highly scalable.


## Pre-requisites

Install homebrew - read Homebrew installation instructions first.


## Step 1: Get non-default version of solr

Tap into homebrew versions, to get an earlier version of Solr 3.6.1

Homebrew currently comes with solr 4.0 configured. The Drupal apachesolr module
has only unstable bleeding edge integration, plus, we want to simulate the
version in our production environment, so we need to setup Homebrew to "tap"
into their versions functionality:

    $ brew tap homebrew/versions

This functionality lets us list all the historic versions of any "Formula" (e.g.
solr). We can find the available versions of Solr, and select the one we need by
executing the git command provided.

    $ brew versions solr
    3.6.1    git checkout baee5b9 /usr/local/Library/Formula/solr.rb
    3.6.0    git checkout 50ad7ca /usr/local/Library/Formula/solr.rb
    3.5.0    git checkout 6259d05 /usr/local/Library/Formula/solr.rb
    3.4.0    git checkout da53d68 /usr/local/Library/Formula/solr.rb
    3.3.0    git checkout 14e4db3 /usr/local/Library/Formula/solr.rb
    3.1.0    git checkout 1fb85ef /usr/local/Library/Formula/solr.rb
    1.4.1    git checkout 0476235 /usr/local/Library/Formula/solr.rb
    1.4.0    git checkout eb32026 /usr/local/Library/Formula/solr.rb
    1.3.0    git checkout 8db9aaa /usr/local/Library/Formula/solr.rb

The official installation and help documentation for Drupal apachesolr module
recommends 3.5.0  however I continually got 404 errors:

    ==> Downloading http://www.apache.org/dyn/closer.cgi?path=lucene/solr/3.5.0/apache-solr-3.5.0.tgz
    ==> Best Mirror http://apache.mirrors.lucidnetworks.net/lucene/solr/3.5.0/apache-solr-3.5.0.tgz

    curl: (22) The requested URL returned error: 404

So I instead decided to use 3.6.1:

    $ git checkout baee5b9 /usr/local/Library/Formula/solr.rb
    $ brew install solr

This will install Solr to /usr/local/Cellar/solr/ containing one subdirectory of the Solr [version], in my case 3.6.1.


## Step 2: Download the apachesolr drupal module.

The Solr configuration files are stored at
`/usr/local/Cellar/solr/[version]/libexec/example` as I wanted to set up a
multicore instance I did the following:

    $ cp -R $(brew --prefix solr)/libexec/example $(brew --prefix solr)/libexec/drupal
    $ vim /usr/local/Cellar/solr/[version]/libexec/drupal/multicore/solr.xml

Define a bucket (core) for each project in solr.xml:

```xml
<cores adminPath="/admin/cores">
    <core name="someproject.local" instanceDir="someproject.local" />
    <core name="anotherproject.local" instanceDir="anotherproject.local" />
</cores>
```

Copy the required files from the Drupal apachesolr module into the core
directories, assume that the apachesolr module is stored at the following path
`~/Sites/drupalsite/sites/all/modules/contrib/apachesolr/` and that our terminal
instance is still in the multicore directory:

    $ cd someproject.local
    $ cp ~/Sites/someproject.local/sites/all/modules/contrib/apachesolr/solr-conf/solr-3.x/*.xml ./
    $ cd ../anotherproject.local
    $ cp ~/Sites/anotherproject.local/sites/all/modules/contrib/apachesolr/solr-conf/solr-3.x/*.xml ./


## Step 3: Start Solr in multicore mode.

    $ java -Dsolr.solr.home=multicore -jar $(brew --prefix solr)/libexec/drupal/start.jar

Access the Solr administration interface at http://localhost:8983/solr/

Assuming you don’t get any Exceptions…


## Step 4: Configure Drupal site with solr settings

    Solr host name: 127.0.0.1
    Solr port: 8983
    Solr path: /solr/[core name value]  (eg. /solr/someproject.local)
    Note: multiple cores on a single Drupal site is possible via Domain Access module.


## Step 5: Run solr in a thread with launchd

    $ vim ~/Library/LaunchAgents/com.apache.solr.plist

Paste the following, replacing [your-username] with your actual username:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC
"-//Apple Computer//DTD PLIST 1.0//EN" "
http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>org.apache.solr</string>
    <key>ProgramArguments</key>
    <array>
            <string>/usr/bin/java</string>
            <string>-Djetty.home=$(brew --prefix solr)/libexec/drupal</string>
            <string>-Djetty.logs=/var/logs/solr</string>
            <string>-Dsolr.solr.home=$(brew --prefix solr)/libexec/drupal/multicore</string>
            <string>-jar</string>
            <string>$(brew --prefix solr)/libexec/drupal/start.jar</string>
    </array>
    <key>ServiceDescription</key>
    <string>Solr</string>
    <key>WorkingDirectory</key>
    <string>/opt/local/share/solr</string>
    <key>UserName</key>
    <string>[your-username]</string>
    <key>GroupName</key>
    <string>staff</string>
    <key>RunAtLoad</key>
    <true/>
</dict>
</plist>
```

Now you can launch or quit Solr:

    $ launchctl load -w ~/Library/LaunchAgents/com.apache.solr.plist
    $ launchctl unload -w ~/Library/LaunchAgents/com.apache.solr.plist

## References:

http://ramlev.dk/blog/2012/06/02/install-apache-solr-on-your-mac/

Solr - https://lucene.apache.org/solr/ - http://en.wikipedia.org/wiki/Apache_Solr

Homebrew - http://brew.sh/ - https://en.wikipedia.org/wiki/Homebrew_(package_management_software)

These steps are a condensed version of an article from RealityLoop.com
