---
categories:
    - Web development
tags:
    - devops
layout: post
title: Migrating to git on Dreamhost with svn2git
---

Step-by-step instructions on how to use svn2git to migrate repositories on Dreamhost.

<!--more-->

1.  Figure out the users in the repo:

        $ cd path/to/svn/repo
        $ svn log | grep -E "r[0-9]+ \| .+ \|" | awk '{print $3}' | sort | uniq

2.  Create a mapping file called `authors.txt`, and add each author to the
    file in the following format:

        james = James Wilson <jrwilson3@gmail.com>

3.  Run svn2git on the subversion repo.

        $ svn2git http://svn.mydomain.com/repository --authors authors.txt

4.  Create a repo with gitolite (see my post on setting up gitolite on Dreamhost).

5.  Add a new remote.

        $ git remote add origin gituser@mydomain.com:repositiory

6.  Push all the changes.

        $ git push --all origin
