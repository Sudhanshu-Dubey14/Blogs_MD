# Using Git

Hey there,

Been so long since posted something here. Well, as you guessed I was busy with stuffs, you know learning and working.
So today I am going to discuss with you guys a very important tool that all developers must use. In fact, why only devs!
Anyone who is working on anything that is long term and requires you change a set of files a number of times should use this amazing tool.

And its called **Git**.

Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency. When I say "version control system", it means a system that tracks and documents (using commit messages) the progress of your project, all the changes that you make.

Git was created by Linus Torvalds (the man who created linux) in 2005 for development of the Linux kernel, with other kernel developers contributing to its initial development. Its current maintainer since 2005 is Junio Hamano.

And though there are a lot of tutorials to learn git like [this simple one](http://rogerdudler.github.io/git-guide/) and [this detailed one](https://www.tutorialspoint.com/git/) 

But what you will get here, is my experience in git on linux i.e what all git commands I have ever used. So they will be a kind indication as to what commands you will mostly need while working with git.
Of course, it would be dynamic post which will be propostionate with my experience in git.

So lets start!

## Creating a Repo

1. Create a new directory (using mkdir).
2. Run the following to create a new git repository:

**``git init``**

## The Workflow

- Your local repository consists of three "trees" maintained by git. 
- The first one is your Working Directory which holds the actual files. 
- The second one is the Index which acts as a staging area. 
- And finally the HEAD which points to the last commit you've made.


![Git Workflow](http://rogerdudler.github.io/git-guide/img/trees.png "Git Workflow")


## Tracking Changes

- Now if you want to see what changes you have made with regards to the files, then you run:

**``git status``**

## Proposing Changes

- You can propose changes (add it to the Index) using:

**``git add <filename>``**

**``git add *``**

## Finalising Changes

- To actually commit these changes use:

**``git commit -m "Commit message"``**

- Now the file is committed to the HEAD
- To write and additional description add another -m flag like:

**``git commit -m "Commit message" -m "Additonal Description``**

- We write additional description seperately, because commit messages should be short and precise.

## Viewing Changes

- In its simplest form, you can study repository history using: 

**``git log``**

- You can add a lot of parameters to make the log look like what you want.


## Sending files to remote server

- To send files to a remote server :
 
**``git push <remote-url> <branch>``**

## Retrieving files from remote server

- To retrieve files from a remote server and merge with local files:

**``git pull <branch>``**
  
So this was it for now. Thats how much I have used till the date this post was published.
As and when I learn and use new commands in git, I will update them here.
Feel free to leave new and useful git commands in comments or ask for any help regarding git.
