
## CaseStudy: DNS-DHCP-HTTP-CONFIGURATION

# Name: HARSSHITHA LAKSHMANAN
# Reg No:212223230075

## INTRODUCTION:

*    Computer networks allow multiple devices to communicate and share information efficiently. In this experiment, four different LAN networks (192.168.10.0/24, 192.168.11.0/24, 192.168.20.0/24 and 192.168.21.0/24) are interconnected using routers, switches, and PCs.
The purpose of this practical task is to configure the PCs, switches, and routers so that devices across different networks can communicate with each other using proper IP addressing and routing.

*  This experiment also verifies whether the configured network supports successful end-to-end connectivity using the ping command.

## NETWORK DIAGRAM:
<img width="1121" height="695" alt="image" src="https://github.com/user-attachments/assets/fbfd710b-b38e-4a94-93d1-ec11ff484eb2" />


## DESCRIPTION:
Network Layout Recap
Main Router (R0): Serial links to Branch Router 1 (R1) & Branch Router 2 (R2)

R0 connects to R1 (Serial0/0/0)

R0 connects to R2 (Serial0/0/1)

Branch Router 1 (R1):

GE0/0 → Switch 1 (192.168.10.0/24, PCs .10-.14, GW .1)

GE0/1 → Switch 2 (192.168.11.0/24, PCs .10-.14, GW .1)

Branch Router 2 (R2):

GE0/0 → Switch 3 (192.168.20.0/24, PCs .10-.14, GW .1)

GE0/1 → Switch 4 (192.168.21.0/24, PCs .10-.14, GW .1)

## PROCEDURE:
# Step 1 — Configure PC IP Addresses:

PC Assignments
| Switch | PC IPs        | Subnet        | Default Gateway |
| ------ | ------------- | ------------- | --------------- |
| 1      | 192.168.10.10 | 255.255.255.0 | 192.168.10.1    |
|        | 192.168.10.11 | 255.255.255.0 | 192.168.10.1    |
|        | 192.168.10.12 | 255.255.255.0 | 192.168.10.1    |
|        | 192.168.10.13 | 255.255.255.0 | 192.168.10.1    |
|        | 192.168.10.14 | 255.255.255.0 | 192.168.10.1    |
| 2      | 192.168.11.10 | 255.255.255.0 | 192.168.11.1    |
|        | 192.168.11.11 | 255.255.255.0 | 192.168.11.1    |
|        | …             | …             | …               |
| 3      | 192.168.20.10 | 255.255.255.0 | 192.168.20.1    |
|        | …             | …             | …               |
| 4      | 192.168.21.10 | 255.255.255.0 | 192.168.21.1    |
|        | …             | …             | …               |

# Step 2 — Configure Router Interfaces:
* Main Router
```
enable
configure terminal
interface serial0/0/0
ip address 10.1.1.1 255.255.255.252
clock rate 64000
no shutdown
exit
interface serial0/0/1
ip address 10.1.2.1 255.255.255.252
clock rate 64000
no shutdown
exit
ip route 192.168.10.0 255.255.255.0 10.1.1.2
ip route 192.168.11.0 255.255.255.0 10.1.1.2
ip route 192.168.20.0 255.255.255.0 10.1.2.2
ip route 192.168.21.0 255.255.255.0 10.1.2.2
end

```

* Branch Router1
```
enable
configure terminal
interface serial0/0/0
ip address 10.1.1.2 255.255.255.252
no shutdown
exit
interface gigabitethernet0/0
ip address 192.168.10.1 255.255.255.0
no shutdown
exit
interface gigabitethernet0/1
ip address 192.168.11.1 255.255.255.0
no shutdown
exit
ip route 192.168.20.0 255.255.255.0 10.1.1.1
ip route 192.168.21.0 255.255.255.0 10.1.1.1
end

```
* Branch Router2
```
enable
configure terminal
interface serial0/0/0
ip address 10.1.2.2 255.255.255.252
no shutdown
exit
interface gigabitethernet0/0
ip address 192.168.20.1 255.255.255.0
no shutdown
exit
interface gigabitethernet0/1
ip address 192.168.21.1 255.255.255.0
no shutdown
exit
ip route 192.168.10.0 255.255.255.0 10.1.2.1
ip route 192.168.11.0 255.255.255.0 10.1.2.1
end

```

# Step 3 — Verify Using PING:

* From PC0 → PC17
```
 C:\>ping 192.168.21.12

Pinging 192.168.21.12 with 32 bytes of data:

Request timed out.
Reply from 192.168.21.12: bytes=32 time=21ms TTL=125
Reply from 192.168.21.12: bytes=32 time=2ms TTL=125
Reply from 192.168.21.12: bytes=32 time=19ms TTL=125

Ping statistics for 192.168.21.12:
    Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
Approximate round trip times in milli-seconds:
    Minimum = 2ms, Maximum = 21ms, Average = 14ms
```


All PCs across Four Switches should successfully communicate.

## OUTPUT:

* All PC IP-confrations:

<img width="780" height="545" alt="image" src="https://github.com/user-attachments/assets/bb164ca0-f829-4fc3-9538-38894aca96c2" />

<img width="756" height="564" alt="image" src="https://github.com/user-attachments/assets/b42dea70-aef8-49d3-9eaf-10fde370a2ef" />

* All  successful ping connections:

<img width="681" height="244" alt="image" src="https://github.com/user-attachments/assets/43171663-dd54-4172-a304-cf62d2276369" />

* IP interface brief on routers

MAIN ROUTER
  
<img width="810" height="141" alt="image" src="https://github.com/user-attachments/assets/fd99bec0-33be-4c83-9213-9eff0787744b" />

BRANCH ROUTER 1
  
<img width="723" height="134" alt="image" src="https://github.com/user-attachments/assets/95a01ddf-4017-4706-93e8-e816eef2615a" />

BRANCH ROUTER 2
  
<img width="738" height="118" alt="image" src="https://github.com/user-attachments/assets/cf9e7660-7254-41ce-8457-8c8d926f46af" />



## RESULT:

* The network was successfully configured with four LAN segments connected through routers using static routing. All PCs received valid IPv4 addresses, and routing ensured cross-network communication.

* The ping results confirmed successful connectivity between all devices in LAN1, LAN2, and LAN3. This shows that the IP addressing, router configuration, and static routing were implemented correctly.
