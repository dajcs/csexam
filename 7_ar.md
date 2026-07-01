# Active Reconnaissance




**1. What is `active reconnaissance` ?**

Active reconnaissance is a phase in information gathering where a security professional or attacker directly engages and interacts with the target system to collect data. Unlike passive reconnaissance (where data is gathered from public records and search engines without touching the target's servers), active reconnaissance involves sending network packets directly to the target. Examples of this include port scanning, ping sweeps to identify live IP addresses, and vulnerability scanning.

**2. Why is `active reconnaissance` it important for cyber security?**

It is important for cybersecurity because it allows defenders (and penetration testers) to accurately map out the real-world attack surface of a target. By actively engaging with systems, you can identify open ports, live hosts, running services, software versions, and misconfigurations that passive methods cannot detect. This process uncovers the exact vulnerabilities and entry points that malicious actors could exploit, allowing organizations to patch and secure their infrastructure before an attack occurs.

**3. How can `Wappalyzer` be used for active reconnaissance?**

Wappalyzer is a technology profiling tool designed to uncover the software stack running on web applications. While often used passively as a browser extension, it can be used for active reconnaissance via its CLI (Command-Line Interface) tool or API (Application Programming Interface). By actively sending HTTP (Hypertext Transfer Protocol) requests to a target website, Wappalyzer analyzes the HTTP response headers, HTML (HyperText Markup Language) source code, and script tags to identify the underlying CMS (Content Management System), web servers, programming languages, and analytics tools. This helps security testers map out the specific technologies in use so they can search for known exploits and vulnerabilities tied to those software versions.

**4. What is `DNS enumeration` ?**

DNS (Domain Name System) enumeration is the process of locating all the DNS records and routing information associated with a specific domain name. This technique is used to map a target's internal and external network infrastructure. By querying the nameservers, attackers and defenders can discover hostnames, IP addresses, mail servers, and hidden subdomains using techniques like brute-forcing, zone transfers, and querying specific record types (such as A, MX, and TXT records).

**5. How to enumerate `SMTP`s using command-line tools?**

To enumerate SMTP (Simple Mail Transfer Protocol) services, you can use several command-line tools to interact directly with the mail server to verify whether specific users or email addresses exist on the system.
*   **Telnet / Netcat:** You can manually connect to the SMTP port (usually port 25) by typing `nc <target-IP> 25`. Once connected, you can use built-in SMTP commands such as `VRFY` (Verify) to check if a specific username exists, `EXPN` (Expand) to reveal members of a mailing list, or `RCPT TO` (Recipient To) to test if an inbox accepts mail.
*   **smtp-user-enum:** This is a dedicated command-line script that automates the brute-forcing of the `VRFY`, `EXPN`, or `RCPT TO` commands against a server using a list of potential usernames. Example command: `smtp-user-enum -M VRFY -U users.txt -t <target-IP>`
*   **Nmap (Network Mapper):** Nmap includes scripts specifically for this purpose. You can run: `nmap --script smtp-enum-users.nse -p 25 <target-IP>`

**6. How should we perform `OS fingerprinting`?**

OS (Operating System) fingerprinting is the process of determining the operating system running on a target device. It should be performed by analyzing the unique ways different operating systems respond to network probes.
*   **Active OS Fingerprinting:** The best way to perform this is by using Nmap. Nmap sends a series of crafted TCP (Transmission Control Protocol), UDP (User Datagram Protocol), and ICMP (Internet Control Message Protocol) packets to the target. It then analyzes the responses—such as TTL (Time to Live) values, TCP window sizes, and packet flags—and compares them against a massive database of known OS signatures. You can execute this by running: `nmap -O <target-IP>`.
*   **Passive OS Fingerprinting:** Alternatively, you can perform this without sending any packets to the target by using tools like `p0f` or Wireshark to silently monitor and capture network traffic, analyzing the packets to deduce the OS.

**7. What is `sqlmap` ? How to use it ?**

`sqlmap` is a highly popular open-source penetration testing tool that automates the process of detecting and exploiting SQL (Structured Query Language) injection flaws. It takes over database servers by utilizing a powerful detection engine that can fingerprint the DBMS (Database Management System), extract data, bypass firewalls, and sometimes even execute commands on the underlying operating system.

**How to use it:**
`sqlmap` is used via the command line. A basic workflow against a vulnerable URL (Uniform Resource Locator) usually follows these steps:
1.  **Test the URL for vulnerabilities:**
    `sqlmap -u "http://example.com/vuln.php?id=1"`
2.  **Enumerate Databases:** If the tool confirms the parameter is vulnerable, you can list the available databases on the server:
    `sqlmap -u "http://example.com/vuln.php?id=1" --dbs`
3.  **Enumerate Tables:** Once you find an interesting database, you can list its tables by specifying the database name:
    `sqlmap -u "http://example.com/vuln.php?id=1" -D target_database --tables`
4.  **Dump Data:** Finally, you can extract the contents of a specific table (e.g., a "users" table):
    `sqlmap -u "http://example.com/vuln.php?id=1" -D target_database -T users --dump`
