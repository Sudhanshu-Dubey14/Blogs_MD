% GSoC Days: Week 1

The results were announced on May 4th and from then to June 1 was the Community Bonding Period. Which means that you need to interact with the mentors, with the organisation and get to know how they work. But we had done this already during the review period so we continued working. When the results were announced, it was all happy and merry with the congratulations but just after that things got serious!

## Rebasing

The first thing Bernd asked me to do was to rebase my branch with FreeCAD's master branch. There is this line he likes to use: "git rebase is your friend.". It surely isn't easy to befriend git rebase. The first time I did it, it completely messed up my local as well as GitHub branch. I had to check the [reflogs](https://www.atlassian.com/git/tutorials/rewriting-history/git-reflog) and hard reset evreything. * sigh *
Oh by the way, [git rebase](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase) means you change the "base" of your branch to the "head" of another branch. Simple right. Nah, I won't go in much detail here. That's reserved for the git related blogs.
But yeah, with more practice I can now say that me and rebase have become very good friends. It helps me rewrite the commit history in any way I want. So yeah, you should definitely send it a friend request as soon as possible.


I had to setup a [user page](https://wiki.freecadweb.org/User:Sudhanshu_Dubey) and [logs](https://wiki.freecadweb.org/User:Sudhanshu_Dubey/GSOC20/logs#TODO) to get things started officially.

## The Example GUI

Now this was the first major task, to get the GUI up and running. What we had before the results was just a list of the examples. You couldn't click to set them up.
Before we could implement that, some refactoring was required. Some modules had more than one examples in them. Also we had to standardise a way to run the example. After some dicussion, we came with the idea to have only one example in a module and to have a method `setup()` in every example which would setup the example.
So with more work in Qt, we implemented a list of all the examples and you can set them up with a single click. Cool.

This marked the end of the first week and my major learning in this week was git rebase and Qt. But honestly I was still struggling with rebase during the whole week. Git is all fun and good unless you start getting conflicts. And what do you do when you get conflicts, well:

![git](https://imgs.xkcd.com/comics/git.png)
