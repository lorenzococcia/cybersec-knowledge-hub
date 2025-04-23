# Nessus Cheatsheet - Vulnerability Scanner

## Overview
**Nessus** is a widely used vulnerability scanner developed by Tenable, designed to identify security issues such as missing patches, configuration weaknesses, and known vulnerabilities (CVEs) in IT environments. It supports comprehensive scanning of systems, applications, and network devices, making it a key component in vulnerability management programs.

## Nessus Versions
| Version             | IP Limit | Web App Scanning | External Surface Scan | Notes                       |
|---------------------|----------|------------------|------------------------|-----------------------------|
| Nessus Essentials   | 16 IPs   | ❌               | ❌                     | Free version for students, personal use or learning |
| Nessus Professional | Unlimited| ❌               | ❌                     | Commercial version for security consultants and internal teams |
| Nessus Expert       | Unlimited| ✅               | ✅                     | Newest and most advanced version with web app and internet-facing asset coverage |

Nessus is continuously updated with the latest vulnerability checks via plugin feeds. Each scan checks against thousands of plugins mapped to CVEs, CPEs, and compliance standards.

---

## Setup & Installation
### Access
- After installing Nessus, the web interface is accessible at `https://<IP>:8834`
- First-time setup includes plugin download (can take **5–15 minutes**, normal behavior)

### Initial Steps
1. Launch Nessus and wait for plugin sync to complete
2. Create an admin account
3. Choose version (Essentials / Pro / Expert) and enter license key
4. Log in and access the dashboard

### Common Setup Notes
- Ensure port `8834` is open if accessing remotely
- Update plugins regularly for accurate results
- Can be installed on Windows, Linux, or macOS

---

## Scan Types & Use Cases
### Templates (GUI)
- **Basic Network Scan**: Scan for common vulnerabilities in internal systems
- **Advanced Scan**: Customize ports, policies, credentials, and plugins
- **Web Application Tests** *(Expert)*: Scan OWASP Top 10 issues in websites
- **Credentialed Scans**: Detect deeper vulnerabilities (e.g., missing patches)
- **Compliance Scans**: Check for PCI-DSS, CIS Benchmarks, and more

### Scan Policies (Custom)
- Control plugin families, performance settings, authentication methods, etc.
- Save and reuse custom scan templates

---

## Scan Workflow
1. Select or create a scan policy/template
2. Enter target IPs/domains/subnets
3. Add credentials if required (SSH, SMB, etc.)
4. Launch the scan manually or schedule it
5. Analyze results and export as PDF, CSV, or HTML
6. Assign remediation tasks or integrate with patch management tools

---

## Reporting & Analysis
### Export Options
- **PDF**: Executive summary or technical breakdown
- **CSV**: Filterable report by IP, plugin ID, CVSS score
- **HTML**: Lightweight, navigable format

### Sorting and Filtering
- By plugin ID, severity (Critical, High, Medium...), CVSS score, asset tags
- Group by host, vulnerability type, or compliance control

---

## CLI Tools (Advanced)
- Nessus comes with a command-line interface (Linux/macOS):
```bash
nessuscli update            # Force update plugins
nessuscli fix --reset       # Reset configuration to defaults
nessuscli managed link      # Link to Tenable.io instance
```
- For Nessus running on Linux systems, useful for automation or recovery

---

## Best Practices
- ✅ Schedule scans during off-hours to avoid performance issues
- ✅ Use **credentialed scans** for full visibility
- ✅ Review reports with IT teams regularly
- ✅ Tag and group assets by department or risk
- ✅ Integrate with SIEM or ticketing systems for remediation tracking

---

## Common Questions
- **Why is Nessus slow on first boot?**
  - It’s downloading and indexing over 180,000+ plugins. First run may take 10–15 minutes.

- **Can I scan externally exposed assets?**
  - Only with Nessus Expert or by pairing Nessus with Tenable.io

- **How often should I scan?**
  - High-risk systems: Weekly
  - Standard internal systems: Monthly
  - After significant patch events or system changes

- **Is Nessus suitable for enterprise use?**
  - Yes, Nessus Professional and Expert versions are widely used by enterprises, especially when integrated with Tenable Security Center or Tenable.io.

---

## Final Notes
Nessus remains one of the most reliable and accurate vulnerability scanners. While tools like OpenVAS are viable alternatives, Nessus offers broader plugin support, better reporting, and enterprise integrations.

> Always scan ethically and only with permission. Vulnerability scanning can impact networks if not handled carefully.

