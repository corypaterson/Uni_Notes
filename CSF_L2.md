# Cyber Security Fundementals
### Lecture 2 - Technical Solution
---

### Levels of abstraction
- The **problem** to be solved.
- A **protocol** or high-level description of the problem.
    - Can be constructed from several lower level **sub-protocols**
- Protocols can then be implemented by different **algorithms**

It is conventional to use the following characters when describing protocols.
- Alice, Bob, Carol and Dave have secrets to share
- Eve the eavesdropper tries to find out the secrets and cause other problems
- Trent is a trusted third party

The **problem** to develop a **protocol** for is: *Alice wants top transmit secret information to Bob, without Eve finding out.*

---
### Using a Secure Transmission Medium

Alice and Bob meet in a secure room or location (the only secure transmission medium).

Electronic transmissions are easy to intercept as:

- **Transponders** can be attached to Ethernet cables, and traffic analysed.
- Email is stored and can be analysed later.

---

### Hiding in Plain Sight

Alic could send Bob and email or phone him.

Due to the large volumes of other emails and voice transmissions, messages may be ignored. 
- Only works if automated tools (similar to search engines), do not find them suspicious.
- And neither Alice or Bob is under surveillance

---

### Secure Preparation

- Alice encrypts the message in a secure area.
- It is then transmitted by an insecure medium.
- Bob then decrypts the message in a secure area

The secure area however is not always secure. **Distributed Files Systems** mean the file is stored else where and will travel via insecure ethernet to an another computer. Computers may also have **keystroke logging** programs and other spyware.

Problems with this method:
 - Alice and Bob both need to know how to encrypt and decrypt the information.
 - They must use a compatible method.
 - They need to communicate the method of encryption by a different protocol.
    - Meet in a secure area perhaps.

**Using a secret algorithm**:

Keepig the details of the algorithm secret is bad for two reasons:

- The algorithm designers know the secret and may be at risk
- If the algorithm is public (not secret), then the peer review will reduce flaws in the algorithm, therefore is **better to use a more refined public algorithm**.

**Public algorithm, Secret Key**: 

Details of the encryption algorthms are kept public. 

- They have a parameter, **the key**, which is kept secret.
- Knowledge of the algorithm is useless without the key
- Alo called a **one key** system
---

### Key Distribution Problem

The key must also be stored safely: **the key storage problem**.

The problem of transfering data between Alice and Bob has been transformed into an easier problem: 
 - The problem of transfering a key.

---
### Public Key System

**Two** different keys are used.

A **public key** is used for encryption. Anyone can access this key, therefore there is no key distribution problem.

A **secret key** is used for decryption. Knowledge of the public key will not lead to knowledge of the secret key.

Then a single encryption algorthm is used, the public key will encrypt, while the secret key will decrypt.

EXAMPLE:

- Alice gets Bob's public key using an insecure medium.
- Encrypts her secret in a secure area.
- Send the ciphertext to Bob using an insecure medium.
- Bob uses his secret key to decrypt the ciphertext in a secure area.


>**Authentication problem**: How does Alice know that the public key is Bob's? and retrospectively, how does Bob know that the message is Alice's? (See man in the middle attack)
---

### Man in the Middle Attack

1. Bob sends his public key to Alice, but it intercepted by Eve.
2. Eve sends her public key to Alice, pretending it is Bob's.
3. Alice encrypts the secrets with Eve's public key (thinking it is Bob's).
4. Alice sends the ciphertext to Bob.
5. Eve intercepts the ciphertext and decrypts it with her secret key.
6. She reads the secrets (can also modify secrets at this stage).
7. She encrypts it with Bob's public key and forwards it to Bob.
8. Bob then decrypts with his matching secret key
9. Both Alice and Bob are unaware of the attack.

---

### Public Key Digital Signatures

Alice encrypts her plaintext document with her secret key, rather than Bob's public key. She sends the original along with the encrypted version to Bob.

Bob can decrypt this information and verify that they are both the same. 

### Properties of Digital Signatures

1. Bob can verify the signature with out Alice's help.
2. The signature cannot be forged becuase only Alice knows her secret key.
3. The signed document is unalterable except by Alice.
4. The signature cannot be transfered to another document.

---

### Secrecy and Authenticity

Signing a document does not make it secure (Eve could also undo the signature and read the document). She could get Alice's public key.

Encrypting a document does not guaruntee authenticity. **Signing and encrypting** a document can provide both secrecy and authentication.

### Public Key Certificates

In many cases, the plain text document to be signed contains a public key. 
 - The signed key plus other information is called a public key certificate.
 - It is signed by Trent, a trusted third party
 
Bob can distribute his key in a public key certificate. Provided Alice already has Trent's public key.

**This defeats the man-in-the-middle attack**.

Problem: 

- In the preceeding example, the signed document was the same length as the unsigned version (inconvenient if many signed documents have to be stored - large memory capacity).
- If just a signature is added, then the signed document becomes public knowledge (it can be seen by using the public key to undo the signature).

---

### Message Digest

A **message digest** is a condensed version of an original document. It is typically about *512 bits long*. It is a short description of the original document, the chance of two different documents producing the same message digest is very low.

The algorthm to create a message digest, is sometimes called a **hash algorithm**.

Message Digest and Signatures:

- Giving someone a signed copy of a message digest is equivalent to a signed version of the document
- If the signature needs to be checked then the message digest can be calculated from the original document a second time.
- The original message digest can be recovered by removing the signature
- If they are both the same, then the signature is valid. 

