# Cyber Security Fundamentals
### Lecture 11 - Network Security
---

### Network Layers:
- Data Link Layer
    - Medium Access Control (MAC) addresses
    - Cable or WiFi
- Network Layer
    - Internet Protocol (IP) addresses
    - Address Resolution Protocol (ARP)
- Transport Layer
    - Ports
- Application Layer
    - Domain Name Server (DNS)

---
### Data Link Layer: Cable

Connects individual devices typically via ethernet.

- Each device has a MAC address for its Network Interface Controller
    - 48 bits long (6 hex values)
    - First 24 bits:
        - Organisationally unique identifier (OUI)
    - Second 24 bits:
        - Network Interface Controller (NIC) specific

Communications via ethernet frame (packet) contains:
- Destination MAC address
- Source MAC address
- Payload
- Checksum

### Data Link Layer: WiFi

Individual devices connected by WiFi: IEEE 802.11

There are additional frame types:
- Management
- Control
- Data

The MAC address of the Access Point (AP) is included in the frame header.

---

### Network Layer

IP packets contain:

- Destination Address
- Source address
- Payload
- Checksum

##### Address Resolution Protocol (ARP)

A device has the IP address of the packet destination and wants to find the MAC address of the device that has this IP address.

Example:

- CA:FE:CO:FF:EE:00 has received the packet with IP address 192.168.0.1 and wants to know who to send it to.
- Who has 192.168.0.1 : sent to FF:FF:FF:FF:FF:FF (everyone)
- Answer: 192.168.0.1 is at FE:ED:DE:AD:BE:EF : sent to
CA:FE:CO:FF:EE:00

---

### Transport Layer

**Sits on top of IP** and connects applications. Each IP address has 64k ports, addressed by 16-bit integers. Each appliaction connects to a **specific port**. 

### TCP/UDP

- UDP packet transmission
    - Delivery not guarunteed
- TCP a sequence of packets
    - Guaranteed delivery
    - Will be delivered in order
- Both connect to ports at an IP address.

---

### Application Layer

- Domain Name Server (DNS)
- Connects text network addresses to IP addresses.

### Types of Attack

- Switch Downgrading: ARP or MAC flooding.
- ARP Poisoning

### Switch Downgrading: MAC flooding

A switch will:

- Recieve a MAC frame
- Look up the IP and port number to find the destination MAC
- Forward the frame

The switch maintains an internal table of IP addresses, port numbers and MAC addresses of the devices associated devices. The table is **built dynamically** by observng traffic, but has **finite size**.

When the table is full, some destinations will not be in the table. These frames will be broadcast rather than sent to the destination.

##### The attack:

- The attacker sends lots of frames with different addresses
- This will fill up the table, forcing the switch to start broadcasting frames.
- The implications
    - The traffic can be monitored since its being broadcast
    - The increased traffic reduces performance

### ARP Poisoning

The aim of the attack is not to fill up the table but **insert incorrect values**. 

When a machine reveievs an ethernet frame, it will ask around to find out who to send it to.

The attacker will send a large number of responses saying that it can forward the packet, hoping that it will be chosen. 

The aim is for all traffic to be **routed via the attacker**, who can then forward it onwards (MiM Attack).

### DNS Poisoning

The '/host' file on the local computer is the first point of contact in the Domain Name Server process.

- If the name is not there then the process searches further afield.
- Uses an ad blocker by redirecting add serving and monitoring IP addresses to 127.0.0.1 (local host).
- Code trying to refer to these addresses will be sent to the host machine, which does not have them (they will not be displayed).
- This approach can also be used for censorship.


---

### Firewalls

Firewalls are used to monitor **incoming and outgoing network signals**, looking for threats. They use rules to decide if traffic is allowed to pass. They are usually placed on gateway machines to control access to an internal network.

---

### Proxy Service

- All connections to the internt are routed through the firewall
- Checking for allowed access is centralised
- Common content is only cached once
- Logs are all in one place for each of monitoring

---

### Packet Filtering

Packets are check against a set of rules to determine if a packet should pass.

Check on the requested service (using port number and machine). **Only some ports are allowed**.

Check the packet source. Black and white lists, for banned and allowed sites.

Deep packet inspection - Check the content of the website. 

---

### Stateful Inspection

Just check key parts of the packet and apply a matching algorithm. The administrator can define the rules. Rules can be use past experience from previous connections to the site, as well as previous packets of info.

---

### Intrusion Detection

Network traffic, rather than single packets, is examined to see if an attack is underway. 

It could be signature based:
- Check with a databse of known attacks
- Recognise them by their 'signature'
- Will not recognise a new attack

Anomaly Detection:

- AI, typically machine learning, looks for non-standard situations and tries to classify them as an attack or just normal variation. 

A **sysadmin** is always contacted to deal with the threat.

### Intrusion Prevention

Will detect an intrusion as before. In this case the firewall can take action without waiting for a sysadmin to initiate it.

---

### Vitrual Private Network

Uses **tunnel mode** IPSEC. 

The user's computer will run the VPN application, which puts the whole of the IP packet, including the header, as an encrypted payload of an outer packet.

The **outer packet** is delivered to a VPN provider's computer (e.g, gateway to a compnay network, computer in another country).

Results travel in reverse, and looks to network providers like you are using the VPN provider's computer.

---




