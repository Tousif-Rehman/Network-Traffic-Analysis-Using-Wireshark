# Findings Report: Network Traffic Analysis Using Wireshark

## Introduction
This report presents findings from a network traffic analysis conducted using Wireshark on Kali Linux. The purpose of this analysis was to identify potential cybersecurity threats by monitoring various forms of network traffic. We simulated certain types of suspicious activities, captured the corresponding packets, and analyzed them to gain insights into potential vulnerabilities.

---

## Table of Contents
- [Environment Setup](#environment-setup)
- [Traffic Analysis Steps](#traffic-analysis-steps)
- [Suspicious Findings](#suspicious-findings)
  - [Unusual DNS Requests](#unusual-dns-requests)
  - [Large Data Transfers](#large-data-transfers)
- [Conclusion and Recommendations](#conclusion-and-recommendations)

---

## Environment Setup
1. **Operating System**: Kali Linux running in a VMware virtual environment.
2. **Network Configuration**: The network adapter was set to "Bridged" mode to capture internet traffic across the local network.
3. **Tools Used**: 
   - **Wireshark**: Network packet capture and analysis.
   - **dig command**: Used to generate DNS requests to specific domains.
   - **SSH**: Command-line tool used for simulating login attempts.

---

## Traffic Analysis Steps
### Step 1: Capture Network Traffic
- Opened Wireshark and selected the primary network interface (`**eth0**`).
- Started the capture by clicking the green "Start" button.

### Step 2: Simulate Suspicious Activities
1. **DNS Requests**:
   - Used the `dig` command to query DNS for random domain names, simulating requests to potentially malicious servers.
   - Example command: `dig randomname1.com`
2. **High Volume Data Transfer**:
   - Initiated a large file download to simulate data exfiltration.

### Step 3: Apply Filters and Analyze
- **DNS Filter**: Used `dns` filter to locate DNS requests in the capture.
- **High-Volume Traffic**: Used `tcp && frame.len > 1000` filter to identify large data packets.

---

## Suspicious Findings

### 1. Unusual DNS Requests
   - **Description**: We observed DNS queries for several unusual and non-existent domains, which might indicate malware trying to contact command-and-control (C2) servers.
   - **Details**:
     - **Source IP**: `192.168.85.129`
     - **Destination IP**: `192.168.85.2`
     - **Domain Names Queried**: `randomname1.com`
   - **Screenshot**: Refer to [dns-lookup.png](./screenshots/dns-lookup.png)
   - **Packet Capture File**: Captured packets are stored in [suspicious-traffic.pcap](./wireshark-capture-files/suspicious-traffic.pcap).

### 2. Large Data Transfers
   - **Description**: Observed large data transfer sessions that could simulate data exfiltration attempts.
   - **Details**:
     - **Source IP**: `192.168.85.129`
     - **Destination IP**: `212.183.159.230`
     - **Data Volume**: High volume, with packet sizes exceeding typical requests.
     - **Protocol**: TCP
   - **Screenshot**: Refer to [large-download.png](./screenshots/large-download.png)
   - **Packet Capture File**: Captured packets are stored in [suspicious-traffic-2.pcap](./wireshark-capture-files/suspicious-traffic-2.pcap).

---

## Conclusion and Recommendations
This analysis demonstrated the detection of suspicious traffic patterns in network traffic using Wireshark. The findings highlight the importance of monitoring DNS requests and data transfer volumes as part of regular network security practices.

### Recommendations
1. **Firewalls**: Restrict outgoing DNS requests to trusted servers.
2. **Data Transfer Policies**: Limit large data transfers and monitor unusual volumes.

These practices can help detect and mitigate similar suspicious activities on a network.

---

