<div align="center">

# 🛡️ IDS Threat Detection Lab - Suricata

  <p align="center">
    Hands-on network security sandbox demonstrating real-time threat detection and security telemetry generation.
  </p>

[![Suricata Version](https://shields.io)](https://suricata.io)
[![Lab Environment](https://shields.io)](https://virtualbox.org)
[![SIEM Layer](https://shields.io)](https://github.com)
[![License](https://shields.io)](https://opensource.org)

---
</div>

## 🌐 Lab Architecture

To better visualize how the attack machine triggers the IDS, the lab utilizes an isolated virtual network mapping malicious activity directly into Suricata's ingestion engine:

```mermaid
graph LR
    subgraph Isolated_Network ["Isolated VirtualBox Network: 192.168.56.0/24"]
        Kali["🐱 Kali Linux (Attacker)<br>192.168.56.102"] 
        Ubuntu["🐧 Ubuntu 20.04 (IDS Server)<br>192.168.56.101"]
    end

    subgraph Suricata_Engine ["Suricata Engine"]
        Interface["📋 Interface: enp0s8"]
        Rules["⚙️ Custom local.rules"]
        Logs["📂 EVE JSON Telemetry"]
    end

    Kali -->|Generates Scans / Pings / Exploits| Ubuntu
    Ubuntu --> Interface
    Interface --> Rules
    Rules -->|SIEM-Ready Alerts| Logs
```

# IDS Threat Detection Lab - Suricata

## Overview
Hands-on Suricata IDS lab demonstrating real-time threat detection and network packet capture on an isolated home network.

## Lab Architecture
- **IDS Server:** Ubuntu 20.04 (192.168.56.101) - Suricata 7.0.10
- **Attack Machine:** Kali Linux (192.168.56.102)
- **Network:** VirtualBox Host-Only (192.168.56.0/24)

## Attack Simulation
- ** Step 1 - Generate Network Traffic
ping -c 5 192.168.56.101
![Network_Traffic](screenshot/Generate_Network_Traffic.png)

# Port Scanning
nmap 192.168.56.101
![Attack Simulation](screenshot/Nmap_scan.png)

- ** Step 2 - Suricata Detection
sudo suricata -c /etc/suricata/suricata.yaml -i enp0s8 -l /var/log/suricata -v
Suricata successfully captures all network traffic on enp0s8 and this confirms
that the custom rule signature was triggered by the simulated traffic
![Suricata Activated](screenshot/Suricata_activated.png)

- ** Step 3 - EVE JSON validation
EVE JSON format enables easy parsing and all attacks generated detections in eve.json with proper timestamps,
source/destination IPs, and protocol information
![EVE JSON](screenshot/Eve_json_alerts.png)

- ## 📊 Alert Output Example (EVE JSON with Full Context)

## Detection Rules (Custom)
1. ICMP Ping Detection (SID: 1000001)
2. Port Scan Detection (SID: 1000002)
3. SSH Connection Attempt (SID: 1000003)
4. HTTP Connection (SID: 1000004)

```json
{
  "timestamp": "2026-08-20T12:34:56.789123+0000",
  "src_ip": "192.168.56.102",
  "src_port": 54321,
  "dst_ip": "192.168.56.101",
  "dst_port": 22,
  "proto": "TCP",
  "alert": {
    "signature": "SSH Connection Attempt",
    "severity": 3,
    "signature_id": 1000003
  },
  "tcp": {
    "flags": "SYN",
    "window": 65535
  }
}

## Quick Start
```bash
sudo suricata -c /etc/suricata/suricata.yaml -i enp0s8 -l /var/log/suricata -v

## Test Result
✅ All attacks detected in real-time
✅ EVE JSON alerts captured successfully
✅ Zero false positives in lab environment

## Files
• Suricata-config/suricata.yaml-Suricata configuration
• Suricata-rules/local.rules-Custom detection rules
• detection-logs/eve.json-Captured network events

Skills Demonstrated
✔️ IDS/IPS configuration and deployment
✔️ Detection rule creation (Snort syntax)
✔️ Real-time threat monitoring
✔️ Network packet analysis
✔️ EVE JSON alert format (SIEM-ready)


## 🔮 Next-Gen Expansion: SIEM Integration
Because this lab captures all events in the standard `eve.json` format, the logical next step is SIEM forwarding. 
* To see how to correlate these alerts with authentication anomalies:
"check out my companion lab: [SSH Brute-Force Detection & Analysis -Splunk SIEM](https://github.com/Ug111/SSH-Brute-Force-Detection-Splunk)"


This lab demonstrates hands-on understanding of threat detection workflows and the detection layer of SOC operations.
