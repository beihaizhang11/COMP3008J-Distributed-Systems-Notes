# Security
## Overall
### Why Security Important
* promote the sharing of resources - open to external access
* Exposed interfaces to services offered by the distributed system
* Insecure networks
### How to Protect Resources
* Access to shared resources are managed by processes. 
* processes outline how you interact with the resource
* protect processes that execute shared objects or communicate with shared processes.
### Security Policy v/s Mechanisms
#### Definition
* Security Mechanisms: techniques used to protect a shared resource
* Security Policies: rules which govern the use of security mechanisms
#### Security Mechanisms
* Goal: protect shared resources from
* * Unauthorized access (hackers)
* * Malicious attacks (viruses)
* * Incorrect Usage (mistakes by valid users)
### Security Threats
* Leakage: the acquisition of information by unauthorized recipients.
* Tampering: the unauthorized alteration of information.
* Vandalism: interference with the proper operation of a system without gain to the perpetrator.
### Method of Attack
#### Overall
* access an existing communication channel
* establish a new channel that looks like an authorized one
#### Methods
* Eavesdropping – obtaining copies of messages without authority.
* Masquerading – sending or receiving messages using the identity of another principal without their authority.
* Message Tampering – intercepting messages and altering their contents before passing them on to the intended recipient.
* Replaying – storing intercepted messages and sending them at a later date.
* Denial of Service – flooding a channel or other resource with messages in order to deny access to others.
### Designing Secure Systems
Use Worst case assumptions.

## Cryptography
### Overall
* Cryptography - making “secret codes”: the study of mathematical techniques related to aspects of information security.
* Cryptanalysis - breaking “secret codes”: the study of mathematical techniques for attempting to defeat information security services.
* Cryptology - The art & science of making +breaking “secret codes”: the study of cryptography and cryptanalysis.
* Cryptosystem - A cipher or cryptosystem is used to encrypt the plaintext.
### Cryptosystem Principle
* Use Kerckhoffs’ Principle: Crypto algorithms (ciphers) are not secret.
* Characteristics of a Good Cipher: A cryptosystem should be secure even if everything about the system, except the key, is public knowledge.
### Types of Cryptography
* Symmetric Key: Same key for encryption and decryption.
* Public Key (asymmetric): Two keys, one for encryption (public), and one for decryption (private).
* Hash algorithms: “one way” crypto.
### Symmetric key (Conventional) Crypto
#### Definition
* In a network, the transmitter and receiver share a common key.
* Keys must be delivered/distributed in a secure manner.
#### 2 Types
* Stream cipher: generalize one-time pad.
* Block cipher: generalized codebook.
### Public Key Cryptography (PKC)
#### Two keys
* Public key: used to **encrypt messages** and **verify signatures**.
* Private key: only known by the owner; used to **decrypt messages** and to **create signatures**.
#### Trapdoor fuction
A trapdoor function is a function that is easy to compute in one direction, yet difficult to compute in the opposite direction (finding its inverse) without special information, called the "trapdoor". Trapdoor functions are widely used in cryptography
### Uses of Cryptography
#### Secrecy and Integrity
Ensuring the safety and correctness of information of transmitted over networks.
#### Authentication
Supporting communication between pairs of principals.
#### Digital Signatures

