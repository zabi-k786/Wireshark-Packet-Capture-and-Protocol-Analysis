# 🛡️ Cybersecurity Internship – Task 5

# Wireshark-Packet-Capture-and-Protocol-Analysis

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
📸 **Network Machines**  
**Kali Linux VM**  
![Kali Linux](https://github.com/zabi-k786/Wireshark-Packet-Capture-and-Protocol-Analysis/blob/main/Kali_Linux.png)

**Metasploitable VM**  
![Metasploitable](https://github.com/zabi-k786/Wireshark-Packet-Capture-and-Protocol-Analysis/blob/main/Metasploitable.png)

---
---

🚀 Step-by-Step Guide:

  1️⃣ Start Wireshark on Kali:
    - command: sudo wireshark
    - interface: eth0
    - action: "Click the green shark fin to start capture"
  ![Wireshark](https://github.com/zabi-k786/Wireshark-Packet-Capture-and-Protocol-Analysis/blob/main/Wireshark.png)
  ![Wireshark_2](https://github.com/zabi-k786/Wireshark-Packet-Capture-and-Protocol-Analysis/blob/main/Wireshark_2.png)

  ### 2️⃣ Generate Traffic from Kali to Metasploitable:

#### 🔹 Ping the Target:
- **Command:**  
  `ping 192.168.134.132`  
- **Description:**  
  Generates ICMP Echo Request and Reply packets

📸 Screenshot:  
![Ping Scan](https://github.com/zabi-k786/Wireshark-Packet-Capture-and-Protocol-Analysis/blob/main/ping_scan.png)

---

#### 🔹 Scan Target with Nmap:
- **Command:**  
  `nmap -sS -sV 192.168.134.132 -v -T3`  
- **Description:**  
  Sends TCP SYN packets, detects service banners

📸 Screenshot:  
![Nmap Scan](https://github.com/zabi-k786/Wireshark-Packet-Capture-and-Protocol-Analysis/blob/main/nmap_scan.png)


  3️⃣ Stop Packet Capture:
  
    - step_1: "Go back to Wireshark"
  
    - step_2: "Click the red Stop button"
    
    - step_3: "Save the capture file"
    
    - filename: metasploitable_scan_capture.pcap

---

filters:
  - protocol: ICMP
    command: icmp && ip.addr == 192.168.134.132
    ![ICMP Filter](https://github.com/zabi-k786/Wireshark-Packet-Capture-and-Protocol-Analysis/blob/main/ICMP_Filter.png)

  - protocol: TCP
    command: tcp && ip.addr == 192.168.134.132
    ![TCP Filter](https://github.com/zabi-k786/Wireshark-Packet-Capture-and-Protocol-Analysis/blob/main/TCP_Filter.png)

  - protocol: FTP
    command: ftp && ip.addr == 192.168.134.132
    ![FTP Filter](https://github.com/zabi-k786/Wireshark-Packet-Capture-and-Protocol-Analysis/blob/main/FTP_Filter.png)

  - protocol: HTTP
    command: http && ip.addr == 192.168.134.132
    ![HTTP Filter](https://github.com/zabi-k786/Wireshark-Packet-Capture-and-Protocol-Analysis/blob/main/HTTP_Filter.png)
---

 Observations:

- Target is alive (confirmed via ICMP ping)
- Nmap revealed open ports and services
- FTP and HTTP banners were captured
- No UDP traffic (UDP scan was not used)

---
