# Setting Up Cache Server: Day 1

<div markdown="1" style="display: flex">

<div markdown="1">

Hello guys,

Been a long time since I posted something, right!
Well, I busy with work and today I started a new work.
And I want to blog the daily progress of this work, so this blog is about the first day which was today. 
We have some unused servers and we wanted to utilise them in some way, so we thought of setting up a cache server.
This server would be connected to our main server and would work like a cache memory in your computer.
That is, whenever someone downloads something through our server, a copy of that will be saved in the cache server.
So that the next time someone wants to download the same thing, he will get it from our cache server must faster than fro he internet.
Also this will save the very precious bandwidth of our main server and thus increasing the overall speed of all the other users.

</div>

<div>
<img src="http://www.itinstock.com/ekmps/shops/itinstock/images/IBM-X3650-M2-2U-Server-2-x-QUAD-CORE-E5540-16GB-RAM-RAID-2-x-PSU-34802-p.jpg" alt="IBM Server">
</div>

</div>

<div markdown="1" style="display: flex">

<div markdown="1">

## Looking up the old server

So, to get started, we first had a look of our server that we wanted to use.
Its a really old IBM server.
It had 3 hard-disks in it, each of 148 GB.
Since that only made 444 GB, we though of replacing them with HDDs of 500 GBs each.
This would not only increase the available space of the server, but also we can protect any data that might be there in the old HDDs.

Luckily, we got our hands on a 500 GB HDD. One is good enough to start experimenting.
But the moment we tried to replace the old HDD with the new one in the HDD slot, we had a big problem.
The screws that connected the HDD with the slot required special hex screwdrivers with pin in the centre.
Quite obviously, we didn't had such stuff in our software oriented lab.
So that put a pause to our work for quite some time. We even thought that we would leave the work for today and continue tomorrow.
(During the pause, we had an MTech student tell us about his work in cryptography!)
Another of our member joined us and now there were three of us.
While explaining to him what all had happened before his arrival, it suddenly crossed my mind that one of my hardware oriented friend might have the required screwdriver.
Well, he didn't had the exact one that we required but one of his small screwdriver was more than what we needed.
Returning to our lab, I found that our third member was testing whether the new 500 GB HDD was working or not.
Sadly, the disk was not responding to any connection! So yeah it's not working. :-(
But we were able to atleast change the HDD in the slot so we may directly test it on the server.

</div>

<div>
<img src="http://www.server-harddrive.com/photo/pl11436686-3_5_form_factor_73gb_hot_swap_hard_drive_15k_for_ibm_40k1043_39r7348_26k5841.jpg" alt="HDD in Slot">
<img src="https://www.brycefastener.com/images/products/tam-6lobe.png" alt="Hex Screw">
</div>

</div>

## Plans for Day 2

So now we have only our old HDDs to work with, unless we buy new ones.
Tomorrow is a holiday, so we are hoping to get a lot of work done with the five of us together.
Our first target is to check the contents of the old HDDs using a live Ubuntu.
This step could have been skiped, if we had new HDDs.
Then, we will backup all the contents, format the HDDs and install Ubuntu 18 LTS (They currently have Ubuntu 12, I guess).
Rest we will see what to do, and I will tell you guys tomorrow what all happened. 
