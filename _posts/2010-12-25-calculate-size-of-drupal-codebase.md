---
layout: post
title: Calculating the size of the Drupal Codebase.
---


Reference:
http://journal.uggedal.com/django-vs-rails-code-size


```
# drush dl drupal
Project drupal (6.20) downloaded to                                  [success]
/Users/jameswilson/Sites/Drupal6/drupal-6.20.
Project drupal contains:                                             [success]
 - 1 profile: default
 - 6 themes: pushbutton, minnelli, garland, marvin, chameleon,
bluemarine
 - 33 modules: user, upload, update, trigger, translation, tracker,
throttle, taxonomy, system, syslog, statistics, search, profile,
poll, ping, php, path, openid, node, menu, locale, help, forum,
filter, dblog, contact, comment, color, book, blogapi, blog, block,
aggregator


# cloc --force-lang=PHP,install --force-lang=PHP,module --force-lang=PHP,inc \
--force-lang=PHP,test --force-lang=PHP,profile --force-lang=Make,info -3 \
drupal-6.20/
     345 text files.
     345 unique files.
      15 files ignored.

http://cloc.sourceforge.net v 1.53  T=1.0 s (330.0 files/s, 87353.0 lines/s)
-------------------------------------------------------------------------------
Language          files     blank   comment      code    scale   3rd gen. equiv
-------------------------------------------------------------------------------
PHP                 204      6819     22792     48091 x   3.50 =      168318.50
CSS                  59       457       409      4305 x   1.00 =        4305.00
Javascript           23       356       936      2347 x   1.48 =        3473.56
make                 39        78         0       406 x   2.50 =        1015.00
Bourne Shell          4        25         3       134 x   3.81 =         510.54
Perl                  1        26        42       127 x   4.00 =         508.00
-------------------------------------------------------------------------------
SUM:                330      7761     24182     55410 x   3.21 =      178130.60
-------------------------------------------------------------------------------



# drush dl drupal-7.0
Project drupal (7.0) downloaded to                                   [success]
/Users/jameswilson/Sites/Drupal7/drupal-7.0.
Project drupal contains:                                             [success]
 - 3 profiles: testing, standard, minimal
 - 4 themes: stark, seven, garland, bartik
 - 47 modules: drupal_system_listing_incompatible_test,
drupal_system_listing_compatible_test, user, update, trigger,
translation, tracker, toolbar, taxonomy, system, syslog, statistics,
simpletest, shortcut, search, rdf, profile, poll, php, path, overlay,
openid, node, menu, locale, image, help, forum, filter, file,
field_ui, text, options, number, list, field_sql_storage, field,
dblog, dashboard, contextual, contact, comment, color, book, blog,
block, aggregator


# cloc --force-lang=PHP,install --force-lang=PHP,module --force-lang=PHP,inc \
--force-lang=PHP,test --force-lang=PHP,profile --force-lang=Make,info -3 \
drupal-7.0/
     852 text files.
     847 unique files.
      33 files ignored.

http://cloc.sourceforge.net v 1.53  T=9.0 s (90.8 files/s, 31723.2 lines/s)
-------------------------------------------------------------------------------
Language          files     blank   comment      code    scale   3rd gen. equiv
-------------------------------------------------------------------------------
PHP                 484     21962     79315    161322 x   3.50 =      564627.00
CSS                 116       810      1098      8909 x   1.00 =        8909.00
Javascript           84       815      2808      5085 x   1.48 =        7525.80
make                108       226         0      1363 x   2.50 =        3407.50
Bourne Shell          8       172         3      1060 x   3.81 =        4038.60
XML                  12         3         0       441 x   1.90 =         837.90
HTML                  3         4         0        69 x   1.90 =         131.10
ASP.Net               1         3         0        40 x   1.29 =          51.60
SQL                   1         0         0         1 x   2.29 =           2.29
-------------------------------------------------------------------------------
SUM:                817     23995     83224    178290 x   3.31 =      589530.79
-------------------------------------------------------------------------------
```
