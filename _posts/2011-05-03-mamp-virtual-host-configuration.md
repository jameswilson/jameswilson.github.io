---
layout: post
title: Mamp virtual host configuration
---

My MAMP Pro demo expired, so I decided it was time to setup the basic MAMP
installation just like I had my old Apache that came with the Mac configured.

<!--more-->

The setup required a couple of changes to my custom user.conf file but here is the result:

```bash
$ cat /Applications/MAMP/conf/apache/jameswilson.conf
```

```apache
DocumentRoot /Users/jameswilson/Sites
<Directory "/Users/jameswilson/Sites/">
    Options Indexes MultiViews FollowSymLinks
    AllowOverride All
    Order allow,deny
    Allow from all
</Directory>

NameVirtualHost 127.0.0.1:80
NameVirtualHost 127.0.0.1:443

<VirtualHost 127.0.0.1:80>
    VirtualDocumentRoot /Users/jameswilson/Sites/%-2+/public
</VirtualHost>

# VirtualDirectoryRoot with SSL instructions:
#   http://bit.ly/dEl8qC
<IfModule mod_ssl.c>
<VirtualHost *:443>
    VirtualDocumentRoot /Users/jameswilson/Sites/%-2+/public
    ErrorLog /Applications/MAMP/log/apache_error_log
    CustomLog /Applications/MAMP/log/apache_access_log combined
    SSLEngine on
    SSLCertificateFile "/Applications/MAMP/conf/apache/ssl_crt/server.crt"
    SSLCertificateKeyFile "/Applications/MAMP/conf/apache/ssl_key/server.key"
</VirtualHost>
</IfModule>
```

I had previous configured the server.crt and server.key settings using another
tutorial.  And the above config file came out of a lot of sweat and tears
configuring Mac OS X's standard apache, for my desired custom config.

Now I am able to put projects in my Sites folder, and inside each project is a
public/ folder where the webroot is located.

Example 1:  Install drupal to:

    ~/Sites/Drupal6/public/

Then access it via:

    http://drupal6.local/

HTTPS is currently not working but I dont have time to futz around with it to
fix it today.
