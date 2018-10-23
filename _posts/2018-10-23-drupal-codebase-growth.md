---
layout: post
title: Codebase growth between Drupal 6, 7 and 8
---

In 2010 I made a post to [Calculate the size of the Drupal codebase][1] by comparing lines of PHP, JavaScript, and CSS code between Drupal 6 and 7.  This is a follow-up that adds Drupal 8 to the comparison matrix.

<!--more-->

## td;lr

The main takeaway is that the code grew almost exponentially between Drupal 6
and Drupal 8. Drupal 8 has introduced a wide array of new file types that
Drupal 6 and 7 did not have, including Twig templates. Please note that I did
not include Twig in the table below. Sadly, a pure 1-to-1 mapping from PHP
Template files to Twig cannot be done because the PHP row includes `tpl.php`
in Drupal 6 and 7. (Suggestions welcome as to how to break these apart.)


## Codebase growth matrix

The following table outlines the codebase growth between the three versions of Drupal.

Criteria                | Drupal 6.20    | Drupal 7.0     |  Drupal 8.0.0
----------------------- | -------------- | -------------- | ----------------
PHP files               |  204           |  484           |  8,413
Javascript files        |  23            |  84            |  483
CSS files               |  59            |  116           |  268
YAML files              |  -             |  -             |  1,564
Markdown files          |  -             |  -             |  138
Ignored files           |  15            |  33            |  662
**Total files**         |  **345**       |  **852**       |  **12,141**
PHP comments            |  22,792        |  79,315        |  422,131
JS comments             |  936           |  2,808         |  15,760
CSS comments            |  409           |  1,098         |  2,151
**Total comments**      |  **24,182**    |  **83,224**    |  **449,797**
PHP lines of code       |  48,091        |  161,322       |  629,420
JS lines of code        |  2,347         |  5,085         |  25,646
CSS lines of code       |  4,305         |  8,909         |  14,911
**Total lines of code** |  **55,410**    |  **178,290**   |  **769,248**
----------------------- | -------------- | -------------- | ----------------
**3rd Gen Equivalent**  | **178,130.60** | **589,530.79** | **2,381,531.67**

Note: The cloc documentation page says that the 3rd gen. equiv. value should be "taken with a large grain of salt."


## How I came about these numbers


Thanks to [this post comparing Django to Rails][3] for inspiration back in 2010, the basic procedure is to download and install [cloc][2] a command line tool that calculate lines of code, comments, etc.

### 1. Install `cloc`

If you're on a mac, you can use Homebrew to install cloc.

```bash
$ brew install cloc
$ cloc --version
1.80
```

### 2. Download Drupal 6.20, 7.0, 8.0.0

Use drush version 8 or lower to download drupal 6, 7 and 8.  For Drupal 6 and 7 I'm using the same versions that I used back in [the 2010 post][1].

```bash
$ drush dl drupal-6.20
$ drush dl drupal-7.0
$ drush dl drupal-8.0.0
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


### 4. Calculate lines of code of Drupal 8

For the Drupal 8 calculation, I used generally the same cloc configuration that was used form Drupal 7, deciding against spending more time to figure out which of the 662 files were ignored and why.

```bash
$ cloc --force-lang=PHP,install --force-lang=PHP,module --force-lang=PHP,inc --force-lang=PHP,test --force-lang=PHP,profile --force-lang=Make,info -3 drupal-8.0.0/
```

```
   12141 text files.
   11897 unique files.
     662 files ignored.

1 error:
Line count, exceeded timeout:  drupal-8.0.0/core/modules/migrate_drupal/tests/fixtures/drupal6.php

github.com/AlDanial/cloc v 1.80  T=47.56 s (242.0 files/s, 28795.7 lines/s)
-------------------------------------------------------------------------------
Language          files     blank   comment      code    scale   3rd gen. equiv
-------------------------------------------------------------------------------
PHP                8413    137594    422131    629420 x   3.50 =     2202970.00
YAML               1564      2149      1499     62912 x   0.90 =       56620.80
JavaScript          483      5189     15760     25646 x   1.48 =       37956.08
CSS                 268       761      2151     14911 x   1.00 =       14911.00
Markdown            138      3722         0     11493 x   1.00 =       11493.00
JSON                113        27         0      9447 x   2.50 =       23617.50
Twig                444       312      8192      6429 x   2.00 =       12858.00
XSD                   7       110        28      3129 x   1.90 =        5945.10
XML                  36        19         9      2415 x   1.90 =        4588.50
Bourne Shell         14       290         0      2289 x   3.81 =        8721.09
Ant                  12       102         0       663 x   1.90 =        1259.70
C                     1        52         8       223 x   0.77 =         171.71
HTML                  7         4         0        86 x   1.90 =         163.40
PO File               4        27         0        85 x   1.50 =         127.50
m4                    1        11        11        41 x   1.00 =          41.00
C/C++ Header          1        12         8        40 x   1.00 =          40.00
make                  2         8         0        18 x   2.50 =          45.00
SQL                   1         0         0         1 x   2.29 =           2.29
-------------------------------------------------------------------------------
SUM:              11509    150389    449797    769248 x   3.10 =     2381531.67
-------------------------------------------------------------------------------
```


[1]: /2010-12-25-calculate-size-of-drupal-codebase
[2]: https://github.com/AlDanial/cloc
[3]: http://journal.uggedal.com/django-vs-rails-code-size
