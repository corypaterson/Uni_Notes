# Cyber Security Fundamentals
### Lecture 9 - Web Security
---

### Problems Specific to the Web

The **underlying software** is very comples and may hide potential security flaws. There are many new systems that may have been installed correctly but are vulnerabel to attack. 

Many casual and untrained users manage web based servers. **Web servers** can be exploited as portals into the entire corporate network.

---

### Network Security

Networks have the following layers (top-down):

1. **Sockets**: a stream of bytes between two applications on different machines.
2. **TCP**: reliable ordered transmission of a series of packets between two machines independant of individual packet route.
3. **UPD**: Like IP but with ports.
4. **IP**: A single packet is transfered between two machines independant of route.
5. **Ethernet**: A single packet is transfered using a fixed connection between two machines.

Security is normally implemented in **IPsec** - IP Security, IP packets are encrypted, **SSL** - Secure Sockets Layer (Trasport Layer Security). 

---

### IP Security

Security can be implemented at the IP level. 

Benefits:

- It is transparent to the application software in higher levels. Users wont need to be trained in security matters
- It can be implemented in a firewall, internal traffic is not encrypted and so does not incurr the performance penalties.
- It can be implemented on an individual basis (offsite workers).
- Can be used in a subnet for sensitive applications

### Transport vs Tunnel (Modes of Operation)

An IP packet has two parts:
- **payload** - the data being carries
- **header** - origin, destination and other information.

**Transport Mode** - protection is provided for the IP payload but not the IP header. 

**Tunnel Mode** 
- Protection is provided for the entire packet
- It is the payload of an outer IP packet, using the **transport** mode.
- It is useful for transport from one firewall to another, hiding traffic analysis.

---

### Transport Layer Security

A socket connects two applications with a 'pipe' across the internet from one computer to another.

Data can be transmitted in both directions, it arrives at the destination in the same order that it was put into the pipe.

Initiation takes place at the session network layer, while communications are in the presentation layer. 

### Handshake Protocol

Client **C** and Server **S**. 

1. C->S: Asks for a secure connection, and shows which algorithms the client supports.
2. S->C: Tell which algorithms the client should use, and gives *public key certificate*
3. C->S: Returns an Unpredicatble Number, encrypted with the servers public key

The certificate contains the servers name and public key, it is encrypted with the secret key of a CA, the client should already have the public key of this CA.

Both the client and the server use UN to generate session keys for bulk encryption of data. If the server is genuine, then it knows the server sectret key and can decrypt the UN.

---

### Resumed Sessions

If a connection is likely to be used for several sessions, then the server can send a session ID or a session ticket during the initial handshake. 

The client is given a session ID, then when the session is resumed, they just present the ID. A session ticket contains the client state in an encrypted form. 

AES session keys, once broken, can be used to gain access to all future and past communications. The best way to ensure this doesnt happen is to use **ephemeral D-H** to calculate the session keys where a **new random key** is generated for each session.

### Man in the middle attack (classic)

This can be prevented by using *public key certificates* (certfifying authority must be secure). If the CA is comprimised, the attacker can forge their own certificates. 

The *weakness* of a MiM attack is that it only takes place between two parties: the **client** and the **sever**. 

This then provides scope for preventing such an attack. We can use:

- Certificate Pinning
- Certificate Perspectives

---

### Certficate Pinning

- Obtain a *trusted* version of the **server certificate** and compare it with the one provided each session
- Client will usually take the certificate obtained on the first visit as genuine.
- If the certificate is then different, a **MiM** has taken place.


### Certificate Perspectives

- Use a third party, a notary, to obtain a server certificate from a different IP address
- The MiM attack will unlikely be occuring on both connections
- If two certificates are different, then MiM is taking place.
- This can be done multiple times with different notaries for added security

---

### Denial of Service (DOS) Attacks

Used to exploit system weaknesses. 

1. **Ping of death**, using the network enquiry *ping* command.
2. **Teardrop attack**, sends mangled IP packets which exploit bugs in code, to reassemble them.
3. **Smurf attack**, sends a packet to the broadcast address and the machine then amplifies it by sending it to everyone else (exploits poorly configured networks)

### DDOS

Distributed Denial Of Service attacks.

A vast number of attackers overwhelm a victim and either:
- Exhaust system resources, or
- Exhaust bandwith

Must have assembled a botnet of comprimised PC's, which all respond to the attack.

---

### Direct Attacks

The most common **direct attack** is **SYN Flooding**. This uses a fake **From address**. 

SYN asks for a connection:
- The victim responds with **SYN-ACK** and waits with a half open connection
- There will never be a reply because the **From address** is fake.
- The vicitm will usually wait and send several SYN-ACK packets before giving up.
- The goal is to open as many half connections as possible and exchaust resources

The only preventative method is for the two parties to exhange **cookies** (a relatively cheap operation), before starting to open a connection.

### Relflector Attacks

**Internal internet nodes** (routers, servers etc) are used to launch the attack. Packets requiring a response are sent to the routers with a **forged From address**.

Routers then send a legitimate response to the victim, which overwhelms the vicitm with normal packets. This is to **exhaust bandwidth**.

>These packets are usually SYN-ACK packets, which can be recognised as bogus however.

### Detect and Filter

When a victim detects an attack:

- They make a request that the attacking soucre providers are filtered out by the **ISP**.
- There will be false positives and false negatives.
- Normal packet survivial rate it quite low however.

**IP Traceback** is a good idea that doesnt always work because firewals stop it, reflector attacks come from a legitimate source. 

**IP hopping** and **proxies** can defend properly against a DDOS attack.







