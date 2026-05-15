\# Wireshark PCAP Analysis



\## Project Overview



This project demonstrates network traffic analysis using Wireshark.  

The goal of the investigation is to identify suspicious network activity, analyze packets, extract indicators of compromise, and prepare a clear SOC-style investigation report.



\## Objective



The main objectives of this analysis are:



\- inspect network packets;

\- identify suspicious IP addresses;

\- analyze DNS, HTTP, TCP, and ARP traffic;

\- detect abnormal communication patterns;

\- document findings;

\- provide security recommendations.



\## Tools Used



\- Wireshark

\- Kali Linux

\- PCAP sample file

\- VirusTotal

\- AbuseIPDB



\## Investigation Steps



\### 1. Opened the PCAP File



The network capture file was opened in Wireshark for packet inspection.



\### 2. Applied Basic Filters



The following filters were used during analysis:



```wireshark

dns

http

tcp

arp

ip.addr == suspicious\_ip

tcp.flags.syn == 1

