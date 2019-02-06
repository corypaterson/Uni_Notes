# Cyber-Security Fundementals
### Lecture 5 - Alternative User Authentication
---

### Three types of Authentication

What you **have**:
- A smart card or something similar

What you **know**:
- Password
- How do you know it?
- How do you remember it?

What you **are**:
- Biometrics

---

### Graphical Passwords

Its easier to remember complex information in visual form. 

We can have these as;

**Recognition** based, you will recognise something if you see it again.

**Recall** based, you can remember and recreate an image.

**Locimetric**, you can remember something with visual clues, or remeber certain parts of an image.

##### Passface - Recognition based system

On **registration**, shoose several different faces that you will have to reconise again. Then on **log in**, user is presented by several screens, eadch with 16 faces - recognise a face on each screen. 

You cant choose relatives or friends - open to a **social media attack**.

This doesnt work well in practice (people arent good at recognising faces they havent had a connection with)

##### Draw a secret - Recall

People remember what they have drawn because of the creative effort involved.

On **registration**, draw a simple shape. On **login**, draw the same again. 

Usually the patterns people make are too simple (so they can remember), therefore is suseptible to **bruteforce attack**.

---

### Biometrics

Finger Prints:


- Can be lifted from anything you touch, easy for someone else to aquire them.
- Readers can have trouble with dirty/oily fingers.
- Fake fnigers are easy to create, and readers find this easier to read.
- Owners of fingerprint based systems can be in danger of loosing a finger.

> Iris scanners are better as it is hard to create a fake iris

Biometric authentication should be monitored to ensure no faking it passed the system.

---

### False Pos/Negatives

False positive - wrongly say that the biometrics **match** (let someone break in).
False Negative - wrongly say that the biometrics **dont match** (exculde someone).

Biometrics should not be used for this issue.

**Solution:** Use an alternative form of identification and use biometrics to authenticate it - **Multifactor Authentication**.

---

# Multiple Key Cryptography
### Secret Splitting

This is authentication using **more than one person**. 

If Sam wants to split a secret message **M** between Alice and Bob: 

- Sam gets a bit string **R** thhat is the same length as **M** 
- Sam calculates **P = M ⊕ R** and gives **P** to Alice and **R** to Bob. 
- Then **M** can be recovered via **P ⊕ R = M**

This cannot be broken by cryptographic techniques. It can be expanded to multiple people by adding more 'same-length' bit strings.

Limitations: 

- All pieces of the encrypted message are necessary.
- If one person is comprimised, then all are comprimised.




