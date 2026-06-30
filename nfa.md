# Networking Foundations and Architecture

**01. What is networking and why is it essential?**

Networking is the practice of connecting computers, devices, and systems together to allow them to communicate. It is essential because it enables the sharing of resources (like printers and internet connections), facilitates the rapid exchange of data, and allows for centralized management and communication across the globe.

**02. What is the difference between LAN and WAN?**

A **LAN** (Local Area Network) connects devices within a limited geographical area, such as a home, school, or office building, typically offering high speeds and low latency. A **WAN** (Wide Area Network) connects multiple LANs over a large geographical area (like cities, countries, or the entire globe, with the Internet being the largest WAN), usually relying on telecommunication links.

**03. What are the main network topologies (Bus, Star, Ring, Mesh)?**

*   **Bus:** All devices share a single central communication cable.
*   **Star:** All devices connect to a central node (like a switch or hub). If a cable fails, only that device goes down.
*   **Ring:** Devices are connected in a closed loop. Data travels in one direction from device to device.
*   **Mesh:** Devices are interconnected with many redundant paths. In a full mesh, every device connects to every other device.

**04. What is the difference between physical and logical topology?**

**Physical topology** refers to the actual physical layout of the cables and devices (how things are plugged in). **Logical topology** refers to how data actually flows through the network from one device to another, regardless of the physical layout.

**05. What are the 7 layers of the OSI model and their functions?**

The **OSI** (Open Systems Interconnection) model has 7 layers:
1.  **Physical:** Transmits raw bit streams over a physical medium (cables, radio waves).
2.  **Data Link:** Formats data into frames and handles node-to-node delivery via **MAC** (Media Access Control) addresses.
3.  **Network:** Routes packets across different networks using **IP** (Internet Protocol) addresses.
4.  **Transport:** Ensures reliable or unreliable delivery of data segments using **TCP** (Transmission Control Protocol) or **UDP** (User Datagram Protocol).
5.  **Session:** Manages and terminates communication sessions between applications.
6.  **Presentation:** Translates, encrypts, and compresses data into a readable format for the application.
7.  **Application:** Provides network services directly to user applications (like web browsers).

**06. What happens at each layer during data transmission?**

When sending data, the payload moves *down* the layers from Application to Physical, getting chopped into smaller pieces and acquiring specific headers/trailers at each layer. When receiving data, the physical bits are converted back up the layers from Physical to Application, with each layer reading and stripping its respective header until the original data is presented to the user.

**07. What is encapsulation and decapsulation?**

**Encapsulation** is the process of adding headers and trailers to data as it moves down the network layers from the sender (e.g., adding an IP header to a TCP segment). **Decapsulation** is the reverse process of removing these headers and trailers as data moves up the layers at the receiving end.

**08. What are the 4 layers of the TCP/IP model?**

The **TCP/IP** (Transmission Control Protocol / Internet Protocol) model simplifies the OSI model into 4 layers:
1.  **Network Access** (combines OSI Physical and Data Link)
2.  **Internet** (OSI Network)
3.  **Transport** (OSI Transport)
4.  **Application** (combines OSI Session, Presentation, and Application)

**09. How does TCP/IP compare to the OSI model?**

While the OSI model is a theoretical, 7-layer framework used primarily for educational and conceptual troubleshooting, the TCP/IP model is a practical, 4-layer model that represents how the modern Internet actually functions.

**10. Protocols & Transmission**

*(Note: This is a category header, but included here to maintain your requested numbering/order.)*

**11. What are the main network protocols (HTTP, HTTPS, FTP, SSH, DNS, DHCP)?**

*   **HTTP** (Hypertext Transfer Protocol): Used for transmitting unencrypted web page data.
*   **HTTPS** (Hypertext Transfer Protocol Secure): Secure, encrypted version of HTTP.
*   **FTP** (File Transfer Protocol): Used for transferring files between a client and server.
*   **SSH** (Secure Shell): Provides a secure, encrypted command-line access to remote devices.
*   **DNS** (Domain Name System): Translates human-readable domain names into IP addresses.
*   **DHCP** (Dynamic Host Configuration Protocol): Automatically assigns IP addresses and network configurations to devices.

**12. What is the difference between TCP and UDP?**

**TCP** (Transmission Control Protocol) is connection-oriented, meaning it establishes a session, guarantees delivery, and checks for errors (reliable but slower). **UDP** (User Datagram Protocol) is connectionless, meaning it just sends data without checking if it arrived (faster, used for streaming and gaming, but unreliable).

**13. What are the different types of transmission media (wired vs wireless)?**

*   **Wired:** Uses physical cables. Examples include Copper twisted-pair (Ethernet cables), Coaxial cables, and Fiber Optic cables (which use light for high-speed transmission).
*   **Wireless:** Uses electromagnetic waves. Examples include Radio Frequency (Wi-Fi, Cellular), Microwave, and Infrared.

**14. What is the role of a Hub, Switch, Router, Firewall?**

*   **Hub:** A basic Layer 1 device that receives data and blindly broadcasts it to all other connected ports.
*   **Switch:** A smart Layer 2 device that forwards data specifically to the destination device using MAC addresses.
*   **Router:** A Layer 3 device that connects different networks together and routes data based on IP addresses.
*   **Firewall:** A security device that monitors and controls incoming and outgoing network traffic based on predetermined security rules.

**15. What is the difference between Layer 2 and Layer 3 devices?**

A **Layer 2** device (like a Switch) operates on the Data Link layer, keeping traffic within a single local network by forwarding frames based on physical MAC addresses. A **Layer 3** device (like a Router) operates on the Network layer, moving packets *between* different networks using logical IP addresses.

**16. What is a VLAN and why is it used?**

A **VLAN** (Virtual Local Area Network) is a logical subdivision of a physical network. It is used to segment traffic on a single physical switch into multiple isolated virtual networks for better security, performance, and organizational management.

**17. What is 802.1Q tagging?**

**802.1Q** is an **IEEE** (Institute of Electrical and Electronics Engineers) standard for VLAN tagging. It inserts a small tag into the Ethernet frame so that switches and routers know which VLAN the data belongs to when traffic travels across shared trunk links.

**18. What are VLAN hopping attacks and how to prevent them?**

A VLAN hopping attack is an exploit where an attacker bypasses network segmentation to access traffic on a VLAN they shouldn't have access to (usually via Switch Spoofing or Double Tagging). Prevent it by disabling **DTP** (Dynamic Trunking Protocol), putting unused ports in an isolated VLAN, and setting the native VLAN to an unused ID.

**19. What is Inter-VLAN routing?**

Because VLANs isolate traffic at Layer 2, devices in different VLANs cannot communicate by default. Inter-VLAN routing uses a Layer 3 device (a router or a multi-layer switch) to route traffic between those separate VLANs.

**20. What is a MAC address and how is it structured?**

A **MAC** (Media Access Control) address is a unique, 48-bit physical hardware address burned into a network card, represented as 12 hexadecimal digits (e.g., `00:1A:2B:3C:4D:5E`).

**21. What is the difference between OUI and NIC-specific portions?**

In a 48-bit MAC address, the first 24 bits are the **OUI** (Organizationally Unique Identifier), assigned to the manufacturer (like Cisco or Apple). The last 24 bits are the **NIC** (Network Interface Card) specific portion, which is uniquely assigned by the manufacturer to that specific hardware component.

**22. What are special MAC addresses (broadcast, multicast)?**

*   **Broadcast MAC:** `FF:FF:FF:FF:FF:FF`. Used to send a frame to every single device on the local network segment.
*   **Multicast MAC:** Used to send a frame to a specific group of devices. In IPv4, these always begin with `01:00:5E`.

**23. What is an IPv4 address and its format?**

An **IPv4** (Internet Protocol version 4) address is a 32-bit logical address used to identify devices on a network. It is formatted in "dotted-decimal" notation, broken into four 8-bit octets (e.g., `192.168.1.1`).

**24. What are IP address classes (A, B, C, D, E)?**

Historically, IPv4 addresses were divided into classes based on their leading bits:
*   **Class A:** For massive networks (1.0.0.0 to 126.0.0.0).
*   **Class B:** For medium networks (128.0.0.0 to 191.255.0.0).
*   **Class C:** For small networks (192.0.0.0 to 223.255.255.0).
*   **Class D:** Reserved for Multicasting (224.0.0.0 to 239.255.255.255).
*   **Class E:** Reserved for experimental use (240.0.0.0 to 255.255.255.255).

**25. What are private IP ranges (RFC 1918)?**

**RFC** (Request for Comments) 1918 defines IP addresses reserved for internal use that are not publicly routable on the Internet:
*   Class A: `10.0.0.0` – `10.255.255.255`
*   Class B: `172.16.0.0` – `172.31.255.255`
*   Class C: `192.168.0.0` – `192.168.255.255`

**26. What are special IP addresses (loopback, broadcast)?**

*   **Loopback:** The `127.0.0.0/8` range (most commonly `127.0.0.1`) routes back to the local host; used for testing the local network stack.
*   **Broadcast:** `255.255.255.255` (global broadcast) or the highest address in a specific subnet, used to message all hosts on that network.

**27. What is CIDR notation?**

**CIDR** (Classless Inter-Domain Routing) notation is a compact way of representing an IP address and its subnet mask. It appends a slash and the number of network bits to the IP (e.g., `192.168.1.0/24` means the first 24 bits are the network address).

**28. How to calculate subnets, hosts per subnet, and network ranges?**

We calculate them by looking at the subnet mask (in binary).
*   **Subnets:** Calculated as $2^s$, where *s* is the number of borrowed network bits.
*   **Hosts:** Calculated as $2^h - 2$, where *h* is the number of remaining host bits (subtracting 2 accounts for the network and broadcast addresses).
*   **Network Ranges:** Determined by the "block size" or increment step created by the borrowed bits.

<BR>

**Example:** Let's look at a standard Class C network: `192.168.1.0/24`.
*   The `/24` (CIDR notation) means the first 24 bits are Network bits.
*   That leaves **8 Host bits** (32 total bits - 24 network bits = 8 host bits).
*   In binary, the subnet mask (`255.255.255.0`) looks like this:
    `11111111.11111111.11111111.00000000`

<BR>

**Borrowed Bits (*s*) and Calculating Subnets ($2^s$)**

If we want to divide this single `192.168.1.0` network into smaller networks, we do this by moving the boundary line.  \
We **"borrow"** bits from the Host portion (the zeros) and turn them into Network bits (ones).

Let's say we borrow **2 bits** from the host portion.
*   Our new subnet mask in binary becomes:
    `11111111.11111111.11111111.11000000`
*   In decimal, this new mask is `255.255.255.192` (since the binary `11000000` equals 192).
*   Because we added 2 network bits, our CIDR notation changes from `/24` to **`/26`**.

**How many subnets did we create?**
We use the formula **$2^s$**, where *s* is the number of borrowed bits.
*   We borrowed 2 bits: $2^2 = 4$.
*   By borrowing 2 bits, we sliced our original single network into **4 smaller, equal-sized subnets**.

<BR>

**Host Bits (*h*) and Calculating Hosts per Subnet ($2^h - 2$)**

Now we need to figure out how many devices (hosts) can fit into each of our 4 new subnets. We look at the remaining zeros in our new subnet mask.

Our new mask is: `11111111.11111111.11111111.11000000`
We have **6 remaining Host bits** (the zeros).

**How many hosts per subnet?**

We use the formula **$2^h - 2$**, where *h* is the number of remaining host bits.
*   $2^6 = 64$ total IP addresses per subnet.
*   Now, we must subtract 2: $64 - 2 = 62$ **usable** host IP addresses.

**Why do we subtract 2?**

In every subnet, the very first and very last IP addresses are reserved and cannot be assigned to a computer:
1.  **Network Address (First IP):** Used to identify the subnet itself (all host bits are `0`).
2.  **Broadcast Address (Last IP):** Used to send a message to every device on that specific subnet (all host bits are `1`).

<BR>

**Network Ranges (The "Block Size")**

Finally, we need to know the actual IP ranges for our 4 new subnets. We determine this by finding the "block size" (or increment step).

The block size is simply the total number of IPs in the subnet before we subtract the 2 reserved ones. Since our formula gave us $2^6 = 64$, our block size is **64**.

Starting from 0, we count up by 64 to find our network ranges:

*   **Subnet 1:**
    *   Network ID: `192.168.1.0`
    *   Usable Hosts: `192.168.1.1` to `192.168.1.62` (62 hosts)
    *   Broadcast: `192.168.1.63`
*   **Subnet 2:**
    *   Network ID: `192.168.1.64`
    *   Usable Hosts: `192.168.1.65` to `192.168.1.126` (62 hosts)
    *   Broadcast: `192.168.1.127`
*   **Subnet 3:**
    *   Network ID: `192.168.1.128`
    *   Usable Hosts: `192.168.1.129` to `192.168.1.190` (62 hosts)
    *   Broadcast: `192.168.1.191`
*   **Subnet 4:**
    *   Network ID: `192.168.1.192`
    *   Usable Hosts: `192.168.1.193` to `192.168.1.254` (62 hosts)
    *   Broadcast: `192.168.1.255`

<BR>

**Summary**

* Moving the line to the right (**borrowing bits**) gives us more networks (subnets), but leaves fewer zeros, meaning fewer devices (**hosts**) can fit in each network.
* Moving the line to the left gives us fewer networks, but more devices per network.

<BR>
<BR>


**29. How to perform subnetting manually?**

Manually subnetting involves converting the IP and mask into binary, identifying the default boundary, borrowing bits from the host portion to create sub-networks, and then calculating the new block sizes (increments) in decimal to list out the new network IDs, host ranges, and broadcast addresses.

**30. What is ARP and how does it work?**

**ARP** (Address Resolution Protocol) is used to map a known logical IPv4 address to an unknown physical MAC address. A device broadcasts an ARP Request asking "Who has IP X.X.X.X?", and the device holding that IP responds with an ARP Reply saying "I do, and my MAC is Y:Y:Y:Y".

**31. What are the security concerns with ARP (ARP spoofing)?**

ARP is stateless and lacks authentication. In **ARP Spoofing** (or ARP Poisoning), an attacker sends fake ARP replies claiming that their MAC address is associated with the IP of another device (like the default gateway), allowing them to intercept, alter, or drop network traffic.

**32. Why was IPv6 developed and how does it differ from IPv4?**

**IPv6** (Internet Protocol version 6) was developed because the world ran out of 32-bit IPv4 addresses. It differs by using a 128-bit address space formatted in hexadecimal (e.g., `2001:0db8::1`), offering vastly more addresses, built-in security features (**IPsec** - Internet Protocol Security), and eliminating the need for NAT.

**33. What are well-known ports (0-1023)?**

Well-known ports are managed by **IANA** (Internet Assigned Numbers Authority) and are tightly bound to common, standard system services, such as port 80 for HTTP, 443 for HTTPS, and 22 for SSH.

**34. What are registered ports and dynamic ports?**

*   **Registered Ports (1024-49151):** Listed by IANA for specific user applications or vendor services (like port 3306 for MySQL).
*   **Dynamic / Ephemeral Ports (49152-65535):** Temporarily assigned by an operating system to a client application to be used as the source port for an outbound connection.

**35. What is DHCP and what problem does it solve?**

**DHCP** (Dynamic Host Configuration Protocol) solves the problem of manual IP management. It automatically dynamically assigns IP addresses, subnet masks, gateways, and DNS servers to client devices joining a network.

**36. What is the DORA process (Discover, Offer, Request, Acknowledge)?**

DORA is the 4-step process DHCP uses to assign IPs:
1.  **Discover:** Client broadcasts seeking a DHCP server.
2.  **Offer:** Server replies with an available IP address.
3.  **Request:** Client formally asks to lease the offered IP.
4.  **Acknowledge:** Server confirms the lease and provides network configuration parameters.

**37. What is a DHCP lease and how does renewal work?**

A DHCP lease is the temporary amount of time a device is allowed to use an assigned IP address. When the lease time reaches 50% (half-life), the client sends a unicast request to the server asking to renew the lease and keep the IP.

**38. What are DHCP attacks (Rogue Server, Starvation)?**

*   **Rogue Server:** An attacker places their own DHCP server on the network to hand out malicious configurations (like pointing users to a fake gateway to intercept traffic).
*   **Starvation:** An attacker floods the true DHCP server with thousands of fake MAC addresses to exhaust the pool of available IP addresses, creating a Denial of Service.

**39. What is DHCP Snooping and how does it protect networks?**

DHCP Snooping is a Layer 2 switch security feature that protects against rogue DHCP servers. It defines ports as "trusted" (where real DHCP servers live) and "untrusted" (user ports), blocking any DHCP Offer or Acknowledge messages coming from untrusted ports.

**40. What is NAT and why is it used?**

**NAT** (Network Address Translation) is the process of modifying IP address information in packet headers. It is primarily used to translate non-routable private IP addresses into publicly routable internet IPs, solving the IPv4 exhaustion problem.

**41. What is the difference between Static NAT, Dynamic NAT, and PAT?**

*   **Static NAT:** A strict 1-to-1 mapping of a private IP to a public IP.
*   **Dynamic NAT:** Maps private IPs to a pool of available public IPs on a first-come, first-served basis.
*   **PAT** (Port Address Translation / NAT Overload): Maps multiple private IPs to a *single* public IP by using unique port numbers to keep track of the different sessions.

**42. What is Port Forwarding?**

Port forwarding (or Destination NAT) is a router configuration that intercepts inbound traffic destined for a specific external port and redirects it to a specific internal IP address and port on the private network (often used to host servers behind NAT).

**43. What is NAT Traversal (STUN, TURN, ICE)?**

NAT Traversal techniques help peer-to-peer protocols (like VoIP or video chat) work across NAT gateways:
*   **STUN** (Session Traversal Utilities for NAT): Helps a client discover its public IP and the type of NAT it is behind.
*   **TURN** (Traversal Using Relays around NAT): If STUN fails, TURN relays the traffic through a middleman server.
*   **ICE** (Interactive Connectivity Establishment): A framework that uses both STUN and TURN to find the most efficient path between peers.

**44. What is Carrier-Grade NAT (CGNAT)?**

**CGNAT** (Carrier-Grade NAT) is a large-scale NAT performed by an **ISP** (Internet Service Provider). Because ISPs don't have enough public IPv4 addresses for every customer, they issue private IPs to customers and perform NAT on the ISP end before traffic hits the internet.

**45. What is DNS and how does it work?**

**DNS** (Domain Name System) is the phonebook of the Internet. It translates human-friendly hostnames (like `www.google.com`) into computer-friendly IP addresses (`142.250.190.46`), allowing devices to locate each other over the network.

**46. What is the DNS hierarchy (Root, TLD, Authoritative)?**

*   **Root:** The top of the tree (represented by a dot `.`), directing queries to the appropriate TLD.
*   **TLD** (Top-Level Domain): Defines the extension (like `.com`, `.org`, `.net`) and points to the authoritative servers.
*   **Authoritative:** The final server that holds the actual DNS records and IP address for the specific domain being queried.

**47. What is the DNS resolution process?**

1. The client checks its local cache.
2. If not found, it queries a Recursive Resolver (usually via the ISP).
3. The resolver queries the Root server, which refers it to the TLD server.
4. The TLD server refers it to the Authoritative server.
5. The Authoritative server returns the IP, which the resolver caches and hands back to the client.

**48. What are the main DNS record types (A, AAAA, CNAME, MX, NS, TXT, PTR)?**

*   **A:** Maps a hostname to an IPv4 address.
*   **AAAA:** Maps a hostname to an IPv6 address.
*   **CNAME** (Canonical Name): Maps a hostname to another hostname (an alias).
*   **MX** (Mail Exchange): Specifies the mail servers responsible for accepting emails for the domain.
*   **NS** (Name Server): Indicates which DNS servers are authoritative for the domain.
*   **TXT** (Text): Allows administrators to insert arbitrary text into DNS (often used for email security like SPF/DKIM).
*   **PTR** (Pointer): Used for reverse lookups, mapping an IP address back to a hostname.

**49. What are DNS security threats (Spoofing, Hijacking, Tunneling)?**

*   **Spoofing (Cache Poisoning):** Injecting forged DNS data into a resolver's cache so users are redirected to malicious sites.
*   **Hijacking:** Taking over the domain registration or authoritative server to alter records at the source.
*   **Tunneling:** Encapsulating non-DNS traffic (like malware command-and-control data) inside DNS queries to bypass firewall restrictions.

**50. What is DNSSEC and encrypted DNS (DoH, DoT)?**

*   **DNSSEC** (Domain Name System Security Extensions): Adds cryptographic signatures to DNS records to ensure they haven't been tampered with (protects against spoofing).
*   **DoH** (DNS over HTTPS) and **DoT** (DNS over TLS): Encrypt DNS queries so ISPs and eavesdroppers cannot see which websites a user is trying to visit. (TLS: Transport Layer Security).

**51. Authentication & Directory Services**

*(Note: Category header, included for completeness).*

**52. What is RADIUS and how does it work?**

**RADIUS** (Remote Authentication Dial-In User Service) is a client/server protocol providing centralized **AAA** (Authentication, Authorization, Accounting). When a user connects to a network device (like a Wi-Fi router), the router forwards the credentials to a centralized RADIUS server to verify if access should be granted.

**53. What is TACACS+ and how does it differ from RADIUS?**

**TACACS+** (Terminal Access Controller Access-Control System Plus) is a Cisco proprietary AAA protocol. It differs from RADIUS by encrypting the *entire* payload (RADIUS only encrypts the password), using TCP instead of UDP, and cleanly separating Authentication, Authorization, and Accounting into distinct processes.

**54. What is Kerberos and what attacks target it?**

Kerberos is a network authentication protocol that uses tickets to prove user identity securely without sending passwords over the network. Common attacks against it include **Pass-the-Ticket** (stealing tickets from memory), **Golden Ticket** (forging a master ticket), and **Kerberoasting** (extracting service account hashes from ticket grants to crack offline).

**55. What is LDAP and how is it used in networks?**

**LDAP** (Lightweight Directory Access Protocol) is an open protocol used for accessing and maintaining distributed directory information. It is commonly used to query and manage users, groups, and permissions within Microsoft Active Directory.

**56. Why is NTP important for security?**

**NTP** (Network Time Protocol) synchronizes clocks across network devices. It is crucial for security because cryptographic certificates rely on accurate timestamps for validity, and security logs must be perfectly synchronized to track an attacker's actions during an incident investigation.

**57. What is Syslog and its severity levels?**

Syslog is a standard protocol used to send event log messages to a centralized logging server. Its severity levels range from 0 to 7: 0 (Emergency), 1 (Alert), 2 (Critical), 3 (Error), 4 (Warning), 5 (Notice), 6 (Informational), and 7 (Debug).

**58. What is an Autonomous System (AS) and ASN?**

An **AS** (Autonomous System) is a large network or group of networks sharing a single routing policy, typically operated by an ISP or a massive tech enterprise. An **ASN** (Autonomous System Number) is a globally unique number assigned to an AS to identify it on the Internet.

**59. What is BGP and how does it work?**

**BGP** (Border Gateway Protocol) is the routing protocol of the Internet. It exchanges routing and reachability information between different Autonomous Systems, finding the most efficient path for data to travel across the globe based on network policies and rules.

**60. What are BGP hijacking attacks?**

BGP hijacking occurs when a malicious or misconfigured Autonomous System falsely announces that it owns a specific block of IP addresses. This tricks global routers into sending traffic destined for those IPs to the hijacker instead, allowing them to blackhole (drop) or intercept the data.

**61. What is peering vs transit?**

*   **Peering:** A mutual agreement between two networks to exchange data directly and for free, benefiting both parties.
*   **Transit:** A business agreement where a smaller network pays a larger ISP for access to the rest of the Internet.

**62. What is an Internet Exchange Point (IXP)?**

An **IXP** (Internet Exchange Point) is a physical location where ISPs, CDNs, and other large network providers connect their infrastructure to peer directly with one another, reducing transit costs and improving network performance.

**63. What is a CDN and how does Anycast work?**

A **CDN** (Content Delivery Network) is a geographically distributed group of servers that caches content close to end-users to speed up web delivery. **Anycast** is a network routing methodology where multiple servers in different physical locations share the exact same IP address; BGP routing automatically sends the user to the server physically closest to them.

**64. What are the Wi-Fi frequency bands (2.4 GHz, 5 GHz, 6 GHz)?**

*   **2.4 GHz:** Older, has longer range and penetrates walls well, but is slow and highly congested.
*   **5 GHz:** Faster and less congested, but has a shorter range and struggles to penetrate solid objects.
*   **6 GHz:** The newest band (Wi-Fi 6E), offering massive amounts of spectrum for gigabit speeds with virtually no congestion, but at the shortest range.

**65. What are the Wi-Fi standards (802.11a/b/g/n/ac/ax)?**

These are IEEE standards dictating wireless speeds and technologies:
*   **802.11a/b/g:** Legacy standards (very slow).
*   **802.11n (Wi-Fi 4):** Introduced MIMO (Multiple Input, Multiple Output).
*   **802.11ac (Wi-Fi 5):** Operates only on 5 GHz, significantly faster.
*   **802.11ax (Wi-Fi 6/6E):** Highly efficient, faster, supports 2.4, 5, and 6 GHz bands.

**66. What is the difference between WEP, WPA, WPA2, WPA3?**

*   **WEP** (Wired Equivalent Privacy): Obsolete and easily cracked in minutes.
*   **WPA** (Wi-Fi Protected Access): Replaced WEP but still vulnerable.
*   **WPA2:** Current standard for most devices; uses **AES** (Advanced Encryption Standard) but is vulnerable to KRACK attacks.
*   **WPA3:** Latest standard; protects against brute-force dictionary attacks by using **SAE** (Simultaneous Authentication of Equals).

**67. What are common wireless attacks (Evil Twin, Deauth, KRACK)?**

*   **Evil Twin:** A malicious access point set up to mimic a legitimate network to steal credentials.
*   **Deauth** (Deauthentication): Sending forged frames to forcibly disconnect a user from their access point.
*   **KRACK** (Key Reinstallation Attacks): An exploit targeting the WPA2 4-way handshake to decrypt wireless traffic.

**68. What are wireless security best practices?**

Best practices include using WPA3 (or WPA2-AES at minimum), employing strong and long passphrases, isolating guest networks, utilizing 802.1X Enterprise authentication, hiding the SSID (less effective but adds obscurity), and disabling **WPS** (Wi-Fi Protected Setup) which is highly vulnerable.

**69. What is the difference between PSK and Enterprise authentication?**

**PSK** (Pre-Shared Key) uses a single password that everyone shares to connect to the Wi-Fi. **Enterprise** authentication uses the 802.1X standard, where every user has their own unique username and password (validated against a RADIUS server) to connect.

**70. What is the CIA Triad (Confidentiality, Integrity, Availability)?**

The CIA Triad is the core foundational model of information security:
*   **Confidentiality:** Keeping data hidden from unauthorized entities (encryption).
*   **Integrity:** Ensuring data has not been altered or tampered with (hashing).
*   **Availability:** Ensuring data and systems are accessible when needed by authorized users (redundancy).

**71. What is Defense in Depth?**

Defense in Depth is an approach to cybersecurity where multiple layers of security controls (e.g., firewalls, antivirus, strict access controls, user training) are placed throughout an IT system. If one layer fails, another layer catches the threat.

**72. What are the key security principles (Least Privilege, Zero Trust)?**

*   **Least Privilege:** Granting users or systems only the bare minimum permissions necessary to do their job.
*   **Zero Trust:** A security framework based on the premise "never trust, always verify"—no device or user is trusted by default, even if they are already inside the corporate network.

**73. What is AAA (Authentication, Authorization, Accounting)?**

*   **Authentication:** Verifying who you are (e.g., checking a password).
*   **Authorization:** Determining what you are allowed to do (e.g., file permissions).
*   **Accounting:** Logging and tracking what you actually did (e.g., audit trails).

**74. What are the main attack categories (Reconnaissance, Interception, DoS)?**

*   **Reconnaissance:** Attackers passively or actively gather information about a network to plan an attack (e.g., port scanning).
*   **Interception:** Attackers capture data as it travels across the network (e.g., packet sniffing, Man-in-the-Middle).
*   **DoS** (Denial of Service): Attackers overwhelm a system, rendering it unavailable to legitimate users.

**75. What is a Man-in-the-Middle (MitM) attack?**

A MitM attack occurs when an attacker secretly intercepts and relays communications between two parties who believe they are communicating directly with each other. The attacker can eavesdrop on or alter the data in transit.

**76. What are DDoS attacks (Volumetric, Protocol, Application)?**

**DDoS** (Distributed Denial of Service) uses multiple compromised devices to attack a target.
*   **Volumetric:** Overwhelms the target's total bandwidth (e.g., amplification attacks).
*   **Protocol:** Exploits weaknesses in Layer 3/4 network protocols to exhaust server resources (e.g., SYN floods).
*   **Application:** Targets Layer 7 applications with seemingly legitimate but resource-heavy requests (e.g., HTTP GET floods).

**77. What are common password attacks?**

*   **Brute-Force:** Trying every possible combination of characters.
*   **Dictionary Attack:** Trying a list of common words or previously breached passwords.
*   **Credential Stuffing:** Using passwords stolen from one site to log into another site.
*   **Password Spraying:** Trying one common password (like "Password123") against many different user accounts to avoid lockouts.

**78. What are the types of firewalls (Packet Filtering, Stateful, NGFW)?**

*   **Packet Filtering:** A stateless firewall that looks only at basic headers (IP/Port) without understanding the context of the connection.
*   **Stateful Firewall:** Keeps track of the state of active network connections and makes decisions based on the context of the traffic flow.
*   **NGFW** (Next-Generation Firewall): Combines stateful inspection with advanced features like **DPI** (Deep Packet Inspection), application awareness, and built-in Intrusion Prevention Systems.

**79. How to write firewall rules?**

Firewall rules (or ACLs - Access Control Lists) are generally written based on variables: Source IP, Destination IP, Protocol (TCP/UDP), Destination Port, and Action (Allow or Deny). They are processed sequentially from top to bottom, ending in an "Implicit Deny All" rule that drops anything not explicitly allowed.

**80. What is a DMZ?**

A **DMZ** (Demilitarized Zone) is an isolated subnet that sits between a trusted internal network and an untrusted external network (the Internet). Public-facing services (like web and email servers) are placed in the DMZ so that if they are compromised, the attacker still cannot access the internal network.

**81. What is the difference between IDS and IPS?**

An **IDS** (Intrusion Detection System) sits out-of-band and passively monitors network traffic, generating alerts when suspicious activity is found. An **IPS** (Intrusion Prevention System) sits inline with the traffic flow and actively blocks or drops malicious packets before they reach their destination.

**82. What are detection methods (Signature, Anomaly, Heuristic)?**

*   **Signature-based:** Compares traffic against a database of known malware/attack patterns.
*   **Anomaly-based:** Establishes a baseline of "normal" behavior and alerts when traffic drastically deviates from it.
*   **Heuristic-based:** Uses algorithms and rules to identify malicious characteristics, helping detect brand new, previously unseen attacks (zero-days).

**83. What is network segmentation and why is it important?**

Network segmentation is the practice of splitting a large network into smaller, isolated subnetworks (often using VLANs and firewalls). It is important because it stops threats from spreading freely across the entire organization (limiting lateral movement) and protects sensitive data.

**84. What is Zero Trust architecture?**

Zero Trust architecture removes the concept of a "trusted internal network." It requires strict identity verification, device health checks, and continuous authorization for every person and device trying to access network resources, regardless of whether they are sitting at a desk in the office or connecting remotely.

**85. What is a SIEM and what logs should be monitored?**

A **SIEM** (Security Information and Event Management) system centralizes, correlates, and analyzes log data from across the enterprise. Critical logs to monitor include firewall allows/denies, domain controller authentication attempts (successes and failures), VPN logins, and antivirus/Endpoint Detection logs.

**86. What is NAC (Network Access Control)?**

**NAC** (Network Access Control) is a system that evaluates devices before they are allowed onto a network. If a device fails security policies (e.g., missing antivirus updates or unauthorized MAC address), the NAC blocks it or places it into a restricted quarantine VLAN.

**87. What is 802.1X authentication and the EAP methods?**

**802.1X** is an IEEE standard for port-based network access control, authenticating devices via a switch/access point communicating with a RADIUS server. It utilizes **EAP** (Extensible Authentication Protocol) methods, such as **EAP-TLS** (Transport Layer Security, using client/server certificates) or **PEAP** (Protected EAP, wrapping username/password in a secure tunnel).

**88. What are the types of port scans (TCP Connect, SYN, UDP)?**

*   **TCP Connect Scan:** Completes the entire 3-way handshake; highly reliable but very noisy and easily logged.
*   **SYN Scan:** (Stealth scan) Sends a SYN packet but tears down the connection before it completes, making it faster and harder for older firewalls to log.
*   **UDP Scan:** Sends empty UDP packets and relies on ICMP (Internet Control Message Protocol) "Port Unreachable" error messages to determine if a port is closed.

**89. What are the port states (Open, Closed, Filtered)?**

When scanning a network, scanning tools (like Nmap) report:
*   **Open:** An application is actively listening for connections on that port.
*   **Closed:** The port is accessible, but no application is actively listening on it.
*   **Filtered:** A firewall or network obstacle is dropping the scan packets, so the scanner cannot determine if the port is open or closed.

**90. What protocols are used for network enumeration (SNMP, NetBIOS, SMB, LDAP)?**

Attackers and admins use protocols to gather detailed network data:
*   **SNMP** (Simple Network Management Protocol): Can reveal routing tables, device statistics, and system details.
*   **NetBIOS** (Network Basic Input/Output System): Can reveal Windows domain details and hostnames.
*   **SMB** (Server Message Block): Can enumerate shared folders, files, and users.
*   **LDAP** (Lightweight Directory Access Protocol): Can extract massive amounts of user, group, and organizational data from Active Directory.

**91. How to defend against reconnaissance?**

To defend against network reconnaissance, organizations should employ strict firewall rules to block unnecessary inbound traffic, disable unused services and open ports, utilize an IPS (Intrusion Prevention System) to detect and block port scanning behavior, implement rate-limiting, and ensure protocols like SNMP and SMB use secure configurations (e.g., SNMPv3) or are blocked from external access.
