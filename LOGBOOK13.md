# Week #13 (Sniffing and Spoofing)

First we set up the environment:
```
docker-compose build  
docker-compose up -d  
```
## Task 1.1
We identified the correct network interface (br-<network_id>) on the host using the command:
```
ip addr 
 ```
The identified interface was br-f2d5ddfe66df.

We created a new file ```sniffer.py``` :
```
#!/usr/bin/env python3
from scapy.all import *

def print_pkt(pkt):
    pkt.show()

pkt = sniff(iface='br-f2d5ddfe66df', filter='icmp', prn=print_pkt)
````
In the above program, the print_pkt() function will be invoked for each captured packet, displaying detailed information about the packet.

### Task 1.1 (A)

We made the ```sniffer.py``` script executable:
```
chmod a+x sniffer.py
```
The next step was to run the script with root privileges:
```
sudo ./sniffer.py
```

Then run the script without root privileges using the seed account:
```
su seed
sniffer.py
```

When running the script with root privileges, we were able to capture packets. However, running the script without root privileges yielded an error. This is due to the need for elevated privileges to capture network traffic.

### Task 1.1 (B)
We applied different filters to observe how they affect the packet capture:

#### Capture only ICMP packets
```
pkt = sniff(iface='br-f2d5ddfe66df', filter='icmp', prn=print_pkt)

```
![Image 1](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task1_LOGBOOK13_1.png)

#### Capture TCP packets from a specific IP and port
```
pkt = sniff(iface='br-f2d5ddfe66df', filter='tcp and src host 10.9.0.5 and dst port 23', prn=print_pkt)
```
![Image 2](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task1_LOGBOOK13_2.png)

#### Capture packets from/to a specific subnet
```
pkt = sniff(iface='br-f2d5ddfe66df', filter='net 128.230.0.0/16', prn=print_pkt)
```
![Image 3](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task1_LOGBOOK13_3.png)


## Task 1.2
We created a new file ```spoof_icmp.py``` :

```
#!/usr/bin/env python3
from scapy.all import *

a = IP()
a.src = "10.9.0.5" 
a.dst = "10.9.0.6"
b = ICMP()

p = a/b

ls(p)

send(p)
```


### IP Header
```a.src = "10.9.0.5"``` : Sets a fake source IP.
a.dst = "10.9.0.6": Defines the destination IP.

### ICMP Header
```b = ICMP()``` : Creates an ICMP Echo Request packet.

### Packet Assembly
```p = a/b``` : Combines the IP and ICMP headers into one packet.

### Packet Verification
```ls(p)``` : Displays the packet fields and values for debugging.

### Send Packet
``` send(p)``` : Sends the spoofed packet to the target (10.9.0.6).


The next step was to run the script:

![Image 4](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task2_LOGBOOK13_1.png)

We used Wireshark to capture the packet transmission:

![Image 5](https://git.fe.up.pt/fsi/fsi2425/logs/l05g06/-/raw/main/Images/Task2_LOGBOOK13_2.png)

The script demonstrates how to create and send spoofed ICMP packets to test network behavior.

