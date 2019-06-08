# Windows to Linux File Transfer over LAN

So today (on the 4th day of my summer internship), we were trying to move data (30 GB of it) from a Windows system to a Linux system.
Being network engineers, we thought it wasn't much of a headache. We tried the following things:

### Over Ethernet Cable

We connected both the systems using an ethernet cable and then assigned IP addresses to them so that they would be in the same network (10.0.0.10 and 10.0.0.11). 
Ideally, it should have worked. The computers were connected in a peer to peer connection, there should have been no issue, **but** there was one.
And it was an issue that didn't even allowed us to ping to each other!!!
Was it that we hadn't defined the Gateway?? Was it that the cable was damaged??
We never found out!!! But we will go deep into this some other time.

### Over WLAN

The next thing we did was create a hotspot from the mobile and connected both the systems to that hotspot. Now we were in the same network and were able to ping each other. So far so good!!!

Then we enabled the sharing options in Windows, but were not able to see the Windows system on Linux (unlike what happens in Windows to Windows transfer).
We tried many things, but in vain.

Then I searched for some tutorial and got [this](https://www.howtogeek.com/176471/how-to-share-files-between-windows-and-linux/).
We followed it, but were getting error:

``mount error(115): Operation now in progress``

Searching for this error, I got this helpful [answer](https://superuser.com/questions/430163/cifs-share-mount-errors).
Following this, I used the command:

    [root@defiant mnt]# mount -t cifs //<IP address>/<Shared Folder> <Location to mount on> -o username=<username>
    Password for <username>@//<IP address>/<Shared Folder>:  **********
    [root@defiant mnt]#

But I later realised I had mad a rather big mistake!!!

I used /home/sudhanshu as <Location to mount on> and that **removed all the data on my home folder**.
I was confident that I would be able to recover that so we continued on with the sharing on files.
Now had the Windows file mounted on my system, so access of data wasn't a problem. The problem was the speed of the WLAN connection.
It wasn't supporting transfer of large number of files at once and was getting hanged up frequently.

So after a few tries, we gave up on transfering 30 gb of data through that poor WLAN connection.

But now I had the big task of recovering ~semi-important~ data. But before doing anything, I gave the whole process a thought.
The command I used was ````mount````, that meant that the data of windows was **mounted** on /home/sudhanshu/, /home/sudhanshu/ was just a **name** for that data.
So my previous data was there, only that it was unmounted.
And surely enough, ````df -h```` revealed that my root directory was occupying the same space as before. That was a **huge** relief!!!

I new that restarting the system would remount that lost part but I decided to do it manually.
The problem that I thought would occur was that /dev/sda4 (the filesystem containing my root directory) was mounted on "/".
Now only a part of /dev/sda4 was unmounted, so I wasn't sure how to name that specific part and mount it on /home/sudhanshu/.

While I was thinking all this through, my system hanged up while reconnecting to the Windows system (I had disconnected the hotspot) at this point. Logging into to tty, it said that the system required a restart. Unable to do it any other way, I used good-old REISUB.

Any my data was back after the restart. But we will try again to transfer data from windows to linux in a better way later on. 
