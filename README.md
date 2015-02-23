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




1) Save all your current router settings.
You probably have a router that is connected to the internet, and are reading this online. Save all your information on your current setup.

In particular, you want to find out:
a) The IP address of your current router.
It is usually 192.168.1.1.

b) Your administrator name and password to your router.

c) Your router configuration details on how it connects to your internet service provider. 
You can get this by logging in to your router and writing down the data on the main page under "WAN".
For some routers the data for "WAN" is called "Internet settings".

2) Get a router running DD-WRT. 

You have two ways to get this.
a) Buy a router that already has DD-WRT installed on it. This is the easy way, and recommended for anyone who is not a professional or technically skilled.

Buffalo Tech offers a series of routers pre-installed with DD-WRT. They are quite good.

http://buffalotech.com/
http://buffalotech.com/products/wireless/open-source-dd-wrt/airstation-n300-dd-wrt-router
http://buffalotech.com/products/wireless/open-source-dd-wrt/airstation-n450-dd-wrt-wireless-router

b) Upgrade a router to use DD-WRT.

This is actually hard to figure out if you are not tech savvy.

Not all routers support DD-WRT. You can use this table to see if your router is on the list:

http://www.dd-wrt.com/site/support/router-database

Make sure you type in the router type and version number correctly- I bought a Linksys WRT54G once, and it was version v7.0 which is the only version that isn't supported. Frustrating.

The instructions for installing DD-WRT vary per router type. Some of the instructions are very clear, and for other models, less so. My advice is, if you can't find your router listed as on the router database, get another router that is!

There is a LOT of help online dedicated to getting DD-WRT installed on your router. There is a separate page linking to some of these help pages.

3) Configure DD-WRT to connect to the internet.
This depends on how you previously connected your router to the internet. You want to duplicate whatever you did before.

Your DD-WRT router can now be accessed via http://192.168.1.1/
a) When you log in for the first time, it strongly recommends you set a new username and password. Do so.
b) Set up your router to have access to the internet. 
- Physically plug in the ethernet cable to the "WAN" or "Internet" port on your router to your DSL modem or cable modem.
- Set the WAN settings on the Setup page of the router (192.168.1.1) to the settings you saved during step #1.

4) Set up OpenDNS
Sign up at opendns.com, select "Home", and "Parental Controls". Sign up with your email for a free account "OpenDNS Home".

5) Configure DD-WRT to use OpenDNS:
- Log in to the router (192.168.1.1);
- Go to Setup->Basic Setup
- Under Router IP, set the Local DNS to 208.67.222.222

(The DNS server for OpenDNS is listed on their website, but is usually 208.67.220.220)
- apply settings.

6) Test that you are now using OpenDNS:
Log in to OpenDNS with your user account.
Click the link on the opendns page that says: "Click here to test your settings":
https://store.opendns.com/settings

or at the bottom of the page of:
https://store.opendns.com/setup/

You need this step to work before continuing. If it does not work, follow the opendns website help guides to see where you went wrong. 

Common errors:
a) You entered the OpenDNS DNS server wrong on the dd-wrt router
b) You have the DNS server value set on your computer manually, which is overriding the router value. Go to your computer internet settings, and delete your DNS server data.  Note that step 8 would force your computer to use OpenDNS' DNS server, no matter what yours had been set to, but it is good to get things verified at this point before moving on to more complex settings.


7) Set up OpenDNS for your network.
a) Log in to OpenDNS with your free account.
b) It should automatically detect the ip address for your network. Add that network. 
c) Your network probably has a dynamic ip address, meaning that your internet service provider doesn't give you the same address all the time.
You need to install an OpenDNS tool on at least one computer on your network that will tell openDNS when your dynamic ip address changes.
There should be a link to download this tool, called OpenDNS Updater.
d) Download, install and run OpenDNS Updater.
e) Enter in your OpenDNS username and password
f) Select your network (you probably only have one to choose from, called "home")
g) Select "Send Dynamic IP updates" checkbox.

8) Configure OpenDNS to filter content.
a) Log in to OpenDNS
b) Select your network
c) Select the web content filtering you desire.


9) Set up DD-WRT to force all users to use OpenDNS.
http://www.dd-wrt.com/wiki/index.php/OpenDNS
http://emtunc.org/blog/05/2011/force-dd-wrt-to-use-opendns-servers-for-dns-queries/

You now have the basic system working, but a user on your network can STILL set his DNS manually and avoid using DNS. 
a) 
Go to Services tab » Services sub tab » Services Management section » DNSMasq sub section
Enable both DNSMasq and Local DNS options

In the Additional DNSMasq Options text box, enter:
no-resolv
strict-order
server=208.67.222.222
server=208.67.222.220

b)
Go to the Administration tab on your DD-WRT gateway page.
Click on the Commands tab.
In the Commands box, enter the following then click Save Firewall

iptables -t nat -A PREROUTING -i br0 -p udp --dport 53 -j DNAT --to $(nvram get lan_ipaddr)
iptables -t nat -A PREROUTING -i br0 -p tcp --dport 53 -j DNAT --to $(nvram get lan_ipaddr)

Note:
You may experience "stuttering" for video on some sites, like hulu or netflix, with this option enabled.
If you do, you can either
a) Remove the iptables command, delete it, and save the command as empty
b) Edit the iptables command to allow SOME clients access to the normal DNS servers, and the rest to the opendns servers.
http://www.bachyaproductions.com/using-dd-wrt-to-override-dns/


A tutorial on what these iptables commands mean:
http://www.astro.ff.vu.lt/~viktoras/toplanet/Iptables_command.htm
http://www.dd-wrt.com/wiki/index.php/Iptables_command

10) Test!
As a test, you might want to filter something safe like "Social Networking" on the OpenDNS Web Content filtering.
Then wait 3 minutes, and try go to facebook.com. You should not be able to access it, and should instead visit an OpenDNS page that tells you that you can't access that material.

If you like, you can then test trying to go to other objectionable sites, but once it filters anything, it basically works on any of the filters you enabled.

You win. The end.



