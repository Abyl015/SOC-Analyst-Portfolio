\# Indicators of Compromise - Case 01



\## Case Name



Malicious Traffic Analysis



\## Summary



This file contains indicators of compromise identified during the malicious traffic analysis case.



\## IP Addresses



| IP Address | Type | Description | Verdict |

|-----------|------|-------------|---------|

| 10.2.28.88 | Internal | Suspicious internal host | Likely compromised |

| 45.131.214.85 | External | Suspicious external destination | Suspicious |



\## Domains



| Domain | Description | Verdict |

|--------|-------------|---------|

| easyas123.tech | Suspicious domain observed in DNS traffic | Suspicious |



\## URLs



| URL | Description | Verdict |

|-----|-------------|---------|

| http://45.131.214.85/fakeurl.htm | Repeated HTTP POST destination | Suspicious |



\## Network Activity



| Activity | Description |

|----------|-------------|

| DNS query | Suspicious domain lookup related to `easyas123.tech` |

| HTTP POST | Repeated outbound POST requests to `/fakeurl.htm` |

| External communication | Communication with unknown external IP `45.131.214.85` |

| Possible C2 | Behavior consistent with command-and-control communication |



\## Detection Ideas



\### Wireshark Filters



```wireshark

ip.addr == 10.2.28.88

ip.addr == 45.131.214.85

dns.qry.name contains "easyas123"

http.request.method == "POST"

http.request.uri contains "fakeurl"
``` 

