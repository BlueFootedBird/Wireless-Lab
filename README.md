# Wireless-Lab
A simple Wireless Lab that I developed as a fun project as a way to teach other people about Wireless Security. Also lays the foundation for creating a completely free, remote network range to facialite hands-on labs for cybersecurity.

# Let's Teach Wireless
As both a student and a former teaching assistant, I firmly believe that the best way to teach and learn involves hands-on lab exercises. However, there are two main challenges when teaching wireless security with hands-on labs:

1. Students require specialized hardware to perform wireless tasks.
2. Students must be physically close to an access point (AP).

Let's address each of these issues one by one.

## The Hardware Dilemma
Assume we are professors at a university. We want to give students a lab (as seen in this repository) where they can perform a WPA2 deauthentication attack.

### What's a Deauth Attack?
For those unfamiliar, this attack aims to deauthenticate (forcibly disconnect) a client (somebody's laptop) from the access point (their router). When this happens, the client will attempt to reconnect to the access point. During this process, a 4-way handshake is performed, during which the hash of the password used to connect to the access point is broadcasted. As attackers, we can capture this hash and attempt to crack it offline using a brute force or dictionary attack. Once we crack the router's password, we can authenticate to the network ourselves, enabling us to scan/sniff the network. This attack is trivial to perform with the right hardware and works on any WPA2-PSK network (which is most of the routers connected to the internet). More info here.

## Back to the Hardware Problem
To perform these tasks, network adapters need to operate in "promiscuous mode." Special hardware is required to enable promiscuous mode, as this feature is disabled on most network interface cards (NICs) that come with computers and laptops. An adapter only costs around $15, so they are relatively inexpensive. However, even if we have X network adapters for X students, administering a lab where students perform a deauth attack presents a challenge. Students cannot perform this attack on just any network—that would be illegal. Therefore, we would need to provide a router in a lab with a weak password specifically for students to target.

## The Physical Issue
Another problem is that students need to be physically close to the access point. What if you have remote students? They wouldn't be able to come in person to do the lab. Even if we provide monitored lab time for 2 hours to use the hardware in a supervised environment, what happens if they don't complete the lab in time? We can't just loan out the adapters for students to use at their leisure—they could lose them or use them maliciously. It would be a terrible look if a student used university-loaned hardware to disconnect people from campus Wi-Fi during an exam, especially at a testing center. They'd have to return to the lab and have a TA or someone else monitor and facilitate the rest of their lab, which causes headaches for both students and instructors.

## The Solution
What if we had computers pre-configured with the necessary hardware that students could remotely access? This would eliminate the need to loan hardware and allow the lab to be completed remotely, making it easier for instructors and teaching assistants to administer. Additional security measures could be enforced to ensure students run only certain commands and don't deauthenticate the wrong network. But how do we create such an environment? How do we make it secure for students to access? Introducing ZeroTier and VirtualBox!

The figure below outlines how this environment was configured, and it was completely free of charge. The solution involved using ZeroTier to create a whitelisted private network that students could access via a VPN. I had three virtual machines running on my personal laptop. I also had a USB hub with three network adapters, each associated with a virtual machine. VirtualBox has a feature that allows someone to RDP into the machine, enabling multiple people to view the same session without disconnecting others. My computer was connected to the VPN, and a test student was able to access the VM via RDP, configured with the network adapter. The student remotely completed the lab attached to this GitHub repository, and I supervised their session the entire time. The implications of this proof of concept were astounding to me. This method could be used to create a virtual network for students to access, not just for wireless security, but for various purposes.

![Alt text](/screenshot.png?raw=true "Diagram")
