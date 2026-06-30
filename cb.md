# Cryptography Basics

# Cryptography in Cybersecurity: Questions and Answers

## 01. What is cryptography in cybersecurity

Cryptography in cybersecurity is the practice of protecting information by transforming it into a form that unauthorized people cannot easily read or alter.

It is used to provide:

- **Confidentiality**: keeping data secret
- **Integrity**: proving data was not modified
- **Authentication**: proving identity or origin
- **Non-repudiation**: preventing someone from denying they performed an action

A simple example: when you visit a website using **HTTPS (Hypertext Transfer Protocol Secure)**, cryptography helps protect the data exchanged between your browser and the website.

---

## 02. What are the different types of cryptography

The main types of cryptography are:

### a.) Symmetric-key cryptography

The same key is used for encryption and decryption.

Example: **AES (Advanced Encryption Standard)**

### b.) Asymmetric-key cryptography

Two keys are used: a public key and a private key.

Examples:

- **RSA (Rivest-Shamir-Adleman)**
- **ECC (Elliptic Curve Cryptography)**

### c.) Hash functions

Data is converted into a fixed-length value called a hash. Hashing is one-way, meaning it cannot practically be reversed.

Example: **SHA-256 (Secure Hash Algorithm 256-bit)**

### d.) Key exchange algorithms

These allow two parties to agree on a shared secret over an insecure channel.

Examples:

- **DH (Diffie-Hellman)**
- **ECDH (Elliptic Curve Diffie-Hellman)**

---

## 03. What is Encryption

Encryption is the process of converting readable data, called **plaintext**, into unreadable data, called **ciphertext**, using an algorithm and a key.

Example:

Plaintext:

```text
Hello
```

Encrypted ciphertext:

```text
X8fK2!pQ
```

The purpose of encryption is to stop unauthorized people from reading the original data.

---

## 04. What is Decryption

Decryption is the process of converting encrypted data, called **ciphertext**, back into readable data, called **plaintext**, using the correct key.

Example:

Ciphertext:

```text
X8fK2!pQ
```

After decryption:

```text
Hello
```

Encryption hides the message. Decryption reveals it again.

---

## 05. What is the importance of cryptography

Cryptography is important because modern cybersecurity depends on it.

It protects:

- Passwords
- Banking transactions
- Messaging apps
- Website traffic
- Cloud storage
- Digital signatures
- Software updates
- Cryptocurrency wallets
- Identity and access systems

Without cryptography, attackers could read private data, modify files, impersonate users, steal credentials, or tamper with online transactions.

The important idea: cryptography does not just hide data. It also helps prove that data is authentic and unchanged.

---

## 06. What are the types of cryptography

The types of cryptography are:

### 1. Symmetric cryptography

One shared secret key is used.

Example: **AES (Advanced Encryption Standard)**

### 2. Asymmetric cryptography

A public/private key pair is used.

Example: **RSA (Rivest-Shamir-Adleman)**

### 3. Hashing

Data is transformed into a fixed-size digest.

Example: **SHA-256 (Secure Hash Algorithm 256-bit)**

### 4. Digital signatures

A private key signs data, and a public key verifies the signature.

Example: **ECDSA (Elliptic Curve Digital Signature Algorithm)**

### 5. Message authentication codes

A secret key is used to prove message integrity and authenticity.

Example: **HMAC (Hash-based Message Authentication Code)**

---

## 07. What are the applications of cryptography

Cryptography is used in many cybersecurity areas, including:

### 1. Secure web browsing

**HTTPS (Hypertext Transfer Protocol Secure)** uses **TLS (Transport Layer Security)** to encrypt web traffic.

### 2. Password protection

Passwords should be stored as hashes, not plaintext.

### 3. Digital signatures

Used to verify documents, software, and transactions.

### 4. Secure messaging

Apps use encryption to protect conversations.

### 5. Virtual Private Networks

**VPN (Virtual Private Network)** systems encrypt traffic between a user and a network.

### 6. Cryptocurrencies

Cryptography protects wallets, signatures, and transaction integrity.

### 7. File and disk encryption

Tools like BitLocker and VeraCrypt protect stored data.

### 8. Email security

**PGP (Pretty Good Privacy)** and **S/MIME (Secure/Multipurpose Internet Mail Extensions)** protect email content and identity.

---

## 08. What is a hash algorithm

A hash algorithm is a mathematical function that converts input data into a fixed-length output called a **hash**, **digest**, or **hash value**.

Example:

Input:

```text
password123
```

Hash output:

```text
ef92b778bafe771e89245b89ecbc...
```

A good cryptographic hash algorithm has these properties:

- **Deterministic**: same input always gives the same hash
- **One-way**: hard to reverse back to the original input
- **Collision-resistant**: hard to find two different inputs with the same hash
- **Avalanche effect**: a tiny input change creates a very different hash

Hashes are used for password storage, file integrity checks, digital signatures, and malware detection.

---

## 09. What SHA stands for

**SHA** stands for **Secure Hash Algorithm**.

Common examples include:

- **SHA-1 (Secure Hash Algorithm 1)**
- **SHA-2 (Secure Hash Algorithm 2)**
- **SHA-256 (Secure Hash Algorithm 256-bit)**
- **SHA-512 (Secure Hash Algorithm 512-bit)**
- **SHA-3 (Secure Hash Algorithm 3)**

**SHA-1 (Secure Hash Algorithm 1)** is considered weak for collision resistance and should not be used for modern security-sensitive systems. **SHA-256 (Secure Hash Algorithm 256-bit)** and **SHA-3 (Secure Hash Algorithm 3)** are stronger modern choices.

---

## 10. What is `John the Ripper`

`John the Ripper` is a password auditing and password hash cracking tool.

It is commonly used by security testers and system administrators to check whether users have weak passwords.

It can test password hashes using techniques such as:

- Dictionary attacks
- Brute-force attacks
- Mask attacks
- Rule-based attacks
- Hybrid attacks

Example use case: a security team exports password hashes from an authorized test system and checks whether weak passwords can be cracked.

---

## 11. How to use `John the Ripper`

A basic authorized workflow looks like this:

### 1. Put the hash into a file

For example:

```text
hashes.txt
```

### 2. Run `John the Ripper` against the file

```bash
john hashes.txt
```

### 3. Show cracked passwords

```bash
john --show hashes.txt
```

### 4. Use a wordlist

```bash
john --wordlist=/path/to/wordlist.txt hashes.txt
```

### 5. Specify a hash format when needed

```bash
john --format=raw-md5 hashes.txt
```

Example with **SHA-256 (Secure Hash Algorithm 256-bit)**:

```bash
john --format=raw-sha256 --wordlist=wordlist.txt hashes.txt
```

Useful commands:

```bash
john --list=formats
```

Lists supported hash formats.

```bash
john --status
```

Shows cracking progress.

```bash
john --restore
```

Restores an interrupted session.

---

## 12. How to crack advanced hashes with `John the Ripper`

For advanced hashes, the important part is identifying the correct hash type and using a realistic attack strategy.

### 1. Identify the hash type

```bash
john --list=formats
```

You can also inspect the hash structure manually. For example, many modern password hashes include identifiers such as:

```text
$2y$...
```

This usually indicates bcrypt.

```text
$argon2id$...
```

This indicates Argon2id.

```text
$6$...
```

This usually indicates SHA-512 crypt.

### 2. Specify the correct format

Example for bcrypt:

```bash
john --format=bcrypt --wordlist=wordlist.txt hashes.txt
```

Example for SHA-512 crypt:

```bash
john --format=sha512crypt --wordlist=wordlist.txt hashes.txt
```

Example for **NTLM (NT LAN Manager)**:

```bash
john --format=nt hashes.txt
```

### 3. Use rules to mutate wordlists

Rules generate variations such as adding numbers, changing capitalization, or appending symbols.

```bash
john --wordlist=wordlist.txt --rules hashes.txt
```

### 4. Use incremental mode

Incremental mode tries many character combinations.

```bash
john --incremental hashes.txt
```

### 5. Use masks for known password patterns

Example: try passwords like `Summer2024!`, `Winter2024!`, and similar patterns.

```bash
john --mask='?u?l?l?l?l?l?d?d?d?d?s' hashes.txt
```

Mask symbols commonly mean:

- `?u`: uppercase letter
- `?l`: lowercase letter
- `?d`: digit
- `?s`: symbol

### 6. Show results

```bash
john --show hashes.txt
```

The key point: “advanced hashes” such as bcrypt, scrypt, **PBKDF2 (Password-Based Key Derivation Function 2)**, and Argon2 are intentionally slow. That is the whole point. They are designed to make cracking expensive.

---

## 13. What is `hashcat`

`hashcat` is a high-performance password recovery and hash cracking tool.

It is especially known for using **GPU (Graphics Processing Unit)** acceleration, which can make it much faster than **CPU (Central Processing Unit)**-only cracking for many hash types.

`hashcat` supports many attack modes, including:

- Dictionary attack
- Brute-force attack
- Mask attack
- Rule-based attack
- Combinator attack
- Hybrid attack

It is commonly used for password audits, penetration testing labs, and defensive security assessments.

---

## 14. How to use `hashcat`

A basic authorized workflow looks like this:

### 1. Put hashes in a file

```text
hashes.txt
```

### 2. Choose the hash mode

For example:

- **MD5 (Message Digest Algorithm 5)**: mode `0`
- **SHA-1 (Secure Hash Algorithm 1)**: mode `100`
- **SHA-256 (Secure Hash Algorithm 256-bit)**: mode `1400`
- **NTLM (NT LAN Manager)**: mode `1000`
- bcrypt: mode `3200`

### 3. Run a dictionary attack

```bash
hashcat -m 1400 -a 0 hashes.txt wordlist.txt
```

Where:

- `-m 1400` means **SHA-256 (Secure Hash Algorithm 256-bit)**
- `-a 0` means dictionary attack
- `hashes.txt` contains the hashes
- `wordlist.txt` contains candidate passwords

### 4. Run a mask attack

```bash
hashcat -m 1000 -a 3 hashes.txt ?u?l?l?l?l?l?d?d
```

This tries patterns like:

```text
Password12
Welcome99
Summer24
```

### 5. Use rules with a wordlist

```bash
hashcat -m 1000 -a 0 hashes.txt wordlist.txt -r rules/best64.rule
```

### 6. Show cracked results

```bash
hashcat -m 1000 hashes.txt --show
```

### 7. Check available hash modes

```bash
hashcat --help
```

### 8. Check available devices

```bash
hashcat -I
```

A simple example:

```bash
hashcat -m 0 -a 0 hashes.txt wordlist.txt
```

This means:

- `-m 0`: **MD5 (Message Digest Algorithm 5)**
- `-a 0`: dictionary attack
- `hashes.txt`: file containing hashes
- `wordlist.txt`: file containing password guesses

`hashcat` is generally faster than `John the Ripper` for many **GPU (Graphics Processing Unit)**-friendly hashes, while `John the Ripper` is often more flexible and convenient for mixed formats and Unix-style password auditing.
