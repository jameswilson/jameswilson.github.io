---
layout: post
title: Calculating the size of the Drupal Codebase.
---

This post demonstrates how to calculate the lines of PHP, JavaScript, and CSS code between Drupal 6 and 7, leveraging [cloc]() a “command line tool that counts blank lines, comment lines, and physical lines of source code in many programming languages.”

<!--more-->

## td;lr

The codebase has generally trippled in size between Drupal 6 and Drupal 7. CSS
and PHP code has doubled.  Javascript code has quadrupled — a nod to the clear
importance of Javascript and the growing Jquery library and JS dependencies
included in Drupal core.  The vast majority of the size increase comes from
code comments.

Criteria                | Drupal 6.20    | Drupal 7.0
----------------------- | -------------- | --------------
PHP files               |  204           |  484
Javascript files        |  23            |  84
CSS files               |  59            |  116
Ignored files           |  15            |  33
**Total files**         |  **345**       |  **852**
PHP comments            |  22,792        |  79,315
JS comments             |  936           |  2,808
CSS comments            |  409           |  1,098
**Total comments**      |  **24,182**    |  **83,224**
PHP lines of code       |  48,091        |  161,322
JS lines of code        |  2,347         |  5,085
CSS lines of code       |  4,305         |  8,909
**Total lines of code** |  **55,410**    |  **178,290**
----------------------- | -------------- | --------------
**3rd Gen Equivalent**  | **178,130.60** | **589,530.79**

Note: The cloc documentation page says that the *3rd gen. equiv.* value should be "taken with a large grain of salt."


## Background and procedure

Thanks to [this post comparing Django to Rails](http://journal.uggedal.com/django-vs-rails-code-size) for inspiration, the basic procedure is to download and install `cloc` a command line tool that calculate lines of code, comments, etc.

### 1. Install `cloc` command line tool.

You can use homebrew or download the source (perl script) from [Sourceforge](http://cloc.sourceforge.net/).

### 2. Download Drupal 6.20 and 7.0

```bash
$ drush dl drupal-6.20
$ drush dl drupal-7.0
```

### 3. Calculate lines of code of Drupal 6

```bash
$ cloc --force-lang=PHP,install --force-lang=PHP,module --force-lang=PHP,inc --force-lang=PHP,test --force-lang=PHP,profile --force-lang=Make,info -3 drupal-6.20/
```
```
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
```


### 4. Calculate lines of code of Drupal 7

```bash
$ cloc --force-lang=PHP,install --force-lang=PHP,module --force-lang=PHP,inc --force-lang=PHP,test --force-lang=PHP,profile --force-lang=Make,info -3 drupal-7.0/
```
```
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
