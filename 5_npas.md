# Network Protocols: Auditing and Securing


## Core Security Principles & Protocol Differentiation


**01. What are the three core security goals that secure protocols aim to achieve.**

Secure protocols primarily aim to achieve the three core goals of the CIA (Confidentiality, Integrity, Availability) triad. However, in the specific context of data transmission protocols, the primary goals usually emphasize Authentication over Availability:
*   **Confidentiality:** Ensuring that data is encrypted so it remains private and unreadable to unauthorized parties.
*   **Integrity:** Ensuring that data has not been tampered with, altered, or corrupted during transit.
*   **Authentication:** Verifying the digital identities of the communicating parties to guarantee they are who they claim to be.

**02. What is the main difference between application-layer protocols and network-layer protocols.**

The main difference lies in their purpose within the OSI (Open Systems Interconnection) model. Network-layer protocols (Layer 3), such as IP, are responsible for routing, addressing, and moving packets of data across different networks from a source to a destination, regardless of what the data is. Application-layer protocols (Layer 7), such as HTTP (Hypertext Transfer Protocol), operate at the top level and are responsible for formatting data and providing specific network services directly to the end-user's software (like web browsers or email clients).

**03. Explain the concept of port numbers and their significance in network communication.**

Port numbers are 16-bit virtual endpoints (ranging from 0 to 65535) used in TCP (Transmission Control Protocol) and UDP (User Datagram Protocol) networks. Their significance is that they allow a single machine with one IP address to run multiple distinct network services simultaneously. When a packet arrives, the port number directs the operating system to hand the data over to the correct application (for example, traffic arriving on port 80 is routed to the HTTP (Hypertext Transfer Protocol) web server, while traffic on port 22 goes to the secure remote login service).


## Secure Web & Remote Access Protocols


**04. What is the difference between SSL and TLS, and which one is actually used today.**

SSL (Secure Sockets Layer) is an older, legacy cryptographic protocol created to secure communication over a network. TLS (Transport Layer Security) is the modern, upgraded successor to SSL, featuring stronger encryption algorithms, faster performance, and better security mechanisms against modern cyber threats. Today, SSL is completely deprecated and considered insecure. TLS (specifically versions 1.2 and 1.3) is the protocol actually used today, even though many people and companies still colloquially refer to it as "SSL."

**05. How the TLS handshake works when visiting a secure website.**

When visiting a secure website, the TLS (Transport Layer Security) handshake occurs immediately after the initial TCP (Transmission Control Protocol) connection is established. It works in these general steps:
1.  **Client Hello:** The web browser sends a message listing its supported TLS versions and cipher suites (encryption algorithms).
2.  **Server Hello:** The server replies with the chosen cipher suite, TLS version, and its digital certificate (which contains its public key).
3.  **Verification:** The client verifies the server's certificate against its trusted CA (Certificate Authority) list to ensure the site is legitimate.
4.  **Key Exchange:** The two parties use mathematics (like a Diffie-Hellman key exchange) to securely generate a shared "pre-master secret."
5.  **Session Keys:** Both sides use this shared secret to generate symmetric session keys.
6.  **Secure Connection:** Both parties send "Finished" messages encrypted with the new session keys. The handshake is complete, and all subsequent web data is encrypted.

**06. What problem did SSH solve that older protocols like Telnet couldn't handle.**

SSH (Secure Shell) solved the critical problem of plaintext data transmission over insecure networks. Older protocols like Telnet sent all communication—including sensitive usernames, passwords, and system commands—in clear, unencrypted text. This made it extremely easy for attackers to use packet sniffers to steal credentials or perform MitM (Man-in-the-Middle) attacks. SSH solved this by encrypting the entire session and providing strong mutual authentication, ensuring confidentiality and integrity.

**07. How does SSH authentication with public keys work.**

SSH (Secure Shell) public key authentication uses asymmetric cryptography. A user generates a mathematical key pair: a private key (kept secretly on the client's device) and a public key (uploaded to the remote server). When the client attempts to log in, the server generates a random challenge and encrypts it using the user's public key (or asks the client to digitally sign a challenge). The client uses its private key to decrypt or sign the challenge and sends the result back to the server. Because only the matching private key can solve this mathematical challenge, the server grants access. This securely proves the user's identity without ever sending the private key or a password across the network.

**08. Differentiate between secure protocols like HTTPS, SFTP and their insecure counterparts HTTP, FTP.**

The fundamental difference is the application of encryption. Insecure protocols like HTTP (Hypertext Transfer Protocol) and FTP (File Transfer Protocol) transmit their data in plaintext, meaning anyone intercepting the network traffic can read the contents, including files, passwords, and user data. Secure protocols wrap this communication in strong encryption. HTTPS (Hypertext Transfer Protocol Secure) secures web traffic using TLS (Transport Layer Security), while SFTP (SSH File Transfer Protocol) secures file transfers using an SSH (Secure Shell) tunnel. These secure counterparts guarantee data confidentiality and integrity, preventing eavesdropping and tampering.

**09. Explain why HTTPS is mandatory for user trust, data protection, and modern web features.**

HTTPS (Hypertext Transfer Protocol Secure) is mandatory for several critical reasons:
*   **User Trust:** Web browsers heavily penalize non-HTTPS sites by labeling them "Not Secure," which drives users away. The padlock icon assures users their connection is private.
*   **Data Protection:** HTTPS encrypts data in transit, protecting sensitive information like login credentials, credit card numbers, and personal messages from interception or MitM (Man-in-the-Middle) attacks.
*   **Modern Web Features:** Browsers restrict powerful modern API (Application Programming Interface) features—such as geolocation, camera/microphone access, offline caching, and secure cookies—exclusively to HTTPS contexts to prevent network attackers from abusing them.


## Network Layer & VPN Protocols


**10. What is the difference between Transport Mode and Tunnel Mode in IPSec, and which is used for VPNs.**

In IPSec (Internet Protocol Security):
*   **Transport Mode** encrypts only the data payload of the IP packet, leaving the original IP header intact and visible. It is generally used for direct end-to-end communication between two specific host machines.
*   **Tunnel Mode** encrypts the entire original IP packet (both the payload and the original header). It then encapsulates this encrypted packet inside a brand-new IP packet with a new header.
**Tunnel Mode** is the one primarily used for VPN (Virtual Private Network) connections, as it securely routes entire networks' traffic over the internet (e.g., connecting a remote worker to a corporate LAN (Local Area Network)) while hiding the internal routing information.

**11. What is the difference between the AH (Authentication Header) and ESP (Encapsulating Security Payload) protocols in IPSec.**

AH (Authentication Header) and ESP (Encapsulating Security Payload) are the two core protocols of IPSec (Internet Protocol Security), but they offer different layers of protection:
*   **AH** provides data integrity, data origin authentication, and protection against replay attacks. However, it does *not* provide encryption; the data payload is sent in plaintext and remains readable to anyone inspecting the packet.
*   **ESP** provides everything AH provides (integrity and authentication) but importantly adds confidentiality through encryption. With ESP, the actual data payload is scrambled and hidden. Because of this encryption, ESP is the standard choice in modern deployments.

**12. Why should PPTP never be used for security-sensitive tasks.**

PPTP (Point-to-Point Tunneling Protocol) is a severely outdated VPN (Virtual Private Network) protocol that relies on broken cryptography. It uses MS-CHAPv2 (Microsoft Challenge Handshake Authentication Protocol version 2) for authentication, which is vulnerable to offline dictionary attacks and can be cracked to recover user credentials. Furthermore, it encrypts data using the weak RC4 (Rivest Cipher 4) algorithm. Because these vulnerabilities are public and easily exploited, attackers can routinely intercept and decrypt PPTP traffic, making it entirely unsafe.

**13. What makes the modern WireGuard protocol faster and more efficient than traditional VPN protocols like OpenVPN.**

WireGuard is vastly faster and more efficient than older VPN (Virtual Private Network) protocols for three main reasons:
*   **Kernel-Space Operation:** WireGuard operates directly within the operating system's kernel space, eliminating the heavy performance lag of constantly switching context between user space and kernel space (a bottleneck for OpenVPN).
*   **Modern Cryptography:** It exclusively utilizes a strict set of state-of-the-art, highly optimized cryptographic primitives (like ChaCha20 and Curve25519) rather than carrying the bloat of older, slower cryptographic libraries.
*   **Lean Codebase:** WireGuard is built on roughly 4,000 lines of code, whereas OpenVPN has hundreds of thousands. This lean design heavily reduces CPU (Central Processing Unit) overhead, lowers latency, and vastly simplifies security auditing.


## Common Protocol Auditing & Risk Assessment


**14. Explain the purpose of the Network File System (NFS) protocol and how misconfigurations can lead to exposed shares.**

The NFS (Network File System) protocol allows a computer to share directories and files over a network, enabling client machines to mount remote file systems and interact with them as if they were local storage.
Security risks heavily arise from poor configuration. If an NFS share is exported to "*" (meaning any IP address can connect) rather than a strict list of trusted IPs, anyone on the network can access the files. Furthermore, if the `no_root_squash` configuration is enabled, it allows a remote user with root privileges on their own client machine to maintain those same root privileges (UID or User Identifier 0) on the shared remote files, easily leading to complete system compromise via privilege escalation.

**15. Describe how the SMTP commands VRFY and EXPN can be exploited for user enumeration on a mail server.**

In the SMTP (Simple Mail Transfer Protocol), VRFY (Verify) is a command designed to check if a specific username or email address actually exists on the mail server. EXPN (Expand) is a command designed to reveal the individual email addresses contained within an alias or a mailing list.
Attackers exploit these commands to perform user enumeration. By automating a list of potential usernames and observing the server's responses to VRFY or EXPN commands, an attacker can mathematically confirm which accounts exist. With a valid list of users, they can then launch highly targeted attacks like spear-phishing or password brute-forcing.

**16. Explain the purpose of SNMP and the security risks associated with unencrypted data and default community strings.**

SNMP (Simple Network Management Protocol) is used by IT (Information Technology) administrators to monitor, manage, and configure devices on a network, such as routers, switches, and servers.
The primary security risk lies in legacy versions (SNMPv1 and SNMPv2c), which transmit all data—including authentication credentials—in unencrypted plaintext. These credentials, known as "community strings," act like passwords. Network devices frequently ship with default community strings (usually "public" for read-only access and "private" for read-write access). If these are not changed, any attacker on the network can trivially read sensitive network topology data, or worse, use the read-write string to maliciously alter the device's configuration.


## System Hardening & Vulnerability Management


**17. Explain the importance of keeping network protocols and server configurations up-to-date and patched.**

Keeping network protocols, server software, and configurations up-to-date is crucial because security researchers and malicious actors constantly discover new vulnerabilities. These flaws (tracked as a CVE, or Common Vulnerabilities and Exposures) can range from memory leaks to critical RCE (Remote Code Execution) exploits.
If systems are left unpatched, attackers can scan the internet to exploit these known vulnerabilities, allowing them to bypass authentication, inject malware, steal sensitive data, or crash the server via a DoS (Denial of Service) attack. Patching closes these security holes, keeping the system resilient.

**18. Explain the need for setting up basic firewall rules (like using iptables) to control network access.**

Setting up basic firewall rules using tools like `iptables` (which manages network packet filtering for the IP) is essential for controlling network access and reducing a system's attack surface. A firewall acts as a digital barrier between your machine and the untrusted internet.
Without firewall rules, every network service running on a machine is potentially exposed to the outside world. By implementing rules based on the principle of least privilege, administrators can explicitly allow traffic only on necessary ports (like port 443 for web traffic) and drop all other incoming connections. This prevents unauthorized access and limits the damage if an internal service is accidentally misconfigured or left running.

**19. Identify common SSH configuration weaknesses that require hardening (permitting root login, password authentication).**

When configuring an SSH (Secure Shell) server, several common default weaknesses require immediate hardening:
*   **Permitting Root Login (`PermitRootLogin yes`):** The "root" user has absolute power over the system, and its username is known to everyone. Leaving this enabled allows attackers to focus all their brute-force automation on guessing a single password to instantly gain total control. It should be disabled or restricted to keys-only.
*   **Password Authentication (`PasswordAuthentication yes`):** Passwords can be guessed, phished, or cracked via dictionary attacks. Hardening requires disabling password authentication entirely and mandating public-key authentication, which is cryptographically secure and virtually immune to automated brute-force attacks.
