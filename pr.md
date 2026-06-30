# Passive Reconnaissance





**01. What can we learn about a `Server`**

A server is a computer system or program that provides resources, data, services, or programs to other computers, known as clients, over a network. By investigating a server, we can learn its IP (Internet Protocol) address, its OS (Operating System), its geographic location, which ports are open, what software applications and versions it is running, and its general role in the network (e.g., a web server, database server, or email server).

**02. What is a `DNS server`**

A DNS (Domain Name System) server is a computer server that contains a database of public IP (Internet Protocol) addresses and their associated hostnames. Its primary purpose is to translate or "resolve" human-readable domain names (like google.com) into the numerical IP (Internet Protocol) addresses that computers and routers use to identify and route traffic to each other across the Internet.

**03. What happens when we type `www.holbertonschool.com` and press `ENTER`**

When you type a URL (Uniform Resource Locator) and press ENTER, a sequence of events occurs:
1. Your web browser checks its local cache for the DNS (Domain Name System) record to find the IP (Internet Protocol) address of `www.holbertonschool.com`.
2. If not found, the OS (Operating System) checks its cache, and then queries the configured DNS (Domain Name System) server (usually provided by your ISP — Internet Service Provider) to resolve the domain to an IP (Internet Protocol) address.
3. Once the IP (Internet Protocol) address is identified, the browser initiates a TCP (Transmission Control Protocol) handshake with the server to establish a network connection.
4. If the connection is secure, a TLS (Transport Layer Security) or SSL (Secure Sockets Layer) handshake occurs to encrypt the communication.
5. The browser sends an HTTP (Hypertext Transfer Protocol) or HTTPS (Hypertext Transfer Protocol Secure) GET request to the server, asking for the webpage data.
6. The server processes the request and sends back an HTTP (Hypertext Transfer Protocol) response containing the website data, usually in HTML (Hypertext Markup Language) format, along with CSS (Cascading Style Sheets) and JS (JavaScript).
7. Finally, your browser parses and renders the HTML (Hypertext Markup Language) and displays the webpage to you.

**04. How can we find the owner information for a `domain name`**

We can find the owner information by using a WHOIS (Who Is) lookup tool. The WHOIS service queries databases maintained by domain registrars and registries to retrieve the registration details of an internet resource. These details often include the registrant's name, organization, contact information, registration and expiration dates, and the associated NS (Name Servers). We can also use lookup tools provided directly by ICANN (Internet Corporation for Assigned Names and Numbers). *Note: Due to modern privacy protection services, some of this PII (Personally Identifiable Information) may be redacted.*

**05. What is `dig`**

`dig` stands for Domain Information Groper. It is a flexible, command-line network administration tool used for querying DNS (Domain Name System) name servers. It is heavily utilized by network administrators and security professionals to troubleshoot DNS (Domain Name System) issues, verify records, and perform lookups because it provides highly detailed output and is very reliable.

**06. What is `nslookup`**

`nslookup` stands for Name Server Lookup. It is a command-line tool available on most OS (Operating Systems) used to query the DNS (Domain Name System) to obtain the mapping between a domain name and an IP (Internet Protocol) address, or to retrieve other specific DNS (Domain Name System) records. While `dig` (Domain Information Groper) is generally preferred on Linux/Unix systems for its robust output, `nslookup` remains a popular and quick troubleshooting tool, especially on Windows.

**07. What are the different types of `DNS RECORDS`**

There are many types of DNS (Domain Name System) records. Some of the most common include:
*   **A (Address) Record:** Maps a domain name to an IPv4 (Internet Protocol version 4) address.
*   **AAAA (Quad A) Record:** Maps a domain name to an IPv6 (Internet Protocol version 6) address.
*   **CNAME (Canonical Name) Record:** Forwards one domain or subdomain to another domain, essentially acting as an alias.
*   **MX (Mail Exchange) Record:** Directs email to a specific mail server for the domain.
*   **TXT (Text) Record:** Allows administrators to insert arbitrary text into the DNS (Domain Name System) record, most often used for verifying domain ownership and configuring email security policies like SPF (Sender Policy Framework).
*   **NS (Name Server) Record:** Indicates which DNS (Domain Name System) server is authoritative for the domain.
*   **SOA (Start of Authority) Record:** Contains core administrative information about the domain, such as the primary name server and the email of the domain administrator.
*   **PTR (Pointer) Record:** Provides a domain name linked to an IP (Internet Protocol) address, used primarily for reverse DNS (Domain Name System) lookups.

**08. What is `DNS Dumpster`**

DNS (Domain Name System) Dumpster is a free, online domain research tool that discovers hosts related to a domain. It performs passive footprinting (information gathering) to map out a domain's attack surface. By querying various public search engines and datasets, it quickly compiles visual and tabular lists of subdomains, IP (Internet Protocol) addresses, MX (Mail Exchange) records, and TXT (Text) records associated with the target domain.

**09. What is `Shodan.io`**

Shodan is a search engine designed specifically for Internet-connected devices, often referred to as IoT (Internet of Things) devices. Unlike standard search engines (like Google) that index website content, Shodan indexes the information returned from open network ports (known as banners). It allows researchers and security professionals to discover servers, webcams, industrial control systems, and routers exposed to the public internet, revealing details about their OS (Operating System), running services, and potential vulnerabilities.

**10. How can we find `subdomains`**

We can find subdomains using several methods:
*   **Passive OSINT (Open-Source Intelligence):** Using websites like DNS (Domain Name System) Dumpster or tools like Subfinder that search public databases.
*   **Searching CT (Certificate Transparency) logs:** Looking at publicly logged SSL (Secure Sockets Layer) / TLS (Transport Layer Security) certificates (e.g., using the website crt.sh) to see which subdomains have had certificates officially issued for them.
*   **Active Brute-forcing:** Using command-line tools (like Gobuster or wfuzz), which guess subdomains from a long wordlist and send HTTP (Hypertext Transfer Protocol) or DNS (Domain Name System) requests to see if they exist.
*   **Zone Transfers:** Attempting a DNS (Domain Name System) zone transfer query (AXFR - Authoritative Zone Transfer) which, if misconfigured on the target server, will leak all DNS (Domain Name System) records for a domain.
*   **Search Engine Dorking:** Using advanced search operators (e.g., `site:domain.com -www`) on Google to find subdomains that have been indexed.

**11. What is `subfinder`**

Subfinder is a fast, open-source subdomain discovery tool. It is used to discover valid subdomains for websites by utilizing passive online sources. It aggregates data from various APIs (Application Programming Interfaces), search engines, and data sets to compile a comprehensive list of subdomains without ever sending direct traffic to the target's infrastructure, ensuring the reconnaissance remains entirely stealthy.

**12. What is the difference between `Active reconnaissance` and `Passive reconnaissance`**

The difference lies in how you interact with the target system:
*   **Active reconnaissance** involves direct interaction with the target's network or systems. Examples include running a port scan, pinging an IP (Internet Protocol) address, or brute-forcing directories. This method yields highly accurate, real-time data but leaves digital footprints in the target's network logs, making it highly likely to be detected by their IDS (Intrusion Detection System) or IPS (Intrusion Prevention System).
*   **Passive reconnaissance** involves gathering information about a target without sending any direct traffic to their servers. You rely entirely on publicly available information, known as OSINT (Open-Source Intelligence). Examples include looking up WHOIS (Who Is) records, searching Shodan, or using Subfinder. Because you are only communicating with third-party databases, the target remains completely unaware that they are being investigated.
