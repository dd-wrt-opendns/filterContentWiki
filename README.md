# filterContentWiki
This is a wiki to describe how to set up dd-wrt to use OpenDNS to filter content.
How to set up filtering for your home or office:

This is a tutorial to describe how to set up your network to allow filtering in your home or office.

It uses a combination of DD-WRT and OpenDNS.

DD-WRT is firmware for your router that makes it more powerful, in particular on how it handles filtering and forwarding of data.

OpenDNS is an online service that keeps track websites by category (business, news, porn etc), and allows you to filter what websites you can access.

OpenDNS controls access by providing a DNS server for your computer to use.

DNS is the tool that helps your computer figure out where on the internet to look to find a website.  When you type in www.google.com, DNS translates www.google.com into an IP address, like 173.194.219.103 (an actual example).

There are many available DNS servers. Your internet provider offers you one by default.

You can set your computer to use OpenDNS instead of your internet provider's default DNS server. OpenDNS keeps track of which website categories you don't want to access, and when your computer asks OpenDNS for a website you don't want to access, OpenDNS returns an "failed" IP address, saying you can't access that webpage.

Signing up for OpenDNS doesn't mean that computers in your home or office need to use it though- a person on your network could simply set his DNS server manually to something like 8.8.8.8 (the google default DNS server), and OpenDNS would never be accessed for that user, so he would have unfiltered access to the internet.

This is where DD-WRT helps you. DD-WRT has the ability to forward all DNS packets to go to OpenDNS, no matter where the person on your network asked that packet to go (such as 8.8.8.8). This means that as long as you control your router, anyone on your network would be filtered by the OpenDNS filters on content.

Here is what you will need to do:

1) Save all your current router settings.
2) Get a router running DD-WRT. 
3) Configure DD-WRT to connect to the internet.
4) Set up OpenDNS
5) Configure DD-WRT to use OpenDNS:
6) Test that you are now using OpenDNS
7) Set up OpenDNS for your network.
8) Configure OpenDNS to filter content.
9) Set up DD-WRT to force all users to use OpenDNS.
10) Test for filtering
