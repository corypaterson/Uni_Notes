# Cyber-Security Fundementals
### Stenography
---

### Secret Writing

Stenography is a form of hiding in plain sight. 

A secret **payload** is hidden inside an innocuous looking **cover object**, producing a **stego object**. They payload can be encrypted for additional security.

##### Text Example

The paylaod, a short piece of text, can be converted into a bit string. The cover object, a longer text document, can be modified by adding a space to the end of the next line if the next bit is a 1. 

Must be a way of indicating the end of a payload, perhaps by terminating it with a NULL character (8 zeros). 

### Detecting Stenography

Text documents with extra spaces at the ends of some lines would look suspcious. 
- The analysis would have to be digital
- If the original cover document was publically available, such as dracula.txt. Then the **stego** version of dracula.txt would be longer.

### Attacking Stenography
- The payload could be removed if the stego was processed to remove all blank spaces at the end of each line.
- This could be done on all emails, if steganography was suspected. 
    - This would prevent steganography but would not recover the secret payload
    - And might not detect if steganography has been used, depending on implementation

### Steganography with Images

- Textfiles have limited capacity, only good for small payloads
- Image files are much larger and are commonly exchanged
- Much more capacity to hide secret info
- Wide variety of image file formats will cause problems for steganographers

##### Image pixels

Image files contain header information and then the pixels. The bulk of the file being made up of pixels. Each pixel contains three colour components of red, green and blue. Each component is 8bits long, giving 256 differen possible values

##### Least Significant Bit

The least significant bit of each colour component is often quite random:

- Replacing it with a different value will often not be noticed
- Replacing all the least significant bits with bits from the payload will usually result in an image that looks the same as the original.
- Gives a payload capacity of 1/8th (12.5%)
- Replacing first two bits, can give 25% capacity

##### Problems with LSB:
- Capacity is quite large (hide an image in another image)
- The example cover image is quite good cayse the colours change rapidly over all of the image
- If cover image is quite plain (sky, plain colour etc), then changing pixels will be noticeable

### Recovering the payload

The embedding algortihm looks through all the segments in order. If the segment is complex enough then it is replaced by payload bits (Non-complex image segments are not changed).

The extraction algorithm also looks through all the segments:
- If the segment is complex then it must contain payload bits
- If it is not complex the it could be part of the cover image
- It could also be a non-complex part of the payload

##### Compression

Must use lossless compression, as otherwise when the file is compressed we will lose oout on information that will likely jeprodise the secret payload. 

##### Encrypted payload
- Payload can be encrypted for added security
- The techniques described here work with any bit string, whether encrypted or not
- Alternatively, keyed steganographic products take a key as a parameter and do both encryption and stagnography

### Steganalysis
Attacks on steganography can have several goals:
- Recover the payload
- Replace the payload
- Destroy the payload

A visual attack looks at images to see if they show signs of containing a hidden payload. This attack is very difficult however.

If someone has the original image, then the pixel comparrisons can be made.



