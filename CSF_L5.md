# Cyber Security Fundementals
### Lecture 5 - User Authentication
---

### Passwords

A **username** and **password** is the standard way for protecting a computer. The computer does not store the passwords, just the *result* of a **one way function** operating on the password.

When a user logs on, the password is entered and the encrypted version of the entered password is compared with the value stored in the database.

 > **Theoretically** this means if the password file is stolen, it is not an issue (UNIX made the files publically available in early versions). However if password is plain English - weak to **brute force attack**.
 
### Dictionary Attacks
(Form of Brute Force Attack)

This is an **offline attack** and is used on a copy of a machines **password file**:

- A *Dictionary* of possible words is constructed and the corresponding encrypted passwords are calculated.
- They are compared with the password file, and any matches indicated a comprimised password.
- This form of attack costs just as much for one password as it does for a large number:
    - If there are 1000 passwords, typically 30% of them can be obtained.
---

### Salt

A salt value (random string) is added to a password before encryption. 

Since all salt values for all passwords in a password file are **individual**, a dictionary attack cannot be run. As it would have to be run for each individual salt value on each password. 

This **does not** make it harder to crack a single password, bnut it prevents a large batch of passwords being cracked in one go.

### Pass Phrases

Generating extra-random passwords will foil a dictionary attack, but the passwords are **hard to remember**.

If the user chooses a very long **pass phrase**, this is then fed into the function - generating a very long password for the password file (harder to crack). 

Rule of thumb: **one letter** in the pass phrase will generate **one bit** of the password for the file.

---

### Remote Authentication

If a **client computer** wishes to log into another server connected to the client:

- Could transmit the password from the client to the server and **let the server authenticate**.
    - Dangerous, as network is insecure
- **The client** could **authenticate the password** and then connect to the server.
    - Dangerous, as server must trust the remote client computer.

The best way to perform this is:

- The user must prove identity to each server. Each server must prove identity to each client.
---
## Kerberos

Kerberos is a **trusted third-party** authentication product used by UNIX and Windows. Providing secure network authentication, allowing different services on the network.

Kerberos provides three levels of protection (Single key encryption) :
1. Authentication at the **start** of a network connection.
2. Authentication of **each message** and
3. **encryption** of each message.
 
##### Actors for Kerberos

- **User (U)**
- **Client (C )** machine, interacts with user
- **Sever (S)** machine, provides a service
- **Authenticator (A)**, authenticates users
- **Ticket granting Service (T)**


##### A Basic Kerberos Protocol
In the following protocol, **IP** is a network address, **P** is a password and **K** is a Key.
        
    C->A: cID, cP, sID
    A->C: Ticket = sK[cID, cIP, sID]
    (encrypted with sK)
    C->S: cID, Ticket

Here:
- Client requests the user's password (cP) and the service required (sID) and sends to **A**
- **A** checks for correct password, and user has permissions for **S**. If OK:
    - **A** sends ticket to **C**
- The ticket is encrypted with sK, which can only be opened by **S**.
- **C** sends ticket to **S**
- **S** checks the correct user is calling from the correct IP address, and has correct ticket for correct server (itself).

Problems:

- The password is sent with no encryption
- The user must enter a password every time a service is used.

These are solved by:

- Creating a **user key (uK)**
    -  both **C** and **A** know the user's password and can generate this key. Then can communicate securely
-  Second problem is solved by creating a **Ticket Granting Service (T)**
    - User gets a ticket for **T** when they log in.
    - **T** will issue tickets for different **S** when required.


##### Better Protocol:

When user logs in:

        C -> A: cID
        A -> C: uK[tTicket]

First use of each new service:

        C -> T: cID, sID, tTicket
        T -> C: sTicket

Each time a service is used:
        
        C -> S: cID, sTicket
    
Ticket for Ticket Granting Service **T**:
- tK[cID, cIP, tID, Timestamp]

Ticket for using a service **S**:
- sK[cID, cIP, sID, Timestamp]

Here:
- The first ticket is encrypted with user's key **uK**, the user is prompted for a password (**U** and **A** know this).
    - Key is generated from the password and unlocks the tTicket
- Client keeps tTicket and uses it whenever a new service is requested
- The client keeps all other tickets to be used whenever each service is used
- Timestamps are needed to prevent **replay attacks**.


Problems:

1. If the lifetime of a **timestamp is too short** then the user has to continually type in his password to create a new ticket when the old one expires
2. If the lifetime of a **timestamp is too long** the system is vulnerable to a **replay attack**
    -  A different user session on the same client machine can use a ticket that has not yet expired to access a service
    -  Thus **T** and **S** must be able to prove that the person using a Ticket is the person issued with that Ticket.
3. The servers must also authenticate themselves to the user
    - Attacker could insert a false server

##### Authenticators 

**Problem 2** is solved by **A** providing a secret piece of info to both **C** and **T** inside the ticket:
- **C** can then prove to **T** that it is the same client session as the one given in the Ticket.
- This is done with a **session key (ctK)** for use with **C** and **T**.

When user requests a service, it sends an **Authenticator** (ctK[cID, cIP, Timestamp]) to the Ticket Granting Service, to prove that it is coming from the same client session.

##### Server Authentication

**Third Problem** is solved as follows:

- When user requests a service, **T** sends back a session key, along with a **server Ticket** which also contains the session key.
- The client creates another authenticator and sends it to the server together with the Ticket.
- The server (if able to open authenticator) add's a 1 to the timestamp and sends back
    - If a 1 is not added, the server was trying to replay a previous ticket
    
### Timestamps

**Timestamps** rely on time being synchronised across all machines. Network time protocols can be insecure, so this can be a weakness (allowing replay attack). 

The have a **fixed lifetime**, and represent a period of time. This is necessary because of network delays etc. 

System's are vulnerable to replay attacks while timestamps are **valid**. Servers should keep a table of all current tickets to foil this.

### Kerberos Software Weaknesses

Machine running software must be kept secure, since all keys are stored in an internal databse on that machine. Attacker must be prevented from replacing the Kerberos process with one of their own choosing. 

**Client Keys** are based on the client's password, so are only as secure as the client makes them. Therefore company password protocols must be put in place to ensure secure passwords.
