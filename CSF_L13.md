# Cyber Security Fundamentals
### Lecture 13 - Attack
---

### Hats
##### White hat:
Conducts **penetration** testing with the permission of the organisation being attacked. This must be written in a **legal contract** of what is allowed and forbidden. 

##### Black hat:
Breaks into systems without authorisation for direct **malicious intent**.

##### Grey hat:
A grey hat does not have permission, but hacks for the **overall good**. Although motive is very hard to prove at the time of offense in a legal setting. 

---

### Passive vs Active testing

##### Passive:
Testing that involves **looking** for vulnerablities.
> "That door looks like it could be kicked in"

##### Active:
Testing that involves trying to gain entry to vulnerabilities
> "The door can be kicked open, I have tried"

----

### Boxes

**Black box testing**, looks at the *functionality* of the system. **White box testing**, looks at the *internal workings* of the system.

##### White Box Penetration:
Testing where **everyone knows** that a test is being conducted.

##### Black Box Penetration:
Testing where most **people involved are unaware** a test is taking place. This approach is more effective as its tests the whole system, including the people involved (*most security problems are human based*).

---

### Penetration Testing

##### Steps:
1. Reconnaissance
2. Scanning
3. Gaining Access
4. Maintaning Access
5. Covering Tracks

### Step 1: Reconnaissance 

Involves **gathering information** about the target. Most is public information and therefore does not need permissions. The information gathering may be logges and target alerted. 

Two main ways of getting this information.

##### Social Engineering
- Phone calls trying to get information
- Bogus tradespeople
- Assuming second identity etc.

##### Electronic Information Available
- Public IP address
    - location
    - other IPs it communicates with
- Operating System
    - Each has its own weakness
    - Malware can be crafted for specific OS
- Mailing list 
    - For phishing and sear fishing

### Step 2: Scanning

If reconnaissance has found an interesting target. Scanning then focusses on that target and tries to **find out more information**. 

- Network scanning
    - Identifies live hosts
- Port scanning
    - Identifies open ports
- Vulnerability scanning
    - Looks up known vulnerabilities from public databses and sees if any of the identified hosts and ports are available.

### Step 3: Gaining Access

Phishing and Social Engineering **try to gain passwords** so that we can gain access using them. Scanning might have also found a vulnerability for exploitation. 

### Step 4: Maintaining Access
One of the first tasks after breaking in, is trying to make it easier for entry again. **Malware** can be installed ot do this.

##### Trojan horses
**Executables** that can be run on the target machine without being explicitly activated. 
They can:
- Open back door for easy access
- Gather data and send it to another lcoation
- Provide root access (root kit)
- Provide remote access (RAT)

##### Viruses
Similar but are code fragments attached to other programs:
- **Worms** look for other hosts to infect, multiplying
- **Keyloggers** record every keystroke and send it home
- Attackers can download the password file and conduct an offline attack to crack passwords
- Can try **escalet priviledges** and gain admin access

### Step 5: Cover your tracks

You should **manipulate logs** and use **annonymous connections**. 

##### Manipulating logs
Edit the logs and remove any trace of entry into the system and any action taken. **Hide any files that were installed**, add modified programs so that they dont list selected files and processes. Change any dates on new inserted files. 

##### Anonymous Connections
Use **Tor** and **VPN** to hide the original entry point. Conduct your attack somehwere with open WiFi connections (no CCTV though).
> Some sites are set-up as "**honey pots**" designed to attract and gather information on attackers.

