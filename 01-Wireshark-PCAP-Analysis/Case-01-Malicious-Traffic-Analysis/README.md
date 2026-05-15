# Network Traffic Analysis with Wireshark

## Overview
This project demonstrates the analysis of network traffic using Wireshark. The goal was to identify suspicious activity, detect a potentially infected host, and distinguish malicious traffic from legitimate traffic.

## Tools Used
- Wireshark
- PCAP file analysis
- DNS inspection
- HTTP traffic analysis

## Objectives
- Identify suspicious internal host
- Analyze DNS queries
- Detect malicious external connections
- Differentiate between normal and suspicious traffic

## Key Findings

### Suspicious Host
- 10.2.28.88

### Suspicious Domain
- easyas123.tech

### Suspicious External IP
- 45.131.214.85

### Malicious Activity
The host **10.2.28.88** generated repeated HTTP POST requests to:

http://45.131.214.85/fakeurl.htm

This behavior is consistent with command-and-control (C2) communication, which indicates possible malware infection.

## Legitimate Traffic Identified
The following traffic was analyzed and identified as legitimate:
- Microsoft update traffic
- filestreamingservice requests
- connecttest.txt requests

These were verified based on trusted IP ranges and expected system behavior.

## Conclusion
The analysis revealed that the internal host **10.2.28.88** is likely compromised. Repeated outbound POST requests and suspicious DNS activity indicate potential malware communication with an external server.

## Screenshots
Screenshots of the analysis are provided in the `screenshots` folder:
- DNS queries
- HTTP POST requests
- Suspicious traffic patterns
- Normal traffic comparison
## Author
Abylai Kondybay – Cybersecurity student focused on SOC and network security.
