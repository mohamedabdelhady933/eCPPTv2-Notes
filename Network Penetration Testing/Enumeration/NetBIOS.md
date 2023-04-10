
# NetBIOS (Network Basic Input Output System) 

is the service that allows Windows Systems to share files, folders and printers among machines on a LAN.


* Flow

PC's on a NetBIOS LAN communicate either by establishing a session or by using datagrams. To to This , NetBIOS uses the following TCP and UDP Ports.
  * UDP 137 for name services
  * UDP 138 for datagram services
  * TCP 139 for session services

---
* Name service

has the same purpose of a DNS record, it translates and maps a NetBIOS name to an IP (16-byte).
[NetBIOS Reference](https://technet.microsoft.com/en-us/library/cc738412(v=ws.10).aspx)

---

* Datagram Service 

The datagram service allows the sending and receiving of the datagram messages to and from:
  * a specific NetBIOS name
  * broadcast the datagram to all NetBIOS names

---

* Session service

The NetBIOS Session Service (NBSS) is the most commonly known of the NetBIOS services. It allows two names to establish a connection in order to exchange data.

---

* Server Message Block (SMB)

SMB lets you shares files , disks, directories, printers.

---

* How to enum NetBIOS

1-Gather information about target

> nbtstat -A 192.168.x.x

2-list domains, computers and resources shared by a computer in the network. 

> smbclient -L 192.168.x.x

> smbclient //192.168.x.x/folder

---

* Null Session

is the one of the oldest and most known attacks performed on Windows 2000 and Windows NT environments. Thanks to this weakness, malicious users are able to establish a connection to the victim in order to
gather information such as shares, users, groups, registry keys and much more.

Null sessions rely on Common Internet File System (CIFS) and Server Message Block (SMB) API, that return information even to an unauthenticated user.

> net use \\192.168.x.x\IPC$ "" /u:""

also using smbclient .

---

* Enum4linux

basically a wrapper around rpcclient , net , nmblookup and smbclient. That can gather (Target information , Workgroup/domain , Share Enum , Password Policy , Groups ,Domain SID , Users , Printer Info)

> enum4linux 192.168.x.x

---

* Rpcclient

a tool that can execute Microsoft RPC (Remote Procedure Call) functionalities.

> rpcclient -N -U "" 192.168.x.x

Then Use enumdomusers to list all users.

![image](https://user-images.githubusercontent.com/73122852/230804850-70ed025e-9a90-49e3-b352-a14f1fff68f2.png)









SNMP (Simple Network Management Protocol) : is a protocol used to both gather information and configure network devices (printers,switches,servers,....).

