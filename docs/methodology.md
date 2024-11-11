# Methodology for Network Traffic Analysis Using Wireshark

## Overview
This document outlines the methodology used for capturing, filtering, and analyzing network traffic in order to identify suspicious DNS requests and large data transfers. The objective is to demonstrate how network anomalies can indicate potential security threats and how Wireshark can be used to analyze these activities.

---

## Table of Contents
- [Environment Setup](#environment-setup)
- [Traffic Capture Process](#traffic-capture-process)
- [Simulating Suspicious Activity](#simulating-suspicious-activity)
- [Applying Filters and Analyzing Packets](#applying-filters-and-analyzing-packets)
- [Saving and Documenting Findings](#saving-and-documenting-findings)

---

## Environment Setup

1. **Operating System**: Kali Linux was used as it provides pre-installed security tools and a flexible environment for packet analysis.
2. **Virtual Machine**: Kali Linux was set up in a VMware virtual machine for ease of configuration and isolation from the main network.
3. **Network Configuration**: The network adapter for the virtual machine was set to "Bridged" mode to capture and analyze network traffic as if it were part of the same physical network.
4. **Tools**: 
   - **Wireshark**: Installed on Kali Linux for network packet capture and analysis.
   - **dig command**: Used to generate DNS queries to simulate requests to potentially malicious domains.

---

## Traffic Capture Process

1. **Launch Wireshark**: Open Wireshark on Kali Linux.
2. **Select Network Interface**: Choose the appropriate network interface from the list (usually `eth0` or `wlan0` in a bridged setup).
3. **Start Capture**: Click the green "Start" button to begin capturing network traffic on the selected interface.
4. **Monitor for Suspicious Patterns**: Allow traffic to accumulate, monitoring for any unusual network patterns.

---

## Simulating Suspicious Activity

To create realistic scenarios for analysis, we simulated suspicious activities as follows:

### 1. Unusual DNS Requests
   - **Objective**: Generate DNS requests to random or non-existent domain names, which might mimic malware contacting command-and-control (C2) servers.
   - **Method**: Using the `dig` command to query non-existent or unusual domain names from the Kali Linux terminal.
   - **Commands**:
     ```bash
     dig randomname1.com
     ```
   - **Explanation**: These commands request IP address resolution for unusual domain names, which may not exist or appear suspicious. The queries appear in Wireshark as DNS requests, allowing us to filter and analyze them later.

### 2. Large Data Transfers
   - **Objective**: Simulate a high-volume data transfer to observe if large packet sizes might indicate data exfiltration.
   - **Method**: Downloaded a large file or transferred substantial data using a browser or file transfer tool.
   - **Steps**:
     - Open a web browser and download a large file from the internet, such as a Linux distribution ISO or large media file.
   - **Explanation**: Large or unusual data transfers could indicate attempts to send significant data out of the network. By observing these patterns, we can practice identifying potential exfiltration activities.

---

## Applying Filters and Analyzing Packets

Once the traffic was captured, filters were applied in Wireshark to target specific types of packets related to DNS requests and large data transfers:

1. **DNS Requests Analysis**:
   - **Filter Applied**: `dns`
   - **Purpose**: Filters out all DNS traffic, allowing us to identify queries to unusual or non-existent domains.
   - **Steps**:
     - Enter `dns` in the filter bar to display only DNS packets.
     - Look for domain names that seem random or untrustworthy, as they may represent suspicious activity.
   - **Example**: A query for `randomname1.com` appeared, indicating an attempt to contact an unknown domain.

2. **Large Data Transfer Analysis**:
   - **Filter Applied**: `tcp && frame.len > 1000`
   - **Purpose**: Filters for large TCP packets, useful for identifying high-volume data transfers.
   - **Steps**:
     - Enter `tcp && frame.len > 1000` in the filter bar to display only large TCP packets.
     - Analyze the source and destination IP addresses to understand where the large data transfer is directed.
   - **Example**: Observed packets above 1000 bytes sent from a local IP address to an external server, indicating potential data exfiltration.

---

## Saving and Documenting Findings

1. **Saving Captured Packets**:
   - **Method**: After the capture, stop the recording and save the file in `.pcap` format.
   - **File Naming**: Name the file meaningfully, e.g., `suspicious-traffic.pcap`, and store it in the `/wireshark-capture-files` directory for reference.
   - **Steps**:
     - Click on "File" > "Save As" and save the captured packets with a `.pcap` extension.

2. **Taking Screenshots**:
   - **Purpose**: Capture screenshots of significant findings, such as DNS queries or large packets, to include in reports.
   - **Steps**:
     - In Wireshark, locate the packet of interest.
     - Take a screenshot of the packet details and save it in the `/screenshots` folder (e.g., `dns-lookup.png` for DNS queries).

3. **Documenting Observations**:
   - **Report Findings**: Record each observation in the `findings.md` file, including details about IP addresses, domain names, and protocols associated with suspicious traffic.
   - **Include Screenshots**: Reference screenshots to illustrate key findings.
   - **Structure**: Document each finding under clear headings, e.g., "Unusual DNS Requests" and "Large Data Transfers."

---

## Conclusion
This methodology provides a structured approach for capturing, filtering, and analyzing network traffic in Wireshark. By simulating specific types of suspicious activities, this project demonstrates how Wireshark can be used effectively for network security analysis. This approach can help identify potential security threats and strengthen overall network monitoring practices.

---

