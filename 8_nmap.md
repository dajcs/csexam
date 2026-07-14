# Nmap Live Host Discovery


**01. What is nmap.**

Nmap (Network Mapper) is a free, open-source command-line tool used to discover hosts and services on a computer network. It sends specially crafted packets to targets and analyzes the responses to build a map of what's alive on the network, what ports are open, what services are running, and often what operating system a host is using. It's a staple in network administration, security auditing, and penetration testing.

**02. How to use nmap.**

The basic syntax is `nmap [scan type] [options] {target}`. The target can be a single IP (Internet Protocol) address, a hostname, a range, or a whole subnet. For example, `nmap scanme.nmap.org` runs a default scan against that host, while `nmap -sV -p 1-1000 192.168.1.10` scans ports 1 through 1000 and attempts service/version detection. Many scan types require root/administrator privileges (run with `sudo` on Linux) because they craft raw packets. Nmap also ships with a graphical front-end called `Zenmap`.

**03. How does nmap scan work**

An Nmap (Network Mapper) scan works by sending specially crafted packets to a target host and analyzing the responses. Depending on the scan type, it sends TCP (Transmission Control Protocol), UDP (User Datagram Protocol), or ICMP (Internet Control Message Protocol) packets to specific ports or addresses. It then infers the state of the port (e.g., open, closed, filtered) or the presence of an active host based on the flags in the return packets or the lack of a response.  \
A scan typically has stages: host discovery (deciding which hosts are online), port scanning (probing ports to see which are open, closed, or filtered), and optional deeper steps like service/version detection and OS (Operating System) fingerprinting. It relies on the expected behavior of network protocols — for instance, the TCP (Transmission Control Protocol) three-way handshake — so that the way a target responds (or fails to respond) reveals the state of a port or host.

**04. What is Subnetworks.**

A subnetwork (subnet) is a logical subdivision of a larger IP (Internet Protocol) network. Subnetting splits a big network into smaller ones to improve organization, performance, and security. Subnets are written in CIDR (Classless Inter-Domain Routing) notation, such as `192.168.1.0/24`, where the `/24` indicates how many bits form the network portion of the address (here, 24 bits, leaving 256 addresses). Nmap can scan an entire subnet at once, e.g. `nmap 192.168.1.0/24`.

**05. How to enumerate Targets.**

Enumerating targets means telling nmap which hosts to scan. You can do this by listing individual IP (Internet Protocol) addresses (`nmap 10.0.0.1 10.0.0.2`), using CIDR (Classless Inter-Domain Routing) ranges (`nmap 10.0.0.0/24`), using octet ranges (`nmap 10.0.0.1-50`), using wildcards (`nmap 10.0.0.*`), or supplying a file with `-iL targets.txt`. The `-sL` (list scan) option simply lists the targets nmap would scan without actually sending packets, and `-sn` performs host discovery only.

**06. What is ARP Scan**

An ARP (Address Resolution Protocol) scan discovers live hosts on a local network segment by sending ARP requests. ARP maps IP (Internet Protocol) addresses to MAC (Media Access Control) hardware addresses. ARP is a broadcast on a local Ethernet/LAN (Local Area Network). Any host that is up and has the queryed IP, must answer an ARP request with its MAC address, so this is the fastest and most reliable way to find live hosts on the same subnet. Nmap uses ARP scanning automatically for local targets; you can force it with `-PR`.

**07. What is ICMP Echo Scan**

An ICMP (Internet Control Message Protocol) Echo scan sends ICMP Echo Request packets (Type 8, the same type used by the `ping` command) to targets. A host that replies with an ICMP Echo Reply (Type 0) is considered up. This is classic "ping" host discovery. In nmap it's invoked with `-PE`. Its limitation is that many firewalls block ICMP Echo, so an unanswered probe doesn't always mean the host is down.

**08. What is ICMP Timestamp Scan**

An ICMP (Internet Control Message Protocol) Timestamp scan is another host discovery method. It sends an ICMP Type 13 (Timestamp Request) packet to the target. If the host is alive, it replies with an ICMP Type 14 (Timestamp Reply) packet. This is highly useful when network administrators block standard ICMP Echo requests but forget to block ICMP Timestamp requests. In Nmap (Network Mapper), this is invoked with the `-PP` option.

**09. What is ICMP Address Mask Scan**

An ICMP (Internet Control Message Protocol) Address Mask scan is a host discovery technique that sends an ICMP Type 17 (Address Mask Request) packet to the target, querying it for its subnet mask. If the host responds, it sends back an ICMP Type 18 (Address Mask Reply) packet. Like the timestamp scan, this is an alternative way to discover active hosts that might be blocking standard ping requests. In Nmap (Network Mapper), this is executed via the `-PM` option.

**10. What is TCP SYN Ping Scan**

A TCP (Transmission Control Protocol) SYN (Synchronize) Ping scan is a host discovery technique that sends an empty TCP packet with the SYN (Synchronize) flag set to a specific port (usually port 80 or 443). If the host is online, it will typically respond with a SYN/ACK (Synchronize/Acknowledgment) packet if the port is open, or an RST (Reset) packet if the port is closed. Either response proves to Nmap (Network Mapper) that the host is active. Because it doesn't complete the full handshake, it's lightweight. In nmap it's invoked with `-PS`, optionally followed by port numbers, e.g. `-PS22,80,443`.

**11. What is TCP ACK Ping Scan**

A TCP (Transmission Control Protocol) ACK (Acknowledgment) Ping scan sends an empty TCP packet with only the ACK (Acknowledgment) flag set. To the target host, this looks like an acknowledgment for a connection that does not actually exist, so the host responds with an RST (Reset) packet. Receiving this RST packet confirms to Nmap (Network Mapper) that the host is active. This scan is useful when some simple, stateless firewalls block SYN (Synchronize) probes but allow ACK packets through. In nmap it's invoked with `-PA`.

**12. What is UDP Ping Scan**

A UDP (User Datagram Protocol) Ping scan sends an empty UDP packet to specific ports (Nmap defaults to port 40125 if no port is specified) to check if a host is alive. If the host is up but the port is closed, it will return an ICMP (Internet Control Message Protocol) Port Unreachable error message. Receiving this error lets Nmap (Network Mapper) know the host is active. This is useful for bypassing firewalls that heavily filter TCP (Transmission Control Protocol) and ICMP traffic. In Nmap, this is triggered with the `-PU` option.

**13. What can nmap detect**

Nmap (Network Mapper) can detect a wide variety of information about a network and its endpoints. This includes:
*   Active hosts (Host discovery).
*   Open, closed, or filtered ports (Port scanning).
*   Applications running on those ports and their versions  (with `-sV`).
*   The OS (Operating System) running on the target host (with `-O`).
*   MAC (Media Access Control) addresses and hardware vendors (only on local networks).
*   Vulnerabilities, misconfigurations, available shares and extended network data using the NSE (Nmap Scripting Engine). Invoked with `-sC` or `--script`.

**14. How to scan an IP address with nmap.**

To scan a single IP (Internet Protocol) address, run `nmap <ip>`, for example `nmap 192.168.1.10`. This runs nmap's default scan (a TCP (Transmission Control Protocol) SYN scan of the 1,000 most common ports when run as root). You can add options for more depth: `nmap -A 192.168.1.10` enables OS (Operating System) detection, version detection, script scanning, and traceroute in one command. To just check whether the host is up without port scanning, use `nmap -sn 192.168.1.10`.

**15. How to check ports with nmap.**

To check specific ports on a target using Nmap (Network Mapper), use the `-p` option followed by the port number or range.
*   **Single port:** `nmap -p 80 192.168.1.100` (Scans only port 80).
*   **Multiple ports:** `nmap -p 80,443,22 192.168.1.100`.
*   **Port range:** `nmap -p 1-1000 192.168.1.100`.
*   **All ports:** `nmap -p- 192.168.1.100` (Scans all 65,535 ports).
*   **Top ports:** `nmap --top-ports 1000 192.168.1.100` (Scans the top 1000 most common ports).
*   **Fast scan:** `nmap -F 192.168.1.100` (Scans the 100 most common ports quickly).
*   **Service/version detection:** `nmap -sV -p 80,443 192.168.1.100` (Detects services and versions on specified ports).

By default, Nmap uses a TCP (Transmission Control Protocol) scan, but you can specify UDP (User Datagram Protocol) ports by using the `-sU` flag and prefixing the port with `U:` (e.g., `nmap -sU -p U:53 192.168.1.100`).
