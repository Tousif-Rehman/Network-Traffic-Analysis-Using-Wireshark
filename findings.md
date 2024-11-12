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
  - [FTP Login Capture on Metasploitable](#ftp-login-capture-on-metasploitable)
- [Conclusion and Recommendations](#conclusion-and-recommendations)

---

## Environment Setup
1. **Operating System**: Kali Linux running in a VMware virtual environment.
2. **Network Configuration**: The network adapter was set to "Bridged" mode to capture internet traffic across the local network.
3. **Tools Used**: 
   - **Wireshark**: Network packet capture and analysis.
   - **dig command**: Used to generate DNS requests to specific domains.
   - **FTP Client**: Used to simulate FTP login attempts to a Metasploitable VM, capturing login credentials transmitted in plaintext.

---

## Traffic Analysis Steps
### Step 1: Capture Network Traffic
- Opened Wireshark and selected the primary network interface (`eth0`).
- Started the capture by clicking the green "Start" button.

### Step 2: Simulate Suspicious Activities
1. **DNS Requests**:
   - Used the `dig` command to query DNS for random domain names, simulating requests to potentially malicious servers.
   - Example command: `dig randomname1.com`

2. **High Volume Data Transfer**:
   - Initiated a large file download to simulate data exfiltration.

3. **FTP Login Capture**:
   - Captured an FTP login session to a Metasploitable VM, where the login credentials (username and password) were transmitted in plaintext over the network.
   - Used Wireshark to capture FTP traffic during the login attempt, observing the clear-text transmission of the `msfadmin` username and password.
   - This step highlights the risk of unencrypted protocols like FTP, as sensitive information is vulnerable to interception.


### Step 3: Apply Filters and Analyze
- **DNS Filter**: Used `dns` filter to locate DNS requests in the capture.
- **High-Volume Traffic**: Used `tcp && frame.len > 1000` filter to identify large data packets.
- **FTP Login Capture**: Used `ftp` filter to locate FTP login packets. This filter helps identify unencrypted FTP traffic, including usernames and passwords transmitted in plaintext. By applying this filter, we could isolate FTP packets, enabling us to analyze and capture sensitive login details such as `msfadmin` username and password being sent over the network.

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
     - **Source IP**: `212.183.159.230`
     - **Destination IP**: `192.168.85.129`
     - **Data Volume**: High volume, with packet sizes exceeding typical requests.
     - **Protocol**: TCP
   - **Screenshot**: Refer to [large-download.png](./screenshots/large-download.png)
   - **Packet Capture File**: Captured packets are stored in [suspicious-traffic-2.pcap](./wireshark-capture-files/suspicious-traffic-2.pcap).

### 3. FTP Login Capture on Metasploitable  
   - **Description**: Captured an FTP login session to a Metasploitable VM, revealing the transmission of the       `msfadmin` username and password in plaintext.  
   - **Risk**: FTP transmits login credentials without encryption, exposing sensitive information to potential interception by attackers on the same network.       
   - **Screenshot**: [metasploitable-ftp-login.png](./screenshots/metasploitable-ftp-login.png)  

---

## Conclusion and Recommendations
This analysis demonstrated the detection of suspicious traffic patterns in network traffic using Wireshark. The findings highlight the importance of monitoring DNS requests and data transfer volumes as part of regular network security practices.

### Recommendations
1. **Firewalls**: Restrict outgoing DNS requests to trusted servers.
2. **Data Transfer Policies**: Limit large data transfers and monitor unusual volumes.
3. **FTP Alternatives**: Replace FTP with more secure protocols like SFTP or FTPS to ensure the protection of sensitive information.  


These practices can help detect and mitigate similar suspicious activities on a network.

---

