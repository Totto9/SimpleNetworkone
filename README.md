# Building Simple Network

Components

## Local Network

1 router, 1 switch, 3 PCs

## To Simulate :

**Internet Access:** 1 External router, 1 Web server

**Website Access:** 1 DNS Server

   ## Step-by-step configuration
## Link the PCs together

The 3 PCs are linked to the switch's first 3 ports (FastEthernet 0/1 0/2 0/3) through their FastEthernet0 port. 

I've attributed the ips/subnets masks to the PCs' interfaces as instructed and made sure the interfaces were up on both them and the switch.

Devices: PC-Arrow    Lan: Eth IP: 192.168.1.10 Mask: 255.255.255.0

Devices: PC-Vegas     Lan: Eth IP: 192.168.1.11 Mask: 255.255.255.0

Devices: PC-Jackson Lan: Eth IP: 192.168.1.12 Mask: 255.255.255.0

The PCs can communicate with each other. By the way, the IP address on the switch is not configured, so the ping between the switch and other devices is not working.
I work plug and play here. I also don't have passwords or message banners configured.

## Add the router that will provide the internet 
The GigabitEthernet 0/0/0 port of the local router is connected to the GigabitEthernet 0/1 port of the switch. The router's interface is configured with the following IP/subnet mask: 192.168.1.1 /255.255.255.0. Again, I've made sure the interface is operational. The router's IP can now be set as the default gateway for the 3 PCs. This will enable ping between the local router and the PC.

Simulate access to the Internet by creating another network with the web servers we need access to
The external router's ## GigabitEthernet 0/0/0 port is linked to the webserver's FastEthernet0 port.
The router's interface is configured with the following ip/subnet mask : 192.140.1.1 / 255.255.255.0.
The server's interface is configured with the following ip/subnet mask : 192.140.1.10 / 255.255.255.0 and it's default gateway is 192.140.1.1.
Again I made sure the interfaces are up and running.
The external router can now ping the webserver.

## Enable communication between the networks so we can reach the webserver
The routers are linked together through their GigabitEthernet 0/0/1 port.
The local router's interface is configured with the following ip/subnet mask : 192.168.2.1 / 255.255.255.0.
The external router's interface is configured with the following ip/subnet mask : 192.168.2.2 / 255.255.255.0.
Again, I've made sure the interface is operational.

The routers can now ping each other. But at this time, the PC cannot communicate with the web server, or even communicate with the external router, and a route needs to be added.

First on the local router with a route to reach network 192.140.1.0 with the mask 255.255.255.0 through next hop which is 192.168.2.2.
Then on the external router with a route to reach network 192.168.1.0 with the mask 255.255.255.0 through next hop which is 192.168.2.1.
The PCs can now reach the webserver on another network. If we use a browser on a PC and try to reach 192.140.1.10, the default cisco packet tracer webpage will be displayed.
But users mostly use domain names. Let's say the domain name of this site is www.cisco.com. If we try to reach it we get a "Host Name Unresolved" error. It's because our network doesn't know which ip is behind this domain name. So we're gonna add a local DNS server to help us.

## Setup the DNS server
The DNS server will be linked through its FastEthernet0 port to the switch's FastEthernet 0/4 port.
It is configured with the following ip/subnet mask : 192.168.1.254 / 255.255.255.0. It's default gateway is 192.168.1.1.
Again I made sure the interfaces are up and running.

The DNS server can now be reached by other end devices.
I've enabled the DNS service on the DNS server and I've added an entry with the name www.cisco.com which has the address 192.140.1.10.
Then I've configured all the end devices with 192.168.1.254 as the DNS server address.

## Related

Here is my first project!

[Link to the PKT file](https://github.com/Totto9/SimpleNetworkone/blob/main/FirstSimpleNetwork.pkt)







