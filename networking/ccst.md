

# 📘 **Cisco CCST Networking – Complete Cheatsheet**

*Author: Alexandre Leonetti*
*Purpose: Revision notes for Cisco CCST Networking Exam*

---

# 🧱 1. Networking Fundamentals

## **1.1 What is a Network?**

* **Network**: Two or more devices connected to share data
* **Host**: Any device with an IP address
* **Node**: Any device on the network (host, switch, AP, router, etc.)

## **1.2 Types of Networks**

* **LAN** – Local Area Network (home, office)
* **WAN** – Wide Area Network (Internet, ISP backbone)
* **MAN** – Metropolitan Area Network (city-wide)
* **WLAN** – Wireless LAN (Wi-Fi)
* **PAN** – Personal Area Network (Bluetooth, AirDrop)

## **1.3 Network Topologies**

* ⭐ **Star** (most used today)
* **Bus**
* **Ring**
* **Mesh**

---

# 🌐 2. OSI & TCP/IP Models

## **2.1 OSI Model (7 Layers)**

1. **Application** – HTTP, DNS, SMTP
2. **Presentation** – encryption, formatting
3. **Session** – session control
4. **Transport** – TCP/UDP
5. **Network** – IP, routing
6. **Data Link** – MAC addressing, switching
7. **Physical** – cables, signals

### **Mnemonic:**

> **All People Seem To Need Data Processing**

## **2.2 TCP/IP Model (4 Layers)**

1. Application
2. Transport
3. Internet
4. Network Access

---

# 🌍 3. IPv4 Addressing

## **3.1 Basics**

* 32-bit address
* Written as `192.168.1.10`
* Contains **network portion** + **host portion**

## **3.2 IPv4 Classes**

| Class | Range   | Default Mask  | Use Case        |
| ----- | ------- | ------------- | --------------- |
| A     | 0–127   | 255.0.0.0     | Large networks  |
| B     | 128–191 | 255.255.0.0   | Medium networks |
| C     | 192–223 | 255.255.255.0 | Small networks  |

## **3.3 Private IP Blocks**

* **10.0.0.0/8**
* **172.16.0.0 – 172.31.0.0**
* **192.168.0.0/16**

## **3.4 Subnet Mask**

Determines what is **network** vs **host**.

Example:
`255.255.255.0` → `/24` → 256 addresses (254 usable)

## **3.5 CIDR Notation**

* `/24` → 256 addresses
* `/30` → 4 addresses (router links)
* `/16` → 65,536 addresses

## **3.6 DHCP**

Assigns IP settings automatically:

* IP address
* Subnet mask
* Default gateway
* DNS servers

---

# 📡 4. MAC Addresses & ARP

## **4.1 MAC Address**

* 48-bit hardware address
* Unique NIC identifier
* Example: `00:1A:2B:3C:4D:5E`

## **4.2 ARP (Address Resolution Protocol)**

Resolves **IP → MAC** on a LAN.

Example:

> *“Who has 192.168.1.5? Tell 192.168.1.10”*

---

# 🔄 5. Switching (Layer 2)

## **5.1 What Switches Do**

* Forward frames using MAC tables
* Reduce collision domains
* Provide full duplex communication

## **5.2 Collision & Broadcast Domains**

| Device | Collision Domains | Broadcast Domains |
| ------ | ----------------- | ----------------- |
| Hub    | 1                 | 1                 |
| Switch | 1 per port        | 1                 |
| Router | 1 per interface   | 1 per interface   |

## **5.3 VLANs**

Logical segmentation inside a switch:

* **Access ports** → one VLAN
* **Trunk ports** → multiple VLANs
* Reduces broadcast size

---

# 🚦 6. Routing (Layer 3)

## **6.1 What Routers Do**

* Forward packets between networks
* Separate broadcast domains
* Determine best path

## **6.2 Static vs Dynamic Routing**

* **Static** – manually configured
* **Dynamic** – routers learn automatically:

  * **RIP** (hop count)
  * **OSPF** (cost)
  * **EIGRP** (Cisco proprietary)

## **6.3 Default Gateway**

Used to go *outside* the local network.
Example: `192.168.1.1`

---

# 🔐 7. Network Security Basics

## **7.1 CIA Triad**

* **Confidentiality**
* **Integrity**
* **Availability**

## **7.2 Common Threats**

* DDoS
* Malware
* Phishing
* MITM attacks

## **7.3 Firewalls**

Control traffic via rules:

* IP
* Port
* Protocol

## **7.4 ACLs**

Access Control Lists allow/deny traffic.

---

# 📡 8. Wireless Networking

## **8.1 Wi-Fi Standards**

| Standard           | Band      | Max Speed |
| ------------------ | --------- | --------- |
| 802.11n            | 2.4/5 GHz | 600 Mbps  |
| 802.11ac           | 5 GHz     | 1.3 Gbps+ |
| 802.11ax (Wi-Fi 6) | 2.4/5 GHz | 9.6 Gbps  |

## **8.2 Wireless Security**

* **WEP** ❌ outdated
* **WPA**
* **WPA2 (AES)**
* **WPA3** 🔒 best

---

# 🔧 9. Troubleshooting Tools

## **9.1 Common Commands**

* `ping` – test reachability
* `traceroute` / `tracert` – show path
* `ipconfig` / `ifconfig` – interface info
* `arp -a` – ARP table
* `netstat` – connections

## **9.2 Basic Troubleshooting Flow**

1. Identify issue
2. Check physical layer
3. Verify IP configuration
4. Ping local gateway
5. Ping remote host
6. Check DNS
7. Escalate if unresolved

---

# 🧪 10. What the CCST Exam Tests (Concepts)

Cisco tests **concepts**, not memorized facts.

You must know:

* OSI vs TCP/IP layers
* Private vs public IPs
* Subnet sizes
* What switches vs routers do
* VLAN and trunk concepts
* ARP, DHCP, DNS behavior
* Wireless basics
* Reading network topologies
* Troubleshooting steps

If you understand the content above → **you can pass the exam**.

---

# 🏁 Final Advice Before the Exam

* Memorize OSI layers
* Review `/24`, `/30`, `/16` subnets
* Understand MAC vs IP roles
* Know switch vs router separation
* Review wireless security differences
* Practice ping/traceroute logic

---
i generated most of this with AI, but it's handy.