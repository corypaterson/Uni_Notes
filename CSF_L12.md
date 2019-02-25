# Cyber Security Fundamentals
### Lecture 12 - Security of a Web Based Application 
---

### Security of a Web Based Application 

Looking at the security threats and possible counter-measures of a typical **4 level** web based application:

- Client 
- Webserver
- Application Sever
- Database and other specialist facilities

Each level has its own **security problems** and **solutions**, as well as the three types of communications between levels.

---

### Threats: Client

The client machine is outside of a developer's control. 

> We expect client machines to use a standard browser, but attackers can generate their own hand crafted HTTP requests if they decide to attack.

**Failure to log out**:
- Allows access to user related info
- This is not strictly a problem for the application, but is still an issue

**Browser Cache**:
- The browser may well cache pages or cookies in case they are needed again.
- These will be caught in the user's file system, where they can be accessed easily.

**Downloadable Information**: 
- Any code that runs on the client can be seen
- This can provide insight into the terminal workings of the application
- This has implications for intterlectual property rights
- ID numbers may also be used to guess at the URLs of internal web pages, the structure of requests, and so on.

### Countermeasures: Client

**Removing Meaning from Client Side Code**:
- Client side code should **not contain any comments** and should be obfusticated as much as possible
- **No business logic should appear in client side code**, which should only deal with presentation issues.

**Avoid Caching**:
- **Set page expiration to immediate** so that the browser will not cache the page. Unfortunately, the back button will not return user to previous pages.
- **Don't use permanent cookies**. Transient in-memory cookies can be used to record session info, but can still be seen by anyone with access to client memory.

**Field Validation**:
- **Length validation** of all input from the client, to prevent buffer overflow attacks.
- **Content validation** of all data from client, to make sure correct format and remove special characters.
- **Use message digests** on all round trip information to detect tampering and replay attacks.

**Avoid in clear information**:
- **Do not use HTTP GET command**, use POST instead.
- **Encrypt HTTP body** using TLS.
- **Do not use hidden fields**, an attacker can save a page, change a hidden field and then replay that page.

---

### Threats: Web Server

Web server is under our control.

**Exploiting Vulnerabilities of Server Software**:

- Need to make sure patches are up to date, as server software vulnerabilities will be well known.
- New vulnerabilites arise and therefore need to keep up to date with literature and relevent web sites.

**Caching of Sensitive Information**:
- Session related infomration may be cached on the server.

**DOS Attacks**, **Impersonation of users**,

**Replay Attack**:
- The replay may be a login request or payment request.

**Hosting an Onward Attack**:
- The structure of the internal domain can be discovered, allowing an enemy to attack it.

**Cross Process Contamination**:
- Information destined for one process may be sent to another
- This happens when using components and web services

### Countermeasures: Web Server

- **No direct access to business data**. This access is achieved at the process server level.
- **Session timeout**, protects against users who leave while still logged in.
- **Null memory after use**, as memory that has not been nulled is similar to a cache.
- **Session management**, correctly identify which session any client activity belongs to.
- **DOS Countermeasures**.

---

### Threats: Process Server

The process server processes requests from the web server.

It can be attacked from a comprimised web server or another machine pretending to be one. 

**Illegitimate Request**:
- If the format of a valid request is known and authentication has been bypassed.

**Denial of Service**:
- This would be from a single webserver machine, and so not as serious as a DDOS attack.

**Illegitimate Corpus**:
- Some parts of the system might have been replaced, either by a successful attack or by an insider attack.

### Counter Measures: Process Servers

**User Authentication**:
- User authentication should take place at this level, rather than the webserver as it is more secure.
- Avoid root users. Each user will have only the permissions they require and no more.

**Authorisation Checks**:
- Make sure that the user is authorised to undertake the requests they are making.

**Password Re-entry**:
- Ask user to re-enter password at crucial stages for extra verification.

**Stateless Components**:
- Make sure each component used, does not retain any information that could be used when they are next invoked. 
- **Components should not have instance variables**

**Component Classification**:
- All components are signed to certify that they are genuine.

**Webserver Authentication**.

---

### Threats: Database and other services

The database is where all persistent information is kept. A lot of damage can be done if comprimised.

**Illegitimate Requests**:
- The database will respond to any well formed query from any machine with the appropriate access rights.

**Internal Attack** (someone inside your own organisation):
- Database tools such as Query Analyser, can be used to comprimise data.
- Other parts of the system may also be vulnerable to an internal attack, but database is detrimental.

### Countermeasures: Database

**Access Controls**:
- Only certified components can access the database.

**Use of Stored Procedures**:
- Make it difficult to construct ad-hoc queroes, although usually there must be a machanism to allow some ad-hoc queries.

**Encrypted Columns**:
- Some columns are encrypted
- Only secure components can access them
- All access to them would be stored via procedures.

---

### Threats: Connections between computers

The client machines, webservers, process servers and database servers are **all connected** and the connections are **all vulnerable**.

**Disclosure to packet analysers**:
- Packet analysers are placed next to communication cables and record all of the packets passing to and fro, reassembling them into streams.

### Threats: Client - Web Server Link

This connection is outside our control and can raise many issues.

**Proxy server Caches**:
- This connection will pass through several nodes, such as an ISP or corporate gateway.
- These nodes might cache information on the way.
- The cached info can be avaliable to others.

**Information Sent in the Clear**:
- The **HTTP header** for all HTTP packets is **never encrypted**. This includes URL.
- The GET method of parameter passing, adds parameters as part of the URL, and therefore, are communicated in the clear.
- The POST method uses the HTTP packet body and can therefore be encrypted.

---

### External Safeguards

**Firewalls**:
- A typical hardware architechture will have **two firewalls**.
- The first:
    - filters all non-HTTP traffic to the webserver.
- The second:
    - makes sure that only the webservers can access the process server.

**Intrusion Detection**:
- Third party products that can detect any unusual activity and alert an administrator.
- Tamper detection can be achieved with messaged digests.

---

### Email Problems

There are security implications if our system accepts inbound email and generates outbound email:

**Impersonation**:
- Phishing etc.

**Denial of Service**:
- Email bombs could be sent

**Viruses and Executable Attachements**:
- This threat will cause problems if our system is affected
- Reputation will suffer if we send out infected emails

**Spam Relay**:
- Email server may be taken over as a spam relay and become blacklisted,
- preventing us from sending legitimate emails.
- This would also damage reputation.

**Security of Mail Content**:
- Encryption of email is not widespread and distribution of encrpyted email relies on encryption at both ends
- We cannot assume that customers will use encrypted email.

### Countermeasures: Email

**Web based mail**:
- Provide our own web based email, which we can make sure is encrypted.

**Check for viruses**:
- Both on inbound and outbound email

**Verify that the SMTP header is valid**.


**Configure email system securely**:
- make sure it cannot be used as a relay.
---
### See table of threats and counter measures in lecture notes so that none are forgotten.





