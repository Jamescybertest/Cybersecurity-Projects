# Task 1: Stealthy TCP SYN Scan

## Task Overview: You have been asked to perform a network reconnaissance without alerting the target's security systems. This requires conducting a port scan that doesn't complete the TCP handshake, thereby reducing the likelihood of detection. By sending SYN packets and waiting for responses, you can infer which ports are open, closed, or filtered without establishing a full connection.

## Purpose of the Scan
The goal of this scan was to perform stealthy reconnaissance on a remote host to identify open ports and running services without triggering the target's intrusion detection systems (IDS) or firewalls. This technique is useful during the early phase of vulnerability assessments or penetration tests, where staying undetected is crucial.

---

## Command Used

sudo nmap -sS seclists.org
```

- `-sS`: Performs a **TCP SYN scan** — sends SYN packets and listens for SYN-ACK replies without completing the handshake.
- `sudo`: Required for low-level packet crafting during stealth scans.

---

## Scan Summary

- **Target:** `seclists.org`
- **Resolved IP:** `50.116.1.184`
- **Host Status:** Up (Latency: 0.065s)
- **Reverse DNS:** `ack.nmap.org`
- **Total Ports Scanned:** 1000
- **Ports Open:** 22 (SSH), 80 (HTTP), 443 (HTTPS)
- **Ports Closed:** 70 (Gopher), 113 (Ident), 31337 (Elite)
- **Ports Filtered:** 994 (no response)

---

## Explanation of Results

| Port | State   | Service | Meaning |
|------|---------|---------|---------|
| 22/tcp | Open   | SSH     | Secure remote login is active. May be used for admin access. 
| 80/tcp | Open   | HTTP    | Web server running unencrypted content. 
| 443/tcp | Open  | HTTPS   | Secure web server with SSL/TLS encryption. 
| 70/tcp | Closed | Gopher  | Responded but service is not active. Legacy protocol. 
| 113/tcp | Closed | Ident | Refused connection. Often used to identify users. 
| 31337/tcp | Closed | Elite | Port used historically in backdoor or demo scenarios. Not in use here. 

**Filtered Ports:** 994 ports gave no response, likely blocked by a firewall.

---

## Real-World Value of This Technique

- **Low detection risk:** This SYN scan avoids triggering logs in basic firewalls or intrusion detection systems.
- **Quick service enumeration:** Identifies open ports and critical services without alerting defenders.
- **Common in red team operations:** Used during the initial recon phase to quietly map a target.
- **Supports vulnerability analysis:** Knowing which services are exposed allows analysts to probe for known exploits or misconfigurations.

---

This task demonstrated how to stealthily enumerate services using TCP SYN scanning a fundamental skill for any cybersecurity analyst involved in network reconnaissance or penetration testing.
