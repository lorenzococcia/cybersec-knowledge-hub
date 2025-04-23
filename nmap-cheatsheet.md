# Nmap Cheatsheet - Network Mapping & Scanning Tool

## Overview
**Nmap** (Network Mapper) is an open-source tool for network discovery and security auditing. It is widely used in cybersecurity, penetration testing, and network administration to:
- Discover live hosts on a network
- Scan open ports
- Detect services and their versions
- Determine operating systems
- Identify potential vulnerabilities using scripts

---

## Basic Scanning
| Command | Description |
|---------|-------------|
| `nmap <IP>` | Scan a single host |
| `nmap <IP1> <IP2>` | Scan multiple hosts |
| `nmap <range>` | Scan a range of IPs (e.g., `nmap 192.168.1.1-50`) |
| `nmap <CIDR>` | Scan a subnet (e.g., `nmap 192.168.1.0/24`) |
| `nmap -iL list.txt` | Scan hosts listed in a file |
| `nmap -sn <IP>` | Host discovery (ping scan) |
| `nmap -sP <IP>` | Legacy ping scan (same as `-sn`) |

---

## Port Scanning Techniques
| Command | Description |
|---------|-------------|
| `-sS` | TCP SYN scan (stealth) |
| `-sT` | TCP connect scan |
| `-sU` | UDP scan |
| `-sA` | TCP ACK scan |
| `-sN` | TCP Null scan |
| `-sX` | Xmas scan |
| `-p <ports>` | Specify ports (e.g., `-p 22,80,443`) |
| `--top-ports <n>` | Scan the top `n` most common ports |
| `-F` | Fast scan (less ports) |
| `--open` | Show only open ports |

---

## Service and OS Detection
| Command | Description |
|---------|-------------|
| `-sV` | Service/version detection |
| `-O` | Operating system detection (requires root) |
| `-A` | Aggressive scan: includes `-O`, `-sV`, `-sC`, and traceroute |

---

## Output Options
| Command | Description |
|---------|-------------|
| `-oN file.txt` | Normal output to file |
| `-oX file.xml` | XML output to file |
| `-oG file.gnmap` | Greppable output |
| `-v` / `-vv` | Verbose mode |

---

## Timing and Performance
| Command | Description |
|---------|-------------|
| `-T0` to `-T5` | Timing template (0 = paranoid, 5 = insane) |

---

## NSE (Nmap Scripting Engine)
| Command | Description |
|---------|-------------|
| `--script <name>` | Run a specific script |
| `--script-help <name>` | Get info about a script |
| `--script vuln` | Run vulnerability scripts |

Common NSE Categories:
- `auth` - authentication bypass
- `vuln` - known vulnerabilities
- `exploit` - exploitation scripts
- `malware` - malware detection
- `safe` - safe scripts

---

## Practical Examples
```bash
nmap -sS -p 22,80 192.168.1.1
nmap -sV -oN services.txt 192.168.1.5
nmap -A -T4 192.168.1.0/24
nmap --script vuln 192.168.1.10
```

---

## Tips
- Use `sudo` to unlock features like OS detection and SYN scan.
- Combine scans with `-v` for better visibility.
- Always have permission before scanning networks!

---

**Note**: Nmap is powerful — always use it responsibly and within legal boundaries.

