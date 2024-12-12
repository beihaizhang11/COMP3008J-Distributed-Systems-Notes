# Security知识结构
## 安全问题产生的层次关系：
分布式系统特性 → 安全威胁 → 攻击方法 → 防护需求
## 安全解决方案的层次：
密码学基础(加密) → 认证机制 → 访问控制 → 安全模型和标准
## 加密技术的演进：
对称加密(简单但密钥分发困难) → 公钥加密(解决密钥分发问题) → 数字签名(提供身份认证)
## 安全机制的完整性：
认证(身份确认) → 授权(权限控制) → 访问控制(具体实现) → 安全等级(标准化)

# Security Problems in DS
## Why Security Important
* promote the sharing of resources - open to external access
* Exposed interfaces to services offered by the distributed system
* Insecure networks
## How to Protect Resources
* Access to shared resources are managed by processes. 
* processes outline how you interact with the resource
* protect processes that execute shared objects or communicate with shared processes.
## Security Policy v/s Mechanisms
* Security Mechanisms: techniques used to protect a shared resource
* Security Policies: rules which govern the use of security mechanisms
## Security Threats
* Leakage: the acquisition of information by unauthorized recipients.
* Tampering: the unauthorized alteration of information.
* Vandalism: interference with the proper operation of a system without gain to the perpetrator.
## Method of Attack
### Overall
* access an existing communication channel
* establish a new channel that looks like an authorized one
### Methods
* Eavesdropping – obtaining copies of messages without authority.
* Masquerading – sending or receiving messages using the identity of another principal without their authority.
* Message Tampering – intercepting messages and altering their contents before passing them on to the intended recipient.
* Replaying – storing intercepted messages and sending them at a later date.
* Denial of Service – flooding a channel or other resource with messages in order to deny access to others.
## Designing Secure Systems
Use Worst case assumptions.

# Cryptography
## Overall
* Cryptography - making “secret codes”: the study of mathematical techniques related to aspects of information security.
* Cryptanalysis - breaking “secret codes”: the study of mathematical techniques for attempting to defeat information security services.
* Cryptology - The art & science of making +breaking “secret codes”: the study of cryptography and cryptanalysis.
* Cryptosystem - A cipher or cryptosystem is used to encrypt the plaintext.
## Cryptosystem Principle
* Use Kerckhoffs’ Principle: Crypto algorithms (ciphers) are not secret.
* Characteristics of a Good Cipher: A cryptosystem should be secure even if everything about the system, except the key, is public knowledge.
## Types of Cryptography
* Symmetric Key: Same key for encryption and decryption.
* Public Key (asymmetric): Two keys, one for encryption (public), and one for decryption (private).
* Hash algorithms: “one way” crypto.
## Symmetric key (Conventional) Crypto
### Definition
* In a network, the transmitter and receiver share a common key.
* Keys must be delivered/distributed in a secure manner.
### 2 Types
* Stream cipher: generalize one-time pad.
* Block cipher: generalized codebook.
## Public Key Cryptography (PKC)
## Two keys
* Public key: used to **encrypt messages** and **verify signatures**.
* Private key: only known by the owner; used to **decrypt messages** and to **create signatures**.
## Trapdoor fuction
A trapdoor function is a function that is easy to compute in one direction, yet difficult to compute in the opposite direction (finding its inverse) without special information, called the "trapdoor". Trapdoor functions are widely used in cryptography
## Differences
* Symmetric encryption uses a single key that needs to be shared among the people who need to receive the message while asymmetrical encryption uses a pair of public key and a private key to encrypt and
decrypt messages when communicating.
* Symmetric encryption is an old technique while asymmetric encryption is relatively new. 
* Asymmetric encryption was introduced to complement the inherent problem of the need to share the key in symmetrical encryption model, eliminating the need to share the key by using a pair of public-private keys.
* Asymmetric encryption takes relatively more time than the symmetric encryption.
# Uses of Cryptography
## Secrecy and Integrity
Ensuring the safety and correctness of information of transmitted over networks.
## Authentication
Validate Identity
## Authorization
Control access permission
### Access Control & Capabilities
* Access Control Lists (ACLs): store access control matrix by column
  - Good when users manage their own files
  - Protection is data-oriented
  - Easy to change rights to a resource.
* Capabilities (or C-Lists): Store access control matrix by row
  - Easy to delegate - avoid the confused deputy
  - Easy to add/delete users
  - More difficult to implement
  - The “Zen of information security”
## Multilevel Security (MLS) Models
### Bell-LaPadula
* designed to express essential requirements for MLS
* deals with confidentiality
* BLP is simple
* BLP is one of the few security models that can be used to prove things about systems
* BLP has inspired other security models
### Biba’s Model
* BLP for confidentiality, Biba for integrity (Biba is to prevent unauthorized writing)
* Biba is (in a sense) the dual of BLP
* Low water mark principle for integrity
