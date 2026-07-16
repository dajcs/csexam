# Nmap Live Host Discovery


**01. What is nmap.**

- Nmap (Network Mapper) is a free, open-source command-line tool used for network discovery and security auditing.
- It sends specially crafted packets to hosts and analyzes the responses to build a picture of a network.
- It is commonly used to discover which hosts are alive on a network, which ports are open, which services (and versions) those ports run, and which operating systems the hosts use.
- It is widely used by network administrators for inventory and monitoring, and by security professionals for penetration testing and vulnerability assessment.
- It includes the NSE (Nmap Scripting Engine), which lets users run scripts to automate advanced tasks such as vulnerability detection and service enumeration.


**02. How to use nmap.**

- The basic syntax is: `nmap [scan type(s)] [options] {target}`.
- The target can be a single IP address, a hostname, a range, or a whole subnetwork – for example:
  - `nmap 192.168.1.1` – scan a single host.
  - `nmap scanme.nmap.org` – scan by hostname.
  - `nmap 192.168.1.1-50` – scan a range of addresses.
  - `nmap 192.168.1.0/24` – scan an entire subnetwork using CIDR (Classless Inter-Domain Routing) notation.
- Common options include:
  - `-sS` – TCP (Transmission Control Protocol) SYN scan.
  - `-sV` – detect service and version information.
  - `-O` – enable OS (Operating System) detection.
  - `-p` – specify ports, e.g. `-p 80,443` or `-p 1-65535`.
  - `-A` – aggressive scan (OS detection, version detection, script scanning, and traceroute).
  - `-v` – increase verbosity of the output.
- Many scan types require elevated privileges, so they are often run with `sudo` on Linux/macOS (e.g. `sudo nmap -sS 192.168.1.1`).
- Nmap also ships with a graphical front-end called `Zenmap`.

**03. How does nmap scan work**


- Nmap works by sending network packets to a target and interpreting the responses that come back.
- The general workflow is:
  - **Host discovery** – determine which hosts are online (also called a "ping scan"), typically using ARP (Address Resolution Protocol), ICMP (Internet Control Message Protocol), TCP, or UDP (User Datagram Protocol) probes.
  - **Port scanning** – probe the discovered hosts to classify ports as open, closed, or filtered based on the responses.
  - **Service/version detection** – send additional probes to identify the application and version listening on open ports.
  - **OS detection** – analyze subtle differences in the target's TCP/IP (Transmission Control Protocol / Internet Protocol) stack behavior to guess the operating system.
  - **Scripting (optional)** – run NSE (Nmap Scripting Engine) scripts for deeper enumeration or vulnerability checks.
- Port states are inferred from responses; for example, in a TCP SYN scan a SYN-ACK reply indicates an open port, a RST (reset) indicates a closed port, and no response (or an ICMP unreachable error) suggests a filtered port.

**04. What is Subnetworks.**

- A subnetwork (subnet) is a logical subdivision of a larger IP (Internet Protocol) network.
- Subnetting splits a big network into smaller, more manageable segments, which improves performance, organization, and security.
- A subnet is defined by an IP address together with a subnet mask (or CIDR – Classless Inter-Domain Routing – prefix), which separates the address into a network portion and a host portion.
- Example: `192.168.1.0/24` describes a subnet where the first 24 bits identify the network and the remaining 8 bits identify individual hosts – giving 256 total addresses (254 usable for hosts).
- In nmap, you can scan an entire subnet at once using CIDR notation, e.g. `nmap 192.168.1.0/24`.

**05. How to enumerate Targets.**

- Enumerating targets means specifying which hosts nmap should scan. Nmap supports several formats:
  - **Single IP or hostname** – `nmap 192.168.1.1` or `nmap example.com`.
  - **Multiple hosts** – list them separated by spaces, e.g. `nmap 192.168.1.1 192.168.1.2`.
  - **IP range** – `nmap 192.168.1.1-100` scans `.1` through `.100`.
  - **CIDR (Classless Inter-Domain Routing) notation** – `nmap 192.168.1.0/24` scans a whole subnet.
  - **Wildcards / octet ranges** – `nmap 192.168.1.*` or `nmap 192.168.0-5.1-254`.
  - **Input from a file** – `nmap -iL targets.txt` reads a list of targets from a file.
  - **Random targets** – `nmap -iR 100` picks 100 random hosts (used for internet-wide research, with care).
- You can also **exclude** hosts using `--exclude 192.168.1.5` or `--excludefile exclude.txt`.
- To only list the targets to be tested but without actually scanning them, use `-sL` (list scan).

**06. What is ARP Scan**

- ARP (Address Resolution Protocol) scan is a host-discovery technique used on a local network (the same broadcast domain / subnet).
- It sends ARP request packets asking "who has this IP address?" – any host that owns the address replies with its MAC (Media Access Control) address.
- Because ARP operates at the data-link layer and every live host on the local segment must respond to be reachable, it is the fastest and most reliable way to find hosts on a local network.
- Nmap automatically uses ARP scanning for local-network targets when run with sufficient privileges; you can force it with `-PR`.
- ARP scanning cannot cross routers, so it only works within the local subnet, not for remote networks.

**07. What is ICMP Echo Scan**

- ICMP (Internet Control Message Protocol) Echo scan discovers live hosts by sending ICMP Echo Request messages – the same mechanism used by the `ping` command.
- A host that is up and not filtering ICMP replies with an ICMP Echo Reply, confirming it is online.
- In nmap it is enabled with the `-PE` option.
- It is simple and fast, but many firewalls and hosts block or drop ICMP Echo Requests, so a lack of reply does not always mean the host is down.

**08. What is ICMP Timestamp Scan**

- ICMP (Internet Control Message Protocol) Timestamp scan sends an ICMP Timestamp Request message to a target.
- A responsive host replies with an ICMP Timestamp Reply, which both confirms the host is alive and can reveal the target's system clock/time information.
- In nmap it is enabled with the `-PP` option.
- It is useful as an alternative host-discovery method when standard ICMP Echo (ping) requests are filtered, because some firewalls block Echo but still allow Timestamp messages.

**09. What is ICMP Address Mask Scan**

- ICMP (Internet Control Message Protocol) Address Mask scan sends an ICMP Address Mask Request to a target.
- A responsive host may reply with an ICMP Address Mask Reply, indicating it is alive and potentially revealing the subnet mask used on that network.
- In nmap it is enabled with the `-PM` option.
- Like the timestamp scan, it is used as a fallback host-discovery method when Echo requests are blocked; however, most modern systems ignore these requests, so it is often less effective.

**10. What is TCP SYN Ping Scan**

- TCP (Transmission Control Protocol) SYN Ping scan is a host-discovery method that sends a TCP packet with the SYN (synchronize) flag set to a specified port.
- If the port is open, the target replies with a SYN-ACK (synchronize-acknowledge); if closed, it replies with a RST (reset). Either response proves the host is alive.
- In nmap it is enabled with `-PS`, optionally followed by port numbers, e.g. `-PS80,443`.
- It is effective for finding hosts that block ICMP (Internet Control Message Protocol) pings, because it uses TCP traffic that firewalls often allow (for example, to web ports 80 and 443).

**11. What is TCP ACK Ping Scan**

- TCP (Transmission Control Protocol) ACK Ping scan sends a TCP packet with the ACK (acknowledge) flag set to a target port.
- Since there is no established connection, a live host responds with a RST (reset) packet, which confirms the host is up.
- In nmap it is enabled with `-PA`, optionally with port numbers, e.g. `-PA80`.
- It is designed to bypass certain firewalls: stateless firewalls that filter incoming SYN packets may still allow ACK packets, so this method can detect hosts the SYN ping would miss (and vice versa).

**12. What is UDP Ping Scan**

- UDP (User Datagram Protocol) Ping scan discovers hosts by sending a UDP packet to a specified port.
- If the target port is closed, the host typically responds with an ICMP (Internet Control Message Protocol) "port unreachable" message, which confirms the host is alive.
- In nmap it is enabled with `-PU`, optionally with port numbers, e.g. `-PU53`.
- It is useful for finding hosts protected by firewalls that filter TCP (Transmission Control Protocol) probes but overlook UDP traffic; it is often aimed at ports that are usually closed to reliably trigger the "unreachable" response.

**13. What can nmap detect**

Nmap can detect a wide range of information about a network and its hosts, including:
  - **Live hosts** — which machines are online (host discovery).
  - **Open ports** — which TCP (Transmission Control Protocol) and UDP (User Datagram Protocol) ports are open, closed, or filtered.
  - **Services** — which network services are running on those ports (e.g. HTTP — HyperText Transfer Protocol, SSH — Secure Shell, FTP — File Transfer Protocol).
  - **Service versions** — the specific software and version number of running services (with `-sV`).
  - **Operating system** — the likely OS (Operating System) and device type via TCP/IP stack fingerprinting (with `-O`).
  - **Firewall/filter presence** — whether packets are being filtered or a firewall is in place.
  - **Network topology** — hops to the target via traceroute (with `--traceroute`).
  - **Vulnerabilities and extra details** — through NSE (Nmap Scripting Engine) scripts, including misconfigurations, exposed information, and known vulnerabilities.
  - **MAC addresses and vendors** — hardware addresses of local hosts and their manufacturers.

**14. How to scan an IP address with nmap.**

- To scan a single IP (Internet Protocol) address, provide it as the target:
  - `nmap 192.168.1.10` — a default scan of the most common 1,000 TCP (Transmission Control Protocol) ports.
- Useful variations:
  - `nmap -sV 192.168.1.10` — also identify service and version information.
  - `nmap -O 192.168.1.10` — attempt OS (Operating System) detection.
  - `nmap -A 192.168.1.10` — aggressive scan combining OS detection, version detection, script scanning, and traceroute.
  - `sudo nmap -sS 192.168.1.10` — a stealthier TCP SYN scan (needs elevated privileges).
  - `nmap -p- 192.168.1.10` — scan all 65,535 ports rather than just the common ones.
- Add `-v` for more verbose output, and `-oN result.txt` to save the results to a file.

**15. How to check ports with nmap.**

- Nmap checks ports as part of its scanning; you control which ports are examined with the `-p` option:
  - `nmap -p 80 192.168.1.10` — check a single port (port 80).
  - `nmap -p 80,443,22 192.168.1.10` — check a specific list of ports.
  - `nmap -p 1-1000 192.168.1.10` — check a range of ports.
  - `nmap -p- 192.168.1.10` — check all 65,535 ports.
  - `nmap -F 192.168.1.10` — fast scan of the 100 most common ports.
  - `nmap --top-ports 20 192.168.1.10` — check the 20 most commonly used ports.
- To specify protocol, prefix ports with `T:` for TCP (Transmission Control Protocol) or `U:` for UDP (User Datagram Protocol), e.g. `nmap -p T:80,U:53 192.168.1.10`.
- Each scanned port is reported with a **state**:
  - **open** — an application is actively accepting connections on that port.
  - **closed** — the port is reachable but no application is listening.
  - **filtered** — a firewall or filter is blocking the probe, so nmap cannot determine whether it is open.
  - **unfiltered**, **open|filtered**, **closed|filtered** — additional states used when the result is ambiguous.
