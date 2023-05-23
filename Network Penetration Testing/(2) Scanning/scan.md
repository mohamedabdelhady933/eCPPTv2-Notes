# Scanning Phase

have basic information on our target, we need more detailed data on the devices in the target network. Ports, Protocols and Services help us in identitying the types of applications running on a system and subsequently any potential weaknesses.




### Ports, Protocols and Services

Good refernce for [ Ports, Protocols and Services ](http://www.iana.org/assignments/port-numbers)
___


### Wireshark

tool to capture the network packets.


**Filters**

1-Get only packets of the specific IP

> ip.addr==192.168.x.x


2-Get a src IP packets

> ip.src==192.168.x.x


3-Get a dst IP packets

> ip.dst==192.168.x.x


4-You can filter a specific protocols

> http / icmp / ssh


5-Filter a specific port

> tcp.port==22


6-Filter all SYN packets

> tcp.flags.syn==1


7-You can type more than one filter line

> ip.src=192.168.x.x and/or ip.dst=192.168.x.x

> tcp.flags.syn==1 and/or tcp.flags.ack==1 and/or ip.addr==192.168.x.x


8-Search for a specific word

> tcp contains "word"


___

### Detect Live Hosts and Ports

hosts discovering and port scanning techniques.

**Usage**

1-Scan port 80 with SYN flag (-S / -sS ) 

> hping3 -S -p 80 192.168.x.x


> nmap -sS -p 80 192.168.x.x

2-Get the open ports for a specific range (1-1000) with SYN flag (-S / -sS )

> hping3 -S --scan 1-1000 192.168.x.x

> nmap -sS -p 1-1000 192.168.x.x

3-TCP and UDP scans
<!-- There are number of services that run and commuunicate over UDP (DNS , SNMP , DHCP , netbios-ns , rpcbind ,.....) -->
> nmap -sT -p 80 192.168.x.x

> nmap -sU -p 137 192.168.x.x

4-Perform OS fingerprinting

> nmap -O -v 192.168.x.x

5-Christmas scan is a combination of (FIN, Push , Urgent) flags

> nmap -sX 192.168.x.x 

more info about [ Nmap ](https://nmap.org/book/man-port-scanning-techniques.html)

___

### Nmap NSE 

Nmap Scripts Engine

**Usage**

1-All scripts location 

>/usr/share/nmap/scripts

2-Search for a specific category/script and get more info

> nmap --script-help "smb*" 

> nmap --script-help smb-vuln-cve2009-3103

3-Get Whois information

> nmap --script whois-domain domain.com -sn

4-Get smb OS information 

> nmap --script smb-os-discovery -p 445 192.168.x.x

5-Show smb shares

> nmap smb-enum-shares 192.168.x.x -p 445

6-Run default scripts ( OS , shares , smb information , security authentication , methods supported ,....more)

> nmap --script default 192.168.x.x

___

### Idle Scan 

is one of the most famous techniques used to perform a port scan without sending packets to the target host containing the attacker IP. All it requires is a third party host called zombie

**Flow**

1-Assume That we already know that port 135 on the zombie is open

> hping3 -S -r 192.168.1.5 -p 135

![image](https://user-images.githubusercontent.com/73122852/230792772-67b40cf9-7353-44ab-8d2b-4f8d2167f945.png)

The id=+1 that means the host is not communicating with any machine on the network but us. So our host is a good zombile candidate for our idle scans 

2- Spoof the zombie's IP if the target is open there will be communication between the zombie machine and the target 

> hping3 -a 192.168.1.5 -S 192.168.1.7 -p 23

![image](https://user-images.githubusercontent.com/73122852/230793721-5abae249-6aba-4df9-90f5-4f66867a4801.png)

The id=+2 that means the zombie communicate with 2 hosts (attacker IP & target IP)

___

### Firewall / IDS Evasion

**Usage**

1-Via fragmentation

> nmap -f -sS 192.168.x.x -p 80,21,153,443 -Pn -n --disable-arp-ping

2-Via spoofing IP

> nmap -p 80 -D 192.168.2,ME,192.168.2.2 192.168.2.1

> hping3 -a 192.168.x.122 -S -p 80 192.168.x.x

3-Via generate random decoys

> nmap -D RND:10 192.168.x.x -sS -p 80 -Pn --disable-arp-ping

4- Random IP source

> hping3 --rand-source -S -p 80 192.168.x.x -c 3

5- decrease Data length

> nmap -sS --data-length 10 -p 21 192.168.x.x

6- MAC spoofing

> nmap --spoof-mac apple 192.168.x.x -p 80 -Pn  --disable-arp-ping -n


