# Git + SSH = Private Collaboration

Today (on the 6th day of my Summer Internship) I got my local server (that I had asked for on the [4th day](https://hacksd.wordpress.com/2019/06/08/day-4-of-summer-internship/)) where I could push my code to collaborate with my head and work together.

Now I have been using git for over a year now and have even written a [blog](https://hacksd.wordpress.com/2019/02/28/using-git/) of all I know about git. But all this time, my remote server was one of Github and that did not required any particular setup to worked with.
But now I had a remote server of my own where I needed to push the code and that did required a bit of tweaking.

I basically followed the [helpful guide](https://bobbelderbos.com/2012/03/push-code-remote-web-server-git/) here. 
And it indeed helped me to successfully push my code to the remote. Thanks [Bob Belderbos](https://bobbelderbos.com/about)! :-)
So why am I writing this post? Well here's why:

- He sets different directories as .git and the Working directory (where the code resides). Now this is somewhat different to how git normally works, where your .git directory is present inside the Working directory itself. His setup didn't suited my taste. I was able to use git commands like git status while in the working directory, because obviously the .git folder was not there. So here is a slightly different way.
-  We in [GD](http://greatdevelopers.github.io/) had a discussion some time ago that whether we need to initialise a git repo in the remote server before pushing a new repo or not. The arguments from both side were convincing and I don't think we reached a conclusion then. So getting the opportunity, I tried that and got the result.
- I also tried a few other things to clear my own doubts which are mentioned here.

So lets go!!!

To push your code to a remote server of your own, you need to follow the following steps:

1. Create a git repo in your local system, write your code and commit it. The basic guide for all that is [here](https://bobbelderbos.com/2012/02/git-in-a-nutshell/) (Bob's blog as a thank. You may search the net for git for begginers).
2. SSH into your remote server (here is a [helpful article](http://matt.might.net/articles/ssh-hacks/)) and do the following:

``$ mkdir ~/newrepo      # Create your working directory
   $ cd ~/newrepo	  # Enter your working directory
   $ mkdir .git		  # Create hidden directory to keep git files 
   $ cd .git		  # Enter the .git directory
   $ git init --bare	  # Initialise a bare git repo``

We are specificaly initialising a "bare" repo so that git doesn't sets the index and working tree on its own, because that will later contradict with the index of the repo you will push.

3. Now tell your empty repo where to put its code by:

``$ cd .git/hooks/
  $ vi post-receive``

And in that file, put these lines:

``#!/bin/sh
  GIT_WORK_TREE= ~/newrepo git checkout -f``

And give this script the permission to execute:

``$ chmod +x post-receive``

4. Come back to your local machine and add the remote server to your repo:

``$ git remote add aliasName ssh://user@domain.com/newrepo/.git``

Make sure to specify the user as the username on the remote server, otherwise it will try to use your local machine's username which may result in you not getting access to the server.

5. Push the code to remote location, creating a new "branch" master there, the hooks/post-receive script causes the source code to be copied to your Working directory, which is the parent of .git directory. So here we are pushing master to aliasName:

``$ git push -u aliasName +master:refs/heads/master``

6. Following updates are easy. After local committing with: 

``$ git add .
  $ git commit -m "message"`` 
  
You push your code to your remote server with: 

``$ git push -u aliasName``

So there you have it.

After all was done, I tried to investigate the question "Is it neccessary to initialse a git repo on remote server before pushing code there?"
Well here is what I did:

``sudhanshu@dubey:/media/sudhanshu/Thunder/Repos/spam_filter$ git remote add local_nogit ssh://root@10.1.1.153/root/
sudhanshu@dubey:/media/sudhanshu/Thunder/Repos/spam_filter$ git push -u local_nogit  +master:refs/heads/master
root@10.1.1.153's password: 
fatal: '/root/' does not appear to be a git repository
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.``

So the answer is **YES**.
You definetly have to create an empty bare repo before pushing code to a remote server.

Also, what if we don't create a bare one, but a normal repo with ``$ git init``. Here is what will happen:

``sudhanshu@dubey:/media/sudhanshu/Thunder/Repos/spam_filter$ git remote add local_nobare ssh://root@10.1.1.153/root/Repos/dummy/.git
sudhanshu@dubey:/media/sudhanshu/Thunder/Repos/spam_filter$ git push -u local_nobare  +master:refs/heads/master
root@10.1.1.153's password: 
Counting objects: 960, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (958/958), done.
Writing objects: 100% (960/960), 982.45 KiB | 3.84 MiB/s, done.
Total 960 (delta 7), reused 0 (delta 0)
remote: Resolving deltas: 100% (7/7), done.
remote: error: refusing to update checked out branch: refs/heads/master
remote: error: By default, updating the current branch in a non-bare repository
remote: is denied, because it will make the index and work tree inconsistent
remote: with what you pushed, and will require 'git reset --hard' to match
remote: the work tree to HEAD.
remote: 
remote: You can set 'receive.denyCurrentBranch' configuration variable to
remote: 'ignore' or 'warn' in the remote repository to allow pushing into
remote: its current branch; however, this is not recommended unless you
remote: arranged to update its work tree to match what you pushed in some
remote: other way.
remote: 
remote: To squelch this message and still keep the default behaviour, set
remote: 'receive.denyCurrentBranch' configuration variable to 'refuse'.
To ssh://10.1.1.153/root/Repos/dummy/.git
 ! [remote rejected] master -> master (branch is currently checked out)
error: failed to push some refs to 'ssh://root@10.1.1.153/root/Repos/dummy/.git``

So that was it. You can start reading blogs of my summer internship days from [here](https://hacksd.wordpress.com/2019/06/05/day-1-of-summer-internship/)



