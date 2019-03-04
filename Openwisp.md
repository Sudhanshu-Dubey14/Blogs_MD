## Installing OpenWisp2 in Raspberry Pi

Hey there!

We have been trying to do new things here. Due to some of our requirements, we are trying to create a switch in a router so that it can create different VLANs (Virtual Local Area Network) in each of its ports. For example, one device connected to a port should get an IP like 192.168.20.x and a device connected on another port should get an IP like 192.168.31.x. Thus, each device on a port should be in a different subnet as compared to device on another port. Now your normal router won't do this, instead it would assign IP's to all the devices so that they are in the same subnet.

To achieve this, after quite a bit of research, we found a nice software: [OpenWisp](http://openwisp.org).
OpenWisp is a network management system that allows managing and automating several aspects of a network:

1. Dynamic auto-configuration of new nodes
1. Dreation of VPN tunnels
1. Initialization of WiFi access points
1. Configuration of mesh networks
1. Configuration of any other network configuration supported by OpenWRT 


