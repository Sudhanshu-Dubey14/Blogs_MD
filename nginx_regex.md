# Nginx x Regex

Too many x's in the title, right. Well that's kind of required and interesting. In this post, we will be talking about [Nginx](https://www.nginx.com/) the web server, [Regex](https://en.wikipedia.org/wiki/Regular_expression) the legend's way of searching and how I have combined the power of the two to get my work done.

What was my work? Well, to put it simply, it was to enable [CGI](https://en.wikipedia.org/wiki/Common_Gateway_Interface) for every user. It sounds simple but it wasn't. The details of how I completed my task will be discussed in another post and here today we will kind of build the base for it by discussing the background stuff.

## So what is Nginx?

> nginx [engine x] is an HTTP and reverse proxy server, a mail proxy server, and a generic TCP/UDP proxy server, originally written by [Igor Sysoev](http://sysoev.ru/en/).

The above is how Nginx [define themself](https://nginx.org/en/). For us simple folks, its a [web server](https://en.wikipedia.org/wiki/Web_server).
Now people who know their networking stuff will ask "Why Nginx?", "Why are you going for all the trouble when you can easily have [Apache](https://httpd.apache.org) do the job for you?". Well, here are my reasons:

1. Because [some researches](https://www.digitalocean.com/community/tutorials/apache-vs-nginx-practical-considerations) indicate that nginx is faster and more efficient than apache.
1. Because it is much more challenging and fun than just doing `a2enmod`.

So now that we are clear as to why I am using Nginx, let's move on.

## What is Regex?

Expanding to [Regular Expression](https://en.wikipedia.org/wiki/Regular_expression), it is a sequence of characters that define a search pattern. Usually such patterns are used by string searching algorithms for "find" or "find and replace" operations on strings, or for input validation. It's concept was given by [Stephen Cole Kleene](https://en.wikipedia.org/wiki/Stephen_Cole_Kleene).

Recently, I have found a mention of regex in our Theory of Computation classes. But honestly, I like it's practical applications more than it's theory.

Anyway, if you casually look at a regex it's just a strange collection of characters. But so is programming a strange collection of words and numbers and we all the know how incredibly powerful it is. Similarly, regex are incredibly powerful if someone know how to handle them. [Here](https://medium.com/factory-mind/regex-tutorial-a-simple-cheatsheet-by-examples-649dc1c3f285) is a cheatsheet of regex if you want to get a taste of it.

Now comes the important thing, how regex is used in Nginx. Well, without getting much technical here I will just show you a simple demo cause the bulk of it will be dicussed in the next post.
So this is what you add in your site's configuration in Nginx for enabling [per-user web directories](http://publib.boulder.ibm.com/httpserv/manual70/howto/public_html.html):

	location ~ ^/~(.+?)(/.*)?$ {   
	alias /home/$1/public_html$2;                                                                                                                       
	index index.html index.htm;                                                                                                                          
	autoindex on;                                                                                                                                         
	}

Now what is happening here???
First of all, focus only on the first two line cause the last two aren't important right now.
So, basically it is telling Nginx to look for the pattern `^/~(.+?)(/.*)?$` (this is the regex here and remember regex are patterns) in the URL and if a pattern is found then name that pattern `/home/$1/public_html$2`.

Thus, if you pass a URL like `https://code.gdy.club/~1715081/cgi-bin/info.php`, then it will extract this `/~1715081/cgi-bin/info.php` as the pattern and try to see if it matches the given regex or not. Now this one matches (believe me!) and to see how, we need to understand the given regex which we will be dissecting now (easier for those who have gone through the cheatsheet):

1. ^ : This signifies the start of the regex.
1. / and ~ : These are simple characters, meant to be matched exactly.
1. (): These are used for grouping, both of the times.
1. . : Meant to match any single character.
1. + : Meant to match one or more of the previous character (Here it's '.', i.e any single character)
1. ? : Meant to match zero or one of the previous character (Here it's ".+", i.e any character sequence with 1 or more characters).
1. **(.+?)** : Thus this is a group having the smallest sequence of any possible characters (except null terminators).
1. * : Meant to match zero or more of the previous characters (Here it's '.', i.e any single character)
1. (/.\*)? : This is a group of characters that starts with '/' and then goes on till the end.
1. $ : This signifies the end of the regex.

Now if we make a one-to-matching between the pattern and the regex, we get:

- /~ = /~
- (.+?) = 1715081
- (/.\*)? = /cgi-bin/info.php

And since we have used grouping:

- $1 = (.+?) = 1715081
- $2 = (/.\*)? = /cgi-bin/info.php

Finally replacing the variables $1 and $2 are replced and we get `/home/1715081/public_html/cgi-bin/info.php` which is the full path of the file on the server and now that Nginx has the address of the file show, it can show it properly.

\* drinks a glass of water * "sigh!" Now that was quite long and sorry if I couldn't make it completely clear to you. Regex is a matter of practise after all.
Now in the next post, we will get into more details of it and how I got CGI to work on my Nginx server.

And since you have endured this long with me to learn regex, let's save the world with it:

![](https://imgs.xkcd.com/comics/regular_expressions.png )

Ah, but I have used it before too, so here is another:

![](https://www.explainxkcd.com/wiki/images/7/7b/regex_golf.png)

And if you want more of this comic and regex, well [enjoy!](https://www.explainxkcd.com/wiki/index.php/1313:_Regex_Golf)
