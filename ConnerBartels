#### Conner Bartels
#### Mini Project 01

# Step-by-Step Configuration Guide

##### Acquire all the necessary hardware and software needed to set up a 2 LAN networks that are connected with each other

This will include:
Router
Switch (x2)
End devices (x4)
Ethernet cables (x6)
Serial console cable

##### Add end devices to the switch

Connect the switch to the client (which is a computer in our case)
Do this with an ethernet cable. Plug one end of the ethernet cable into an available port on the switch. Plug the other end into the PC.
Connect the other end device to the switch using the same method.

##### Set IP addresses to the end devices

Open System Settings, go to the Network tab, turn off wifi, click on “USB 10/100/1000 LAN” (this should appear after you connect the switch and the end device), click on “Make Active”, then click on “Details…”, then click on “TCP/IP”. There will be something that’s called “Configure IPv4”. To the right of that, there will be something that says “Using DHCP”. Click on that and change it to “Manually”.
Enter your own IP address: (don’t use .1 for the last octet, this is saved for the default gateway)
Enter the subnet mask: Enter the subnet mask that aligns with the IP address (the subnet mask is essentially the binary code of the IP address transformed into decimal)
Enter the router ip address: use .1 for the last octet

##### Set up web browser on one of the end devices

Install MAMP
Select Nginx as the web server
Update nginx port from 8888 to 80 and press ok
Press the start button
Create index.html in the directory for you operating system
Mac: /Applications/MAMP/htdocs/index.html
Use Visual Studio Code or another code editor and type
“Welcome to Capstone Consulting {LAN##}”

##### Set up the DNS on one of the end devices

Install NAMO local DNS Server
Click + to add new host and create the host name
Set IP Address to individual IP address of designated laptop that does DNS server
System Settings
Network
Select the connected ethernet interface
Details
DNS
Remove and existing DNS Servers
Add the IP address of the laptop that is assigned to act as the DNS server
Confirm DNS Servers configuration
	From CLI (terminal):
Networksetup -listallnetworkservices
Networksetup -getdnsservers{NETWORK INTERFACE}

##### Test Connection by pinging

Go to terminal one of the end devices
Type “ping” and the IP address of the other end device that’s on the LAN
If this doesn’t work, do this (if you are on a windows:
Disable Windows Defender or
Update the firewall on the windows machine to allow ICMP
Add a firewall rule to allow ICMP command:
netsh advfirewall firewall add rule name=”Allow ICMPv4-In”
protocol=icmpv4:any,any dir=in action=allow
When done with the network, remove the firewall rule command:
Netsh advfirewall firewall delete rule name=”Allow ICMPv4-In”
Do this on both end devices to see if you can ping each other

##### Test the Web Server

Using the end device that is running DNS, go to a web browser and type in”http://” and then whatever the domain name is. The DNS should convert the web name into the IP address and the web page should load.
Troubleshooting method:
Check if all the IP addresses were typed in correctly
Check to see if the cables are plugged in

##### Add the router

Connect the switch to the router with ethernet cables

##### Configure IPs on the router (to set up the default gateway)

Turn on the router
Download a driver on an end device
Connect a serial console cable from the router to one of the end devices
Go to the terminal code and type:
router enable 
this enters EXEC mode to make changes
now what’s going to pop up is router# 
configure terminal 
press enter
hostname router01 
press enter
interface gigabitEthernet 0/0
t press enter
ip address 192.168.0.1 255.255.255.192
press enter
This is just an example IP address and subnet mask, enter the correct numbers when actually doing this
description ##to switch 01## 
then press enter
This describes the connection we are creating from the router to the switch
no shutdown
exit
wr
This writes the configuration into memory
show startup-config
Confirms the config was permanently saved

##### Turn the port status on (on the router)

##### Repeat steps 2-8 to set up to set up the other LAN

##### Configure IP address for the other LAN on the router (to finish setting up the default gateway)

Type:
config t
int g0/1 (enter)
ip add 172.16.0.1 255.255.0.0 (enter)
description ##switch 01
no shut (enter)
exit
wr
show ip interface brief
This will check to see if the IP addresses have been configured. Numbers that show up should be 0/0 and 0/1 instead of 0/0/0 and 0/0/1

##### Test Connection

Make sure the computers on different LANs can ping each other
Test to see if computers on different LANs can make an HTTP request to the other LAN’s web server IP
Make the HTTP request using a domain name

# FAQ:

On our project, Christopher was not able to ping the other LAN but they were able to ping him. What do we do?
We realized that Christopher likely had a firewall set up. Therefore, we concluded that he either had to disable the firewall or update the firewall to allow ICMP. In order to update the firewall, you must type in this code to the terminal:
netsh advfirewall firewall add rule name=”Allow ICMPv4-In”
protocol=icmpv4:any,any dir=in action=allow
After you are done with the firewall, you can remove it by typing in this code to the terminal:
netsh advfirewall firewall delete rule name=”Allow ICMPv4-In”
We tried the ping again and it worked.
We connected the switch to the router with an ethernet cable and an end device to the router with a serial console cable. We are attempting to configure it and we typed all the code in correctly, yet we think we are still missing something. What might be the issue?
Though this seems obvious, my group actually forgot to turn on the router. Make sure to turn it on and set the port status to on after setting its IP address.
How do end devices send data to one another within a LAN?
ARP (Address Resolution Protocol)
ARP finds a physical MAC (media access control) to match with an IP address on a local network. The purpose of this is so the end device that wants to send data knows where exactly to send it. It essentially helps devices on the same network communicate with each other.
Process
ARP Request
Device A needs to communicate with Device B
Device A knows Device B’s IP address but not it’s MAC address
Device A broadcasts an ARP request packet to all devices on the LAN (basically asking “Who has IP address X.X.X.X? Can you please tell me your MAC address?”
ARP Reply
Device B (with the matching IP address) replies with a packet (containing its MAC address). Device A stores this in its “ARP cache” for future references. An ARP cache will temporarily store IP-to-MAC address mappings.
Communication once MAC address is stored
Device A can use the MAC address of Device B to send data in ethernet frames directly to Device B
When you manually set your own IP address, it will ask you to type an IP address, a subnet mask, and the IP address of the router. When I did this for the first time, I wondered what the point of a subnet mask was. Please explain a subnet mask.
A subnet mask is a 32-bit number that divides an IP address into network and host portions. It’s used to determine which part of an IP address is the network address and which part is the host address.
It’s purpose is to help routers and devices on a network understand which IP addresses are within the same local network and which addresses are outside of it
How do hosts know which portion of the 32 bit number is network and which portion is host? This is the job of the subnet mask. 
Subnet mask is 32 bits long
255.255.255.0
In binary: 11111111.11111111.11111111.00000000
The first X.X.X represents the network
The last .X represents the host
Example
/24 at the end of an IP address means the subnet mask will start with 255.255.255
This is because the first 24 bits of the subnet mask represent the network. The last 8 bits identify the host address
What is an ICMP?
ICMP (Internet Control Message Protocol)
It is used for network diagnostics and error reporting.
ICMP manages and troubleshoots network operations by sending messages regarding network issues (like unreachable destinations or timeouts)
ICMP doesn’t handle data transfer between hosts, it provides feedback about network operations
Error Reporting
ICMP indicates network problems like unreachable hosts or network congestion
EX: a router cannot deliver a packet to its destination, therefore an ICMP Destination Unreachable message will go back to the source
What’s the point of running a DNS on a LAN?
DNS, or Domain Name System, translates domain names into IP addresses, therefore allowing computers to identify each other on a network. DNS allows you to find and website or service by name and not by having to remember confusing IP addresses

# Reflection:

During Network Cloud Computing class, my team and I set up a local area network (LAN). It was a hands-on experience, which deepened my understanding on the topic. While reflecting on this project, I realized the importance of problem-solving and attention to detail. These traits are vital if your goal is to successfully set up a connection between two LANs. Through the process, I encountered a number of obstacles, learned new skills, and discovered areas for future improvement.
The first challenge I faced arose when I mistyped my IP address while manually setting it up in my network settings. I noticed something was wrong when Christopher attempted to ping my computer. This resulted in failed ping attempts. It was only after carefully reviewing the network settings that I realized I mistyped my IP address. This highlighted the importance of accuracy when dealing with network configurations, as a small error can cause a significant problem.
Another challenge I encountered was a simple but significant mistake: I forgot to turn on the router. This might seem like a small issue but this fundamental step caused confusion to our group when we couldn’t establish a connection between the different LANs. At first, we thought it was a configuration problem, but after about 20 minutes, we realized that the router was off. Once the router was powered on, the network began functioning properly, allowing us to connect the two LANs together.
Our last complication was related to testing connectivity between LANs via ping. After setting up the IP addresses on all computers, our group attempted to ping one computer on LAN1 to another computer on the other LAN2. The ping worked in one direction, but not in the other. After checking the network settings and firewall configurations, we found that the firewall on one of the computers was blocking incoming ping requests. By adjusting the firewall configurations, we were able to solve the problem and establish a two-way connection between the devices.
Throughout this project, I gained a basic understanding on how to set up a LAN and how to think critically by solving troubleshoot errors, which will be valuable for future networking tasks. I definitely gained an understanding on how IP address configuration works. By setting up IP addresses manually, I learned how to ensure that devices within the same network can communicate effectively. I also was able to configure a router and set its IP address and default gateway, which was crucial in connecting the two LANs.
Another valuable insight was related to the troubleshooting process. When we encountered issues, whether it was related to the firewall or a mistyped IP address, we learned how to approach the problem systematically. By gathering information, breaking down the possible causes, and testing each one, I was able to resolve the issues in a methodical manner. This approach not only helped me fix problems during this project but will also be useful for my problems in general.
Additionally, setting up the DNS server and web server provided valuable hands-on experience with server configuration. Configuring a DNS server to resolve domain names and a web server to host a website gave me a deeper understanding of how different components of a network interact. I never knew that DNS even existed and it’s super interesting to think about all the things your computer does to make the user interface run smoothly.
While the project was ultimately successful, there are several areas where I could improve in the future. First and foremost, I need to pay more attention to details. The mistake of mistyping an IP address and forgetting to turn on the router could have been easily avoided with attentiveness. In future projects, I will make sure to double-check my configurations and hardware, which should save time and confusion.
Another area for improvement is firewall management. While we were able to resolve the issue of the blocked ping requests by adjusting the firewall settings, I realized I still don’t understand how firewalls interact with network traffic. In the future, I hope to spend more time learning about firewall rules and configurations.
Finally, I would like to improve my overall efficiency when working on networking projects. While I was able to solve the problems that arose during the setup, it took longer than expected to identify and fix some of the issues. By practicing more and becoming familiar with common network issues and their solutions, I can improve my troubleshooting speed and overall project efficiency.
