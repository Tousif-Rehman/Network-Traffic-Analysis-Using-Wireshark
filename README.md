# Network Traffic Analysis Using Wireshark

## Overview
This project demonstrates how to use Wireshark, a powerful network analysis tool, to capture and analyze network traffic. The goal is to simulate potential malicious activities, identify suspicious patterns, and analyze them for potential cybersecurity threats. This project is set up in a Kali Linux virtual environment.

---

## Table of Contents
- [Overview](#overview)
- [Project Structure](#project-structure)
- [Setup](#setup)
- [Usage](#usage)
- [Analysis Process](#analysis-process)
- [Findings](#findings)
- [Resources](#resources)

---

## Project Structure
The project is organized into the following directories and files:

```plaintext
wireshark-network-traffic-analysis/
├── README.md                    # Project overview and instructions
├── findings.md                  # Report with analysis findings
├── /screenshots                 # Screenshots of Wireshark suspicious activity views
│   ├── dns-lookup.png           # Example of DNS request packet
│   ├── failed-login.png         # Example of SSH failed login attempt
│   └── large-download.png       # Example of high-volume download traffic
├── /wireshark-capture-files     # Folder to store Wireshark capture files (.pcap)
│   └── suspicious-traffic.pcap  # Sample capture file for analysis
└── /docs                        # Detailed steps and extra documentation
    └── methodology.md           # Full documentation of project setup and analysis
```

---

## Setup

### Prerequisites
- **Kali Linux**: A Linux distribution for penetration testing.
- **Wireshark**: Install via `sudo apt update && sudo apt install wireshark`.
- **VMware or VirtualBox**: Used to run Kali Linux virtually.

### Setting Up Kali Linux with Wireshark
1. **Install Kali Linux**: Set up a virtual machine for Kali Linux using VMware or VirtualBox.
2. **Install Wireshark**: Use the command above to install Wireshark on Kali Linux.
3. **Configure Network**: Set the network adapter to "Bridged" mode to monitor network traffic.

---

## Usage

### Capturing Traffic in Wireshark
1. **Start Wireshark**: Open Wireshark on Kali Linux.
2. **Choose Network Interface**: Select the active network interface (e.g., `eth0`, `wlan0`).
3. **Start Capture**: Click "Start" to begin capturing network traffic.
4. **Apply Filters**: Apply relevant filters to target specific traffic (e.g., `dns`, `tcp.port == 22`).
5. **Save Capture**: Stop the capture and save it as a `.pcap` file for analysis.

### Sample Filters Used
- **DNS Traffic**: `dns`
- **Failed SSH Logins**: `tcp.port == 22`
- **High-Volume Downloads**: `tcp && frame.len > 1000`

---

## Analysis Process
This project simulated various network events to identify suspicious activities, such as:
1. **Unusual DNS Requests**: DNS lookups for non-existent or suspicious domains.
2. **Failed SSH Login Attempts**: Frequent failed login attempts on SSH, which may suggest a brute-force attack.
3. **Large Data Transfers**: High-volume file transfers that could indicate data exfiltration.

Details of these simulations and analysis can be found in the [`findings.md`](./findings.md) file.

---

## Findings
The project’s findings include observed packet details and interpretations of possible security threats. Full analysis and packet details are documented in [`findings.md`](./findings.md), which provides a summary of:
1. **DNS Requests to Suspicious Domains**
2. **Brute Force Attempts on SSH**
3. **High-Volume Data Transfers**

These findings illustrate basic traffic analysis techniques that can help in identifying potential cybersecurity threats in a network environment.

---

## Resources
- **Wireshark Documentation**: [https://www.wireshark.org/docs/](https://www.wireshark.org/docs/)
- **Kali Linux**: [https://www.kali.org/](https://www.kali.org/)
- **Packet Analysis Basics**: Introductory guides on network packet analysis.

---

## License
This project is licensed under the MIT License.
```
