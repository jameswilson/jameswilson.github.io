---
layout: post
title: Install git on Verve hosting.
---

1.  Login via ssh access to the verve hosting server:

       $ ssh user@host.verve.com

2.  Ensure gcc is available

        $ which gcc
        /usr/bin/gcc


3.  Download and install git, from source:

        mkdir src
        cd src
        wget --no-check-certificate https://git-core.googlecode.com/files/git-1.7.8.3.tar.gz
        tar xvf git-1.7.8.3.tar.gz

