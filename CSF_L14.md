# Cyber Security Fundamentals
### Lecture 14 - Digital Forensics
---

##### Dead Forensics:
What happened in the **past** - Contents of the hard drive, USB sticks, and other external memory.

##### Live Forensics:
What is happening **at the moment** - Contents of RAM, network traffic etc.

----

### Steps in a Computer Forensics Investigation

1. Seizure 
2. Acquisition
3. Analysis
    a. Physical searching
    b. Using a whitelist
    c. Registry examination
    d. Timeline reconstruction
4. Reporting

### Step 1 - Seizure

If a system is powered on, decide whether to shut it down or conduct a live investigation. 
- **Check for active traffic**, if router lights are flashing then someone might be erasing files remotely. 
- Get the time from the Bios
- Label and register all equipment found, document all connections between components before disconnecting. 
- Remove hard drives and place in anti-static bags
- Photograph all activity

### Step 2 - Acquisition
- Copy the hard drive making sure that the integrity of the contents can be proved
- Create a message digest of the entire drive conents
- Create an exact copy of the drive, making sure that writing is blocked
- Check that the message digest of the copy is the same
- Create a copy of the copy to do work with
    - If this copy is messed up, can still revert back to original
- Log the initial hard drive as evidence

### Step 3 - Analysis
##### Physical Searching
Searching for the copy of the evidence and **recovering deleted files**. Useful information includes:
- List of users
- Emails
- Documents
- Pictures

##### Registry Examination

Windows OS store configuration infomration in the registry. Entries can be viewed and changed using **regedit**. Linux systems store config info in many different places: 
- Many text files in /etc
- Many hidden (.) files in user's home directories

##### Timeline Reconstruction
Involves examining logs to determine when various things happened. **File create and modify times**. Depends on an accurate system clock.

##### Step 4: Reporting
The final report should present the finding in a form suitable for a court. If it results in a court case then the evidence will be presented to the defence for the court appearance. The defence will conduct their own forensic examination. 

---

### Netork Forensics

**Analysing packets** as they flow around the network, you can see all the packets visible to a computer's network controller. **Network taps** can capture lots of info, but network sniffing is *illegal*. 

---
### Legislation 
##### Computer Misuse Act 1990

1. Unauthorised access to computer material
    - Must be knowledge that the access is unauthorised
2. Unauthorised access with intent to commit or facilitate commission of further offensives
3. Unauthorised access with intent to impair the operation of a computer.
    - Includes preventing access (DOS attack)
4. Attacks on critical infrastructure
5. Making or suppling malware

##### RIPA

Regulation of Investigatory Powers Act

- Unlawful interception of communications
- Hacking into a network

##### Data Protection Act
- Obtaining or disclosing personal data
- Procuring the disclosure of personal data
- Selling or offering to sell personal

##### Copyright, Designs and Patents Act

- Provides protection to digital works
- COvers devices designed to circumvent copy-protection of works in electronic form
- Fradulent reception of transmissions

