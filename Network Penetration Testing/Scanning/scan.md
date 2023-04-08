# Scanning Phase

have basic information on our target, we need more detailed data on the devices in the target network. Ports, Protocols and Services help us in identitying the types of applications running on a system and subsequently any potential weaknesses.




### Ports, Protocols and Services

Good refernce for [ Ports, Protocols and Services ](http://www.iana.org/assignments/port-numbers)



### Wireshark

Great tool to capture the network packets.


**Filters**

1-Get only packets of the specific IP
```
ip.addr==192.168.x.x
```

2-Get a src IP packets
```
ip.src==192.168.x.x
```

3-Get a dst IP packets
```
ip.dst==192.168.x.x
```

4-You can filter a specific protocols
```
http / icmp / ssh
```

5-Filter a specific port
```
tcp.port==22
```

6-Filter all SYN packets
```
tcp.flags.syn==1
```

7-You can type more than one filter line
```
ip.src=192.168.x.x and/or ip.dst=192.168.x.x

tcp.flags.syn==1 and/or tcp.flags.ack==1 and/or ip.addr==192.168.x.x
```

8-Search for a specific word
```
tcp contains "word"
```
