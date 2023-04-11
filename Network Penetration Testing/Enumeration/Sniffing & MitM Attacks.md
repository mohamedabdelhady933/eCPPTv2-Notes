# Sniffing & MitM Attacks

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























