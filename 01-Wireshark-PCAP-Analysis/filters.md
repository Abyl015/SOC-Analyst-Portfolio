# Wireshark Filters

This file contains useful Wireshark display filters for SOC Analyst investigations.

## Basic Protocol Filters

```wireshark
ip
tcp
udp
dns
http
tls
icmp
arp
```

## Host-Based Filters

```wireshark
ip.addr == 192.168.1.10
ip.src == 192.168.1.10
ip.dst == 8.8.8.8
```

## Port-Based Filters

```wireshark
tcp.port == 80
tcp.port == 443
tcp.port == 22
tcp.port == 445
tcp.port == 3389
udp.port == 53
```

## TCP Investigation Filters

```wireshark
tcp
tcp.flags.syn == 1
tcp.flags.syn == 1 and tcp.flags.ack == 0
tcp.flags.reset == 1
tcp.analysis.retransmission
tcp.analysis.lost_segment
```

## DNS Investigation Filters

```wireshark
dns
dns.qry.name
dns.flags.response == 0
dns.flags.response == 1
dns.qry.name contains "example"
```

Purpose:

- identify DNS queries;
- find suspicious domains;
- detect repeated domain lookups;
- check DNS responses;
- investigate possible malware or phishing-related domains.

## HTTP Investigation Filters

```wireshark
http
http.request
http.request.method == "GET"
http.request.method == "POST"
http.host
http.user_agent
```

Purpose:

- inspect web requests;
- identify visited hosts;
- check suspicious URLs;
- review User-Agent values;
- detect possible credential submission or file download activity.

## TLS / HTTPS Filters

```wireshark
tls
tcp.port == 443
tls.handshake.type == 1
```

Purpose:

- identify encrypted HTTPS sessions;
- review TLS handshakes;
- identify external communication over port 443.

## ICMP Filters

```wireshark
icmp
icmp.type == 8
icmp.type == 0
```

Purpose:

- identify ping requests and replies;
- check host discovery activity;
- detect possible reconnaissance.

## ARP Filters

```wireshark
arp
arp.opcode == 1
arp.opcode == 2
arp.duplicate-address-detected
```

Purpose:

- analyze local network communication;
- detect possible ARP spoofing indicators;
- identify duplicate IP address issues.

## Suspicious Activity Filters

### Possible Port Scanning

```wireshark
tcp.flags.syn == 1 and tcp.flags.ack == 0
```

### Failed TCP Connections

```wireshark
tcp.flags.reset == 1
```

### HTTP POST Requests

```wireshark
http.request.method == "POST"
```

### DNS Queries Only

```wireshark
dns.flags.response == 0
```

### Traffic from Specific Host

```wireshark
ip.src == 192.168.1.10
```

### Traffic to Specific Host

```wireshark
ip.dst == 192.168.1.10
```

### Traffic Between Two Hosts

```wireshark
ip.addr == 192.168.1.10 and ip.addr == 8.8.8.8
```

## Useful Wireshark Menu Sections

- Statistics -> Protocol Hierarchy
- Statistics -> Conversations
- Statistics -> Endpoints
- Statistics -> I/O Graphs
- File -> Export Objects -> HTTP

## Notes

These filters are used during packet analysis to identify suspicious traffic, DNS queries, HTTP requests, retransmissions, unusual connections, and possible scanning activity.

The example IP addresses and domains should be replaced with real values during practical analysis.
