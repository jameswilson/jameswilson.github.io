---
categories:
    - Web development
tags:
    - devops
layout: post
title: Install Gitolite on Dreamhost
---

How-to guide to installing Gitolite on Dreamhost.

<!--more-->

## Part 1: Installation

1.  In the Dreamhost control panel, create new user `mygitoliteuser` and ensure
    that *shell access* is enabled.  Write the password down, or copy it to
    your clipboard, and wait for the user to be installed by the Dreamhost
    robot.


2.  While you're waiting for the user to be installed by the Dreamhost robot,
    double check that you have your own SSH keys setup on your local machine.

    After the user is created on the server, copy your public key to the new
    user you just created in your Dreamhost account, with the command below.
    Naming the file `yourdesiredgitusername.pub` on the server. Gitolite uses
    these public key files as the basis for its access control lists, explained
    further down.

    Execute the following command:

        $ scp ~/.ssh/id_rsa.pub mygitoliteuser@xxxxx.dreamhost.com:~/yourdesiredgitusername.pub

    Do not put your SSH public  key in the `~/.ssh/config/authorized_keys`
    file on the server, because it will cause problems during Gitolite
    installation.


3.  Log into the remote machine via SSH with the following command, provide the
    password you created in step 1 above when prompted.

        $ ssh mygitoliteuser@xxxxx.dreamhost.com


4.  Ensure git is installed on your machine.

        $ which git
        $ git --version

    If git is not installed follow another tutorial on installing git.


5.  Download gitosis and install it.

        $ git clone git://github.com/sitaramc/gitolite
        $ gitolite/src/gl-system-install
        $ gl-setup ~/YourName.pub

    If you hit any problems installing check the [documentation][docs].


6.  On your local machine, download the gitolite-admin repository.

        $ git clone mygitoliteuser@xxxxx.dreamhost.com:gitolite-admin

7.  Once downloaded, you should see a folder structure that looks like this:

        gitolite-admin
        ├── conf
        │   └── gitolite.conf
        └── keydir
            └── yourdesiredgitusername.pub


## Part 2: Example usage

Here are a few things you can do, once you've got gitolite installed on the
server, and downloaded locally to your machine. Remember that you administer
gitolite using the gitolite-admin clone on your local machine!

### How to create a new project repository with Gitolite

1.  Edit the `gitolite-admin/conf/gitolite.conf` file in your favorite editor.

        # Default configuration shown...
        repo  gitolite-admin
              RW+ = yourdesiredgitusername

        repo  testing
              RW+ = @all

        # Add the following for your new repository:

        repo  foo
              RW+ = yourdesiredgitusername

2.  Save the file, commit the change, and push it to the server.

        $ git commit conf/gitolite.conf -m "Added repository for the foo project."
        [master 90b63b7] Added repository for the foo project.
         1 files changed, 21 insertions(+), 4 deletions(-)

        $ git push
        Counting objects: 7, done.
        Delta compression using up to 4 threads.
        Compressing objects: 100% (3/3), done.
        Writing objects: 100% (4/4), 508 bytes, done.
        Total 4 (delta 0), reused 0 (delta 0)
        remote: creating elementalidad...
        remote: Initialized empty Git repository in /home/mygitoliteuser/repositories/foo.git/
        To mygitoliteuser@desarolo.com:gitolite-admin
           295694a..90b63b7  master -> master

3.  Now you can clone down your new repository… and start committing.

        $ git clone mygitoliteuser@xxxxx.dreamhost.com:foo
        $ cd foo
        $ touch file.txt
        $ git add file.txt
        $ git commit file.txt -m "Testing the foo project repository."

### How to add a new code contributor user in Gitolite

1.  First, you must obtain from your new contributor, his SSH public key.

2.  Place the public key file into the correct format, adding it to the
    `gitolite-admin/keydir` folder.

        mv pubkeyfile.pub  ~/gitolite-admin/keydir/username.pub
        git add keydir/username.pub
        git commit keydir/username.pub -m "Added public key for User Name"


[docs]: http://gitolite.com/gitolite/install.html#insttrouble
