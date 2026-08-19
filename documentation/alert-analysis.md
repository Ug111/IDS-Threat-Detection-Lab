```markdown
# Suricata IDS Lab - Alert Analysis Report

## Test Date: August 16, 2026

## Environment
- **IDS Server:** Ubuntu 20.04 (192.168.56.101)
- **Attack Source:** Kali Linux (192.168.56.102)
- **Network:** Host-only 192.168.56.0/24
- **Suricata Version:** 7.0.10

## Lab Results
✅ Suricata configured successfully
✅ 365 rules loaded (4 custom + 361 default)
✅ EVE JSON alert output enabled
✅ Real-time packet capture active

## Attack Detection Results
| Attack Type | Detection Rule |   Status     |
|-------------|----------------|--------------|
| ICMP Ping   |    SID 1000001 |  ✅ Detected |
| Port Scan (nmap) | SID 1000002| ✅ Detected |
| SSH Connection | SID 1000003 |  ✅ Detected |
| HTTP Traffic | SID 1000004 |    ✅ Detected |

## Technical Achievements
- 4 custom detection rules created from scratch
- EVE JSON alert logging enabled
- Real-time packet capture on enp0s8 interface
- Sub-100ms detection latency
- Zero configuration errors

## Conclusion
Lab demonstrates hands-on proficiency in IDS configuration, detection rule creation, and threat detection workflows essential for SOC roles.
