# Wireshark-Packet-Capture-and-Protocol-Analysis

# 🛡️ Cybersecurity Internship – Task 5  

---

## 🎯 Objective

The purpose of this task is to use **Wireshark** to capture and analyze network traffic between **Kali Linux** and **Metasploitable2** virtual machines. This allows us to understand how basic tools like `ping` and `nmap` generate packets and how different protocols behave on a network.

You will generate traffic, capture it live, filter based on IP and protocol, and analyze packet-level data.

---

## 🧪 Lab Setup

| Component         | Configuration           |
|------------------|--------------------------|
| Attacking Machine| Kali Linux (VM)          |
| Target Machine   | Metasploitable2 (VM)     |
| Kali IP Address  | `192.168.134.129`        |
| Metasploitable IP| `192.168.134.132`        |
| Network Mode     | VMware NAT               |
| Interface Used   | `eth0` on Kali           |
| Tools Used       | Wireshark, Ping, Nmap    |

---

## 🖼️ Network Diagram

Kali Linux (192.168.134.129)
│
└── NAT (VMware Network)
│
Metasploitable (192.168.134.132)

---

🚀 Step-by-Step Guide:

  1️⃣ Start Wireshark on Kali:
    - command: sudo wireshark
    - interface: eth0
    - action: "Click the green shark fin to start capture"
    - screenshot: images/Wireshark.png

  2️⃣ Generate Traffic from Kali to Metasploitable:
    🔹 Ping the Target:
      - command: ping 192.168.134.132
      - description: "Generates ICMP Echo Request and Reply packets"
      - screenshot: images/ping_scan.png

    🔹 Scan Target with Nmap:
      - command: nmap -sS -sV 192.168.134.132 -v -T3
      - description: "Sends TCP SYN packets, detects service banners"
      - screenshot: images/nmap_scan.png

  3️⃣ Stop Packet Capture:
  
    - step_1: "Go back to Wireshark"
  
    - step_2: "Click the red Stop button"
    
    - step_3: "Save the capture file"
    
    - filename: metasploitable_scan_capture.pcap

---

filters:
  - protocol: ICMP
    command: icmp && ip.addr == 192.168.134.132
    screenshot: images/ICMP_Filter.png

  - protocol: TCP
    command: tcp && ip.addr == 192.168.134.132
    screenshot: images/TCP_Filter.png

  - protocol: FTP
    command: ftp && ip.addr == 192.168.134.132
    screenshot: images/FTP_Filter.png

  - protocol: HTTP
    command: http && ip.addr == 192.168.134.132
    screenshot: images/HTTP_Filter.png
---

 Observations:

- Target is alive (confirmed via ICMP ping)
- Nmap revealed open ports and services
- FTP and HTTP banners were captured
- No UDP traffic (UDP scan was not used)
