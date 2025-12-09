# Wireshark – TCP Analysis

## Objective
The objective of this lab is to analyze **TCP (Transmission Control Protocol)** packets using Wireshark.  
This includes understanding:
- How TCP establishes connections  
- The **3-way handshake**  
- Common TCP fields and flags  
- How to use Wireshark filters to investigate traffic  

---

## Sample PCAP File
**[Download Sample PCAP](https://github.com/0xrajneesh/90-Days-SOC-Challenge-Beginner/raw/refs/heads/main/Protocol_Analysis_pcap.pcapng)**  
Open the file in wireshark to begin analyzing TCP packets.

---

## What is TCP?
TCP is a **Layer 4 transport protocol** responsible for:
- Reliable delivery  
- Ordered packet flow  
- Error correction  
- Connection-oriented communication  

Unlike UDP (User Datagram Protocol), TCP **guarantees** that data arrives correctly and in order.

---

## Key TCP Fields

| **Field Name**        | **Description**                                      |
|-----------------------|------------------------------------------------------|
| **Source Port**       | Sender’s port number                                 |
| **Destination Port**  | Receiver’s port number                               |
| **Sequence Number**   | First byte number of the segment                     |
| **Acknowledgment No.**| Confirms received data                               |
| **Flags**             | Control bits (SYN, ACK, FIN, RST, PSH, URG)          |
| **Window Size**       | Available buffer size                                |
| **Checksum**          | Error-checking for the TCP segment                   |

---

## TCP 3-Way Handshake
TCP establishes a connection using:

1. **SYN** - Client → Server: “I want to connect”
2. **SYN-ACK** - Server → Client: “I acknowledge, let's sync”
3. **ACK** - Client → Server: “Connection confirmed”

After this, data transfer begins.

---

## Useful Wireshark TCP Filters

1️) Show all TCP traffic-
[tcp]
<img width="960" height="479" alt="Screenshot 2025-12-09 060659" src="https://github.com/user-attachments/assets/011105b3-f048-409a-ab7a-15933b135a55" />


2️)Show SYN packets (start of connections)
[tcp.flags.syn == 1]
<img width="958" height="477" alt="Screenshot 2025-12-09 061337" src="https://github.com/user-attachments/assets/033a7395-d7ea-4603-adca-743191e58e88" />

Used to identify connection attempts-useful for detecting scanning.

3️)Show FIN packets (connection termination)
[tcp.flags.fin == 1]
<img width="934" height="479" alt="Screenshot 2025-12-09 061620" src="https://github.com/user-attachments/assets/e73d2e69-5035-47b5-87a4-5532bc3e118b" />

Helps analyze normal shutdowns vs. abrupt resets.

4️)Show TCP packets on port 80 (HTTP)
[tcp.port == 80]
<img width="957" height="478" alt="Screenshot 2025-12-09 061659" src="https://github.com/user-attachments/assets/8f115af9-5924-40e4-a4ef-8606bd2e8211" />

Useful for application-layer investigation.

---

Why TCP Analysis Matters in Security & SOC Work
Understanding TCP behavior helps analysts detect:

✔ Port scanning
Look for many SYN packets with no SYN-ACK responses.

✔ Reset attacks (RST floods)
Used maliciously to disrupt active connections.

✔ Abnormal connection terminations
FIN vs. RST reveals how connections ended.

✔ Suspicious long-lived or repeated sessions
Indicators of malware C2, persistence, or data exfiltration.

✔ Misconfigurations or failed sessions
Sequence/Ack anomalies often point to network issues.

## Conclusion ##
TCP is one of the most important protocols for SOC analysts to understand.
By inspecting flags, handshake behavior, and port activity, analysts can identify:

Connection states

Failed or abnormal communications

Reconnaissance attempts

Potential malicious activity

Wireshark provides the visibility needed to diagnose and investigate traffic at the packet level.
