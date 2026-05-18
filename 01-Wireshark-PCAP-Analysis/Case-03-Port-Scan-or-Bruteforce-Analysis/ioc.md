# Scan Indicators - Case 03

## Case Name

Port Scan Reconnaissance Analysis

## Summary

This file contains scan indicators, exposed services, and detection ideas identified during the Case 03 port scan reconnaissance analysis.

This is not a malware IOC list. It documents network observables related to scanning activity.

## Network Observables

| Type | Value | Description |
|------|-------|-------------|
| Scanner IP | `192.168.1.57` | Host that initiated the Nmap scan |
| Target IP | `192.168.1.49` | Scanned Windows host |
| Target MAC | `98:FA:9B:00:0A:27` | MAC address of target host |
| Target Hostname | `IT-01` | Hostname identified by Nmap |
| Target OS | Windows 10 / Windows 11 | OS estimate from Nmap |

## Open Ports and Services

| Port | Service | Description | Risk |
|------|---------|-------------|------|
| `80/tcp` | HTTP | Apache httpd 2.4.66 on Windows | Medium |
| `135/tcp` | MSRPC | Microsoft Windows RPC | Medium |
| `139/tcp` | NetBIOS-SSN | Windows NetBIOS session service | Medium |
| `445/tcp` | SMB | Microsoft SMB / microsoft-ds | High |
| `515/tcp` | Printer | Microsoft LPD | Medium |
| `3389/tcp` | RDP | Microsoft Terminal Services | High |
| `5357/tcp` | HTTPAPI | Microsoft HTTPAPI 2.0 | Medium |
| `7070/tcp` | SSL / Remote Access | AnyDesk Client certificate observed | High |

## Nmap Evidence

```cmd
nmap -sT 192.168.1.49 -oN case03-basic-scan.txt
nmap -sV 192.168.1.49 -oN case03-service-scan.txt
nmap -A 192.168.1.49 -oN case03-aggressive-scan.txt
```

## Wireshark Detection Filters

### Incoming SYN Packets to Target

```wireshark
ip.dst == 192.168.1.49 and tcp.flags.syn == 1 and tcp.flags.ack == 0
```

### Open Port Responses

```wireshark
ip.src == 192.168.1.49 and ip.dst == 192.168.1.57 and tcp.flags.syn == 1 and tcp.flags.ack == 1
```

### Reset Responses

```wireshark
ip.src == 192.168.1.49 and ip.dst == 192.168.1.57 and tcp.flags.reset == 1
```

### Traffic Between Scanner and Target

```wireshark
ip.addr == 192.168.1.57 and ip.addr == 192.168.1.49
```

## SIEM Search Ideas

```text
src_ip="192.168.1.57" AND dest_ip="192.168.1.49"
dest_ip="192.168.1.49" AND tcp_flags="SYN"
src_ip="192.168.1.57" AND count_distinct(dest_port) > 20
dest_ip="192.168.1.49" AND dest_port IN (80,135,139,445,515,3389,5357,7070)
```

## Detection Logic

A potential port scan can be detected when a single source IP sends TCP SYN packets to many destination ports on the same target within a short time window.

Example:

```text
If one source IP contacts more than 20 unique destination ports on the same destination IP within 5 minutes, generate a port scan alert.
```

## Recommended SOC Actions

- Confirm whether the scan from `192.168.1.57` was authorized.
- Investigate the scanner host if the scan was not expected.
- Review firewall and endpoint logs on `192.168.1.49`.
- Monitor repeated SYN packets to multiple destination ports.
- Restrict access to exposed services.
- Disable unnecessary services.
- Require VPN or allowlist access for RDP.
- Restrict SMB access to trusted systems only.
- Review AnyDesk usage and restrict remote access tools.
- Disable HTTP TRACE on Apache if not required.

## Final Verdict

The observed traffic is consistent with TCP port scanning and reconnaissance activity.

The scanner was identified as `192.168.1.57`, and the target was `192.168.1.49`. The target exposed multiple services, including HTTP, SMB, RDP, Microsoft HTTPAPI, and a remote access-related service associated with AnyDesk.
