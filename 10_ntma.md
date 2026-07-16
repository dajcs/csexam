# Network Traffic Monitoring & Analysis


**01. What is packet capture and why is it important?**

Packet capture, often referred to as PCAP (Packet Capture), is the process of intercepting and logging digital traffic that passes over a computer network. To do this, a NIC (Network Interface Card) is typically placed in promiscuous mode so it can capture all traffic on the segment, not just traffic addressed specifically to it. It is important because it allows network administrators and security professionals to perform deep packet inspection. By examining the actual data traversing the network, teams can:
- Troubleshoot complex connectivity issues.
- Identify security breaches.
- Detect malicious software.
- Analyze network performance.
- Verify that applications behave as expected
- Validate that configurations such as firewalls, routing, and encryption actually do what they're supposed to

**02. How does Wireshark display and dissect network packets?**

Wireshark reads captured traffic and applies protocol dissectors — modular components that understand the structure of specific protocols — to interpret the raw bytes layer by layer. The interface has three main panes:

- **Packet list** (top): one row per packet, with columns like time, source, destination, protocol, and info
- **Packet details** (middle): an expandable tree showing each protocol layer from the frame up through Ethernet, IP (Internet Protocol), TCP (Transmission Control Protocol) or UDP (User Datagram Protocol), and the application layer
- **Packet bytes** (bottom): the raw hexadecimal and ASCII representation

When you click a field in the details tree, Wireshark highlights the corresponding bytes below, mapping interpreted fields directly to their position in the raw data. The dissectors handle the tedious work of decoding flags, offsets, and field lengths so you see human-readable values instead of raw hex.

**03. What is the difference between capture filters and display filters?**

- **Capture filters** decide which packets get recorded in the first place. They are applied *before* capture and use Berkeley Packet Filter (BPF) syntax (for example, `tcp port 443` or `host 10.0.0.5`). Anything that doesn't match is discarded and never written, which keeps files smaller and reduces load on busy links — but filtered-out data is gone permanently.
- **Display filters** are applied *after* capture to packets you already have, controlling only what is shown while everything remains stored. They use Wireshark's own richer syntax (for example, `http.response.code == 404` or `ip.addr == 10.0.0.5 && tcp.flags.syn == 1`) and can reference deeply dissected fields that BPF cannot.

In short: capture filters are about what you collect and are irreversible; display filters are about what you view and are freely changeable.

**04. How do you follow TCP streams in Wireshark?**

To follow a TCP (Transmission Control Protocol) stream:

- Right-click any packet belonging to the conversation and choose Follow, then TCP Stream (or use the Analyze menu)
- Wireshark reassembles all segments of that connection in order and presents the reconstructed conversation in a single window, color-coding the two directions (client-to-server and server-to-client) differently
- You can view it as ASCII, hex dump, or raw bytes, and save it out
- Wireshark automatically applies a display filter (like `tcp.stream eq 3`) so the packet list narrows to just that conversation

This is useful because a single logical exchange is often split across many interleaved packets; following the stream stitches them back together so you can read the application-layer dialogue as a continuous whole. The same feature exists for UDP (User Datagram Protocol), TLS (Transport Layer Security), and HTTP (HyperText Transfer Protocol) streams.

**05. What is tcpdump and when should you use it over Wireshark?**

tcpdump is a lightweight, command-line packet capture and analysis tool that runs on most Unix-like systems without a graphical interface. Reach for it over Wireshark when:

- You're working on a remote server over SSH (Secure Shell) with no display available
- You need to capture on a resource-constrained or headless machine where a heavy graphical application would be impractical
- You want to script and automate captures as part of a larger pipeline
- You want to quickly grab traffic to a file for later analysis — a common workflow is to capture with tcpdump on the server (`tcpdump -w capture.pcap`) and open the file in Wireshark on a workstation

Wireshark remains preferable for deep interactive inspection, extensive protocol dissection, and visual statistics; tcpdump wins on speed, footprint, and remote or automated use.

**06. How do you construct effective tcpdump filter expressions?**

tcpdump uses Berkeley Packet Filter (BPF) syntax built from primitives combined with logical operators. The primitives fall into a few categories:

- **Type qualifiers**: `host`, `net`, `port`
- **Direction qualifiers**: `src`, `dst`
- **Protocol qualifiers**: `tcp`, `udp`, `ip`, `arp`

You combine these with logical operators:

- `and`, `or`, `not` (or their symbols `&&`, `||`, `!`)
- Parentheses for grouping (quoted or escaped so the shell doesn't interpret them)

For example, `tcp and dst port 80 and not src host 10.0.0.1` captures web-bound traffic except from one host. You can also match specific header fields and bit values, such as `'tcp[13] & 2 != 0'` to catch packets with the SYN (synchronize) flag set. Effective filters are as specific as the situation allows — narrow enough to cut noise, but not so narrow that you accidentally exclude the packets you're trying to diagnose.

**07. What are common indicators of network anomalies?**

- Unexpected spikes or drops in traffic volume
- A high rate of TCP (Transmission Control Protocol) retransmissions, duplicate acknowledgements, or resets (RST flags) suggesting instability or scanning
- Large numbers of connection attempts to many ports or hosts (a signature of port scanning or sweeping)
- DNS (Domain Name System) queries to suspicious or algorithmically-generated domain names
- Traffic on non-standard ports for a given protocol
- Beaconing patterns where a host contacts an external address at regular intervals (often malware calling home)
- Large outbound transfers that don't match normal business activity (possible data exfiltration)
- Malformed packets, unexpected protocol usage, or plaintext credentials
- ARP (Address Resolution Protocol) anomalies suggesting spoofing or man-in-the-middle activity
- Latency or jitter beyond normal baselines

Crucially, "anomaly" is defined relative to a known baseline, so understanding what normal looks like for your network is what makes deviations meaningful.

**08. How can you identify unauthorized connections in packet captures?**

Start by establishing what authorized traffic looks like — known hosts, expected destinations, sanctioned ports and protocols — then look for anything outside that:

- Filter for connections to or from unfamiliar external IP (Internet Protocol) addresses, especially on high or unusual ports
- Check destinations against threat-intelligence lists of known-malicious addresses
- Use Wireshark's Statistics, then Conversations view, which lists every endpoint pair with byte and packet counts, making rogue or unexpectedly chatty connections stand out
- Watch for internal hosts initiating outbound connections they shouldn't (a database server reaching out to the internet, for instance)
- Look for connections at odd hours, repeated beaconing intervals, or protocols tunneled over ports meant for something else

Correlating packet evidence with firewall logs, DNS (Domain Name System) records, and authentication logs helps confirm whether a connection was actually unauthorized versus merely unusual.

**09. What tools does Wireshark provide for traffic statistics?**

Wireshark's Statistics menu offers a rich set of analytical views:

- **Protocol Hierarchy**: breaks down what fraction of traffic each protocol represents
- **Conversations**: lists every pair of communicating endpoints with packet, byte, and duration figures
- **Endpoints**: summarizes activity per individual host
- **IO (Input/Output) Graphs**: plot traffic rate over time to spot spikes, gaps, or periodic patterns
- **Service Response Time**: tables measuring how quickly servers reply
- **Flow Graphs**: draw a sequence diagram of a conversation's packets
- **Expert Information**: summarizes warnings and errors the dissectors flagged
- **Protocol-specific statistics**: for things like HTTP (HyperText Transfer Protocol), DNS (Domain Name System), and TCP (Transmission Control Protocol) stream analysis

Together these let you move from individual packets to a high-level picture of what the network is doing.

**10. How do you analyze DNS queries in network traffic?**

Apply the display filter `dns` to isolate Domain Name System traffic, then examine the query and response pairs. Each query shows the requested name and record type, while responses show returned answers or an error code. Common record types include:

- **A**: IPv4 addresses
- **AAAA**: IPv6 addresses
- **MX**: mail servers
- **TXT**: text records

Things worth looking for:

- Queries to suspicious or randomly-generated domain names (which can indicate malware using a domain-generation algorithm)
- An unusually high volume of queries or an abnormal number of failed lookups (such as NXDOMAIN, non-existent domain)
- Long or oddly-encoded subdomains that may signal DNS tunneling used to smuggle data
- Responses pointing to unexpected IP (Internet Protocol) addresses

Wireshark's Statistics, then DNS view gives aggregate breakdowns of query types, response codes, and timing. Comparing query names against known-good and known-bad lists helps distinguish routine name resolution from something malicious or misconfigured.

**11. What are best practices for capturing network traffic?**

- Capture at the right location — a point where the traffic you care about actually flows, such as a SPAN (Switched Port Analyzer) mirror port, a network TAP (Test Access Point), or the host itself
- Use capture filters to limit collection to relevant traffic so files stay manageable
- Consider ring buffers or file-size limits for long captures so they don't fill the disk
- Ensure you have legal authority and appropriate permissions, since packet data can contain sensitive and personal information; handle and store the files securely
- Capture with sufficient buffer and adequate hardware to avoid dropped packets on busy links
- Timestamp accurately and document what you captured and why
- When possible, capture from more than one vantage point to see both sides of a conversation
- Be mindful that capturing itself consumes resources and, on the monitoring host, can alter the very behavior you're observing

**12. How does encryption affect traffic analysis?**

Encryption — most commonly via TLS (Transport Layer Security) — conceals packet payloads, so you can no longer read application-layer content such as web page contents, credentials, or message bodies directly from the capture. What remains visible is metadata:

- IP (Internet Protocol) addresses and ports of the endpoints
- Packet sizes and timing
- Connection duration
- For TLS, portions of the handshake including the Server Name Indication (SNI) field and certificate details (though newer mechanisms like Encrypted Client Hello are closing even that gap)

As a result, traffic analysis of encrypted flows shifts toward behavioral and metadata-based techniques — traffic volume, timing patterns, beaconing, and flow characteristics — rather than payload inspection. To see inside encrypted traffic legitimately, you generally need the session keys:

- In a controlled environment, configure endpoints to log TLS key material (via the `SSLKEYLOGFILE` environment variable) and point Wireshark at it to decrypt
- Or use a man-in-the-middle proxy that you control and trust

Absent those keys, the content stays opaque — which is by design, and is exactly why encryption protects privacy and security.
