# Wireshark User Manual – Packet Analysis for Pentesters

## 📘 Overview

Wireshark is a powerful open-source packet analyzer used to capture and inspect network traffic in real time. It plays a critical role in cybersecurity, network troubleshooting, malware analysis, and penetration testing. This manual covers how Wireshark works, core protocol behaviors, filtering techniques, and packet analysis strategies for both offensive and defensive use cases.

---

## 🧠 Core Concepts

### 🔹 What Wireshark Captures

- Each **packet** transmitted or received on a selected interface
- Source and destination **IP addresses and ports**
- **TCP/UDP flags**, protocol headers, and payload data
- Timing between packets (useful for detecting delays or anomalies)

### 🔹 TCP Flags Explained

- **SYN** – Initiates a TCP connection (first handshake)
- **SYN, ACK** – Sent by server to acknowledge and accept a SYN
- **ACK** – Acknowledges receipt of data or a handshake step


- **RST** – Terminates a connection abruptly (Reset)
- **FIN** – Gracefully closes a TCP connection
- **PSH** – Pushes buffered data to the receiving application immediately

> The `PSH` flag is common in interactive sessions (e.g., remote shells), ensuring user input and responses are sent/received instantly.

---

## 🔍 Display Filters

Display filters help you isolate relevant packets from large traffic captures. They do not stop capture—they only affect what’s shown.

### 🔸 Port Filtering

```wireshark
tcp.port == 22         # Show only SSH traffic
tcp.port == 80         # Show only HTTP traffic
tcp.port == 443        # Show HTTPS
udp.port == 53         # Show DNS queries/responses
```

### 🔸 Combine Filters with Logical Operators

```wireshark
tcp.port == 80 || tcp.port == 443
```

➡️ Show packets with **either port 80 or 443**.

```wireshark
ip.src == 192.168.1.10 && tcp.dstport == 22
```

➡️ Show SSH packets sent from IP 192.168.1.10.

### 🔸 IP-Based Filters

```wireshark
ip.addr == 192.168.1.1
ip.src == 10.0.0.1
ip.dst == 8.8.8.8
```

### 🔸 Protocol Filters

```wireshark
http
ftp
icmp
dns
ssl || tls
```

### 🔸 TCP Stream Filters

```wireshark
tcp.stream eq 2
```

➡️ Follow a single conversation between two hosts. Helpful in login sequences or shell sessions.

---

## 📡 Analyzing TCP Connections

### 🔁 TCP 3-Way Handshake

A standard TCP connection starts with:

1. `SYN` (client → server)
2. `SYN, ACK` (server → client)
3. `ACK` (client → server)

If this sequence completes, the connection is considered established.

### ❌ TCP Resets (RST)

A packet with `RST` indicates the target rejected the connection:

- Service may not be listening
- Port is filtered
- Unexpected packet received

### 📬 PSH, ACK in Interactive Sessions

- `PSH` sends data immediately to the application (e.g., typed command)
- Paired with `ACK` to confirm delivery

These flags are common in shell sessions, chat applications, or remote login protocols.

---

## 🎯 Use Cases in Pentesting

### ✅ Credential Capture

- Apply filter: `ftp || http || smtp`
- Look for unencrypted logins or passwords

### ✅ DNS Reconnaissance

- Filter: `dns`
- Observe domain lookups, potential data exfiltration via DNS tunneling

### ✅ Port Scanning Detection

- Filter: `tcp.flags.syn == 1 && tcp.flags.ack == 0`
- This pattern reveals SYN scans (common in tools like Nmap)

### ✅ Shell Access or Reverse Shells

- Use: `tcp.stream eq X`
- Look for `PSH, ACK` packets and plaintext commands

---

## 🛠 Tips & Best Practices

- **Color rules**: Customize colors to quickly identify suspicious traffic (e.g., red for `RST`, green for `SYN`)
- **Follow TCP Stream**: Right-click → Follow → TCP Stream to view the full conversation
- **Name resolution**: Turn off (under Preferences) for raw IP view
- **Mark packets**: Use shortcuts (`Ctrl + M`) to highlight key moments
- **Expert Info**: Use the Expert Info panel for anomalies and warnings

---

## 💾 Saving and Sharing Captures

- Save captures in `.pcapng` format for full compatibility
- Use `File → Export Specified Packets` to trim down large captures
- Mask sensitive data before sharing (e.g., with `editcap` or anonymization plugins)

---

## 🔗 Additional Resources

- 👉 To see a practical lab that includes the analysis of a backdoor shell established via FTP traffic and the use of filters to detect interaction over TCP 6200, visit the following resource: [wireshark-analyze-vsftpd.md](https://github.com/lorenzococcia/pentest-labs/blob/tools/wireshark/wireshark-analyze-vsftpd.md)

## ✅ Summary

Wireshark is indispensable for cybersecurity professionals. Whether for offensive operations (e.g., reverse shells, packet injection detection) or defensive analysis (e.g., identifying scanning, traffic anomalies), mastering filters and packet behavior gives you visibility and control.

> 📌 Practice using real-world lab traffic and follow TCP stream flows to build pattern recognition and intuition.

