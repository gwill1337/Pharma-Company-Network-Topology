# Pharma Company Network Topology
## About
This project represents a network topology for a pharmaceutical company with two branches and one pharmacy.

In this topology I configured 2 branches of company and one pharmacy. Between branches I configured IPSec for secure connection. Routing is implemented using OSPF and static routing with the ISP. Details on security, routing, and infrastructure are provided below.

## Security
On every access interface on switches is configured with:
* **Port Security**
* **Nonegotiate**
* **STP Portfast**
* **BPDU Guard**
* **CDP Disable**

The main branch also includes a Cisco ASA firewall.
### Details:

1. **Port Security** - disconnect device if limit of connection was exceeded. This prevents unauthorized access to the network if someone connects an unknown device.
2. **Nonegotiate** - disables DTP on access ports to prevent an attacker from forcing a trunk mode and gaining access to all VLANs.
3. **Portfast** - speeds up the connection process for end devices (not used on switches or routers).
4. **BPDU Guard** - prevents potential network loops by disabling a port that receives BPDUs unexpectedly.
5. **CDP Disable** - CDP can expose device information that may be exploited for ARP spoofing or network mapping, so it’s disabled for security.

## Main branch
### Topology
### Devices:
* 1 x Cisco 4331 Router 
* 1 x Layer 3 Switch
* 1 x Cisco ASA Firewall
* 4 x Layer 2 Switches
* 10 x Servers
* PCs

**Router:** Configured with IPSec, NAT and OSPF.  
**L3 Switch:** Configured with VTP, Inter-VLAN routing (Vlans 10-40), ACLs per department (except servers), and OSPF.  
**Cisco ASA:** Used for ACLs and firewall functionality (currently allows all IPs for testing).



### Servers

Server      |     Function
---------   |    :----------:
ERP         | Simulated ERP (WEB + FTP)
DHCP        | DHCP for internal network
NTP         | Time synchronization for all branches
FTP         | Data storage
TFTP        | Backup storage
SYSLOG      | Log collection
DNS         | Resolves company domain + forwards to Google DNS (8.8.8.8)
WEB         | Company website
AAA         | Authentication (TACACS+)
LAB-FTP     | Local FTP for laboratory

## Second branch
### Topology
### Devices:
* 1 x Cisco 4331 Router 
* 1 x Layer 3 Switch
* 4 x Layer 2 Switches
* 4 x Servers
* 1 x Wireless Router
* 1 x Access Point
* 1 x Tablet (Cash Register)
* PCs

**Router:** Configured with IPSec, NAT, DHCP, and OSPF.  
**L3 Switch:** Configured with VTP, VLAN routing (VLANs 10–50), ACLs per department (except servers), and OSPF.  
Branch also includes a pharmacy with a wireless router as an access point.



### Servers

Server      |     Function
---------   |    :----------:
TFTP        | Backups
DNS         | Local + external name resolution
SYSLOG      | Logging
FTP         | Data storage


## Pharmacy
### Topology
### Devices:
* 1 x Cisco 2911 Router 
* 1 x Layer 2 Switch
* 3 X PCs
* 1 x Wireless Router
* 1 x Access Point
* 1 x Tablet (Cash Register)

**Router:** Configured with NAT, DHCP, and OSPF.  
**L3 Switch:** CVLANs 10 (Main), 50 (WiFi).

## About ISP
The provider side uses MetroEthernet with fiber optics and EtherChannel for link aggregation.  
The ISP Router performs routing with OSPF and includes its own DNS server (8.8.8.8).
