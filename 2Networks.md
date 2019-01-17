# Setting up Two Networks in One Server

Hey guys, I am back with a report something interesting that I did today.

## The Targets

So yesterday, we restarted this work of setting up 2 networks in a single server using 2 network cards.
Suraj and Alok installed CentOS in the server.

Today, Suraj and I configured both the network cards one by one and were able to ping either <IP1> or <IP2> from my local
system. Also, we weren't able to ping to <IP3> from the server. ( <IP1> can be accessed from anywhere wheres <IP2> and <IP3> can only be accessed from within the local network)

We had 2 targets:

1. To be able to ping/ssh both <IP1> and <IP2> simultaneously. 
1. To be able to ping <IP3> from the server.

For that, we did quite the intensive research work. I even tried to learn the basics of networking since we had guessed that problem was
between the gateway and the device because we were able to ping to both the gateways irrespective of systems being up or down.

And indeed, the research revealed that the problem was in the gateway since by default a system has only one gateway as multiple gateways may cause ambiguity.
The general solution of having a common gateway for both the IP's didn't worked for us. We used the gateway of real IP for local IP and
vice versa but in vain.

## The Solution

By this time, only me and Satinderpal sir were working on this problem.

I somehow found this nice, [life-saving tutorial]( https://www.thomas-krenn.com/en/wiki/Two_Default_Gateways_on_One_System)
on how to have two default gateways on a system.

According to that, the solution was to create another routing table (by default we have only one) using iproute2 and set up rules on when
and how to use that routing table.

So I followed the tutorial, which can be briefly described as:

1. Add a new routing table called "rt2" (name can be anything) in the file /etc/iproute2/rt_tables with preference one.
   After which the rt_tables file should look like this:

    ````#
	# reserved values
	#
	255     local
	254     main
	253     default
	0       unspec
	#
	# local
	#
	#1      inr.ruhep
	1 rt2````

1. Add network details, IP Address and link it with the respective network card using command:
   
  ````ip route add <Network2>/24 dev <NetworkCard2> src <IP2> table rt2````  

1. Add gateway and link it to the card using:

   ````ip route add default via <Gateway2> dev <NetworkCard2> table rt2````

1. Add rule to get traffic from IP address using the rt2 table: 

   ````ip rule add from <IP2>/32 table rt2````

1. Add rule to direct traffic to IP Address using the rt2 table:

   ````ip rule add to <IP2>/32 table rt2````

After doing these temporary changes, I was able to ping both the IPs simultaneously from my local system, so first target was achieved
(YAY!).

For the second target, Satinder sir helped me. We predicted from intuition that we only need to make some changes in the rules.
And indeed that was the case. To ping to <IP3>, we only needed to add its from and to rules:

    ````ip rule add from <IP3>/32 table rt2
    ip rule add to <IP3>/32 table rt2````

And Boom!!!
We were able to ping to <IP3> from the server, so second target achieved.

## More to do

But these were temporary changes, to make them permanent we had to add these command to some file like /etc/network/interfaces.
But alas!
CentOS 7 has no such interfaces file. Instead it has rc.local file (in fact 2 of them) where we need to add commands if we want run them at
automatically after booting.
The commands that should be added to the rc.local file are:

 ````iface <NetworkCard2> inet static
    address <IP1> 
    netmask 255.255.255.0
    post-up ip route add <Network2>/24 dev <NetworkCard2> src <IP1> table rt2
    post-up ip route add default via <Gateway2> dev <NetworkCard2> table rt2
    post-up ip rule add from <IP1>/32 table rt2
    post-up ip rule add to <IP1>/32 table rt2````
 
The rc.local files requires permission to run after boot which is given by:

  ````chmod +x /etc/rc.d/rc.local````

So after all that, we thought that we were done.
But no, after rebooting, the changes we had done did took affect but now the <IP1> was down.
We had to shut the <IP2> and get it up again to get the <IP1> back.
And then implement the temporary solution again to achieve both targets.

We then tried a few things and did a bit of debugging but nothing worked.
So currently, the server is up with both IPs running and everything fine but after a network restart/ system reboot we will be back with
only <IP1>.

We will tryo to find a permanent solution and then I will update this blog.

Till then, see ya.

Our guess of the problem is that we are setting the preference of rt2 table higher than the default routing table, thus it is making the
network of rt2 table as the primary one. (we have tried changing the preference but to no effect.)

