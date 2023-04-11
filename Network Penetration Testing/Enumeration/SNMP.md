# SNMP (Simple Network Management Protocol)

it is used for exchanging management information between network devices (printers,switches,servers,....).


* SNMP commands types
  - Read
    - The read command is used to monitor devices.
  - Write
    - The write command is used to configure devices and change device settings.
  - Trap
    - The trap command is used to "trap” events from the device and report them back to the monitoring system.
  - Traversal Operations
    - The Traversal operations are used to determine what variables a certain device supports.

---

* SNMP attacks
  - Flooding
    - Flooding: DOS attack which involves spoofing an SNMP agent and flooding the SNMP trap management with tens of thousands of SNMP traps, varying in size from 50 bytes to 32 kilobytes, until the SNMP management trap is unable to function properly.
  - Community
    - Using Default community strings to gain privileged access to systems
  - Brute force
    - Brute force: Using a tool to guess the community strings used on asystem to achieve elevated privileges. 

---

* SNMP Enumeration

Snmpwalk uses SNMP GETNEXT requests to query a network entity for a tree of information.

> snmpwalk -v 2c -c public 192.168.x.x 

> nmap -sU -p 161 --script snmp-win32-services 192.168.x.x          (get all services)

> nmap -sU -p 161 --script snmp-brute 192.168.x.x                   (get community string)

> nmap -sU -p 161 --script snmp-win32-users 192.168.x.x              (get users)



