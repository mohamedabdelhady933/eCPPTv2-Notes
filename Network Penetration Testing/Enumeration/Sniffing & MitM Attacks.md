# Sniffing 

is a network layer attack consisting of capturing packets transmitted by other computers. having these packets will not only allow us to read the data, but also search for sensitive information like
passwords, session tokens, or various types of confidential information.

* Passive sniffing

attacks are performed by just “watching” packets on a network in order to gather sensitive information such as userids, passwords, and other sensitive information.

---

* Active sniffing

is performed by actively performing (malicious) operations (MAC flooding or ARP poisoning) on the network. This means that we will inject packets on the
network in order to redirect the traffic.

---

* Passive sniffing techniques
  - MAC Flooding
    - MAC flooding is meant to stress the switch and fill its CAM table. A CAM table keeps all the info required to forward frames to the correct port
    - When the space in the CAM is filled with fake MAC addresses, the switch cannot learn new MAC addresses. The only way to keep the network alive is to forward the frames meant to be delivered to the unknown MAC address on all the ports of the switch, thus making it fail open, or act like a Hub. 
  
* Passive sniffing techniques  
  - ARP Poisoning
    - is probably thestealthiest among the Active sniffing techniques.It does not need to bring down switch functionalities,instead it exploits the concept of traffic redirection.
    - By exploiting the network via ARP poisoning, the attacker is able to redirect the traffic of the selected victims to a specific machine (usually the attacker's machine). Doing this will enable the attacker to not only monitor, but also modify the traffic.


---

* List summarizes when ARP is used
  - A host desires to send a packet to another host in the same
network

  - A host desires to reach another host beyond his local
network and needs the gateway hardware address

  - A router needs to forward a packet for one host through
another router

  - A router needs to forward a packet to the destination host
on the same network

---

* ARP Poisoning ways
 - Host Poisoning
   - In the first scenario the attacker will create a Man in the Middle configuration between two hosts, transferring data between them.
   - All the traffic from first PC to Second PC and from second PC to first PC will pass through attacker PC. Attacker PC must be able to forward the packets quickly to keep the system administrator from suspecting anything.
   
 - Gateway Poisoning
   - The second scenario is one-way: the machine that is going to sniff traffic in the network will send Gratuitous ARP replys to some or all the hosts in a network, announcing his MAC address as the MAC address of the default gateway for the network.


---

* Sniffing Tools
  - dsniff 
    - The dsniff suite has a collection of tools for active/passive sniffing, MITM attacks and can also monitor the network for data such as passwords, emails, files and much more.
  - Wireshark
  - Tcpdump

---

* Flow

1- Show the interfaces

> tcpdump -D

2- sniff (eth1)

> tcpdump -i eth1

3- Sniff Web for a specific host

> tcpdump -i eth1 host domain.com

4- Filter traffic for a specific source and distination

> tcpdump -i eth1 src 192.168.x.x and dst 192.168.x2.x2

---

# MITM Attacks

![image](https://user-images.githubusercontent.com/73122852/231283265-50246f25-a3a2-46e6-be16-b9b6a5f69860.png)

As you see attacker is able to read , modify the packets transmitted between two peers.





* DHCP Spoofing

DHCP is a service usually running on routers to dynamically assign or revoke |IP address to new hosts on the network. The protocol is based on the UDP protocol and consists of an exchange of messages that are mostly sent in broadcast and are visible to the entire broadcast domain.

DHCP clients choose the best offer according to the lease time attribute in the DHCP offer: the longer the better.This packet is used to designate a winner between all the DHCP servers.











