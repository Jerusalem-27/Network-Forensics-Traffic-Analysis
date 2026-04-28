# Network Forensics & Traffic Analysis

---

## Overview  
Performed a network forensic investigation to analyze packet-level data, identify security risks, and reconstruct attacker activity from captured traffic. This project demonstrates how sensitive information can be exposed in transit and how attackers can extract credentials and files directly from network communications when encryption is not enforced.

Using packet analysis, log correlation, and behavioral inspection, the investigation uncovers credential exposure, file reconstruction, and suspicious network behavior.

---

## Investigation Evidence  

### 1. HTTP Traffic Analysis  

<p align="center">
  <img src="./evidence/01 - http-traffic-analysis.png" width="800">
</p>

Analyzed HTTP traffic to identify communication patterns between internal and external systems, confirming unencrypted web activity.

---

### 2. FTP Credential Extraction  

<p align="center">
  <img src="./evidence/02 - ftp-credentials-extraction.png" width="800">
</p>

Captured plaintext FTP authentication using TCP stream reconstruction, exposing valid username and password transmitted over the network.

---

### 3. File Reconstruction from Traffic  

<p align="center">
  <img src="./evidence/03 - file-reconstruction.png" width="800">
</p>

Reconstructed transferred file directly from packet capture, demonstrating how attackers can recover sensitive data from network traffic.

---

### 4. Firewall Log Analysis  

<p align="center">
  <img src="./evidence/04 - firewall-log-analysis.png" width="800">
</p>

Analyzed pfSense firewall logs to validate network behavior and identify blocked and allowed traffic patterns.

---

### 5. Routing & Traffic Path Analysis  

<p align="center">
  <img src="./evidence/05 - routing-analysis.png" width="800">
</p>

Reviewed routing table configuration and identified static route influencing traffic flow toward external systems.

---

## Detection Logic Summary  

The detection logic focuses on identifying insecure data transmission, credential exposure, and suspicious network behavior through packet analysis and log correlation.

- Monitored network traffic for unencrypted protocols (FTP, HTTP) to detect sensitive data transmitted in plaintext  
- Identified credential exposure by inspecting FTP authentication commands within packet streams  
- Reconstructed TCP sessions to analyze full communication and verify data exchange  
- Detected file transfer activity and reconstructed files from packet data to confirm data exposure  
- Correlated packet capture with firewall logs to validate outbound connections and traffic patterns  
- Analyzed repeated communication with external hosts to identify potential data transfer or suspicious activity  
- Reviewed routing configurations to detect abnormal static routes influencing traffic flow  

This approach enables early identification of insecure communication, potential data leakage, and network misconfigurations that could be exploited by attackers.

---

## Attack Scenario  
An attacker gains visibility into network traffic through packet capture or a Man-in-the-Middle position.

To exploit the environment, the attacker:
- Captures unencrypted network traffic  
- Extracts credentials transmitted over FTP  
- Reconstructs files from packet data  
- Monitors communication with external systems  
- Leverages routing weaknesses to influence traffic flow  

Without encryption and proper network controls, this allows credential theft and data exfiltration.

---

## Detection Focus  
- Plaintext authentication (FTP)  
- Credential exposure in network traffic  
- File transfer reconstruction from packets  
- External communication patterns  
- Routing anomalies and static route manipulation  
- Unencrypted data transmission risks  

---

## Data Sources  
- Packet Capture (PCAP Data)  
- Firewall Logs (pfSense)  
- Network Device Configuration (Routing Table)  

---

## Investigation Approach  

1. Traffic Collection  
   Captured full packet data to analyze all network communications  

2. Protocol Analysis  
   Filtered traffic based on protocols (FTP, TCP, IP)  

3. Credential Identification  
   Identified plaintext credentials transmitted over FTP  

4. Session Reconstruction  
   Used TCP stream reconstruction to analyze full sessions  

5. File Recovery  
   Extracted transferred file directly from packet data  

6. Log Correlation  
   Correlated packet data with firewall logs  

7. Behavioral Analysis  
   Identified repeated external communication patterns  

8. Infrastructure Review  
   Analyzed routing table and detected abnormal static route  

---

## Key Findings  
- High: Credentials exposed via plaintext FTP communication  
- High: Sensitive file successfully reconstructed from packet capture  
- Medium: Repeated communication with external host  
- Medium: Suspicious static route affecting traffic behavior  
- High: Lack of encryption enables full data visibility  

---

## Security Improvements  
- Replace FTP with secure protocols (SFTP / FTPS)  
- Enforce encryption for all sensitive communications (TLS)  
- Monitor outbound traffic for anomalies  
- Audit and validate routing configurations  
- Strengthen firewall rules and logging visibility  

---

## MITRE ATT&CK Mapping   
- T1040 – Network Sniffing  
- T1557 – Adversary-in-the-Middle  
- T1071.002 – Application Layer Protocol: FTP  
- T1005 – Data from Local System  

---

## Technologies & Tools  
- Wireshark (Packet Analysis)  
- pfSense (Firewall Logs)  
- GNS3 (Network Simulation)  
- FileZilla (FTP Traffic Simulation)  
- PuTTY (Remote Access)  

---

## Skills Demonstrated  
- Network Traffic Analysis  
- Network Forensics & Investigation  
- Credential Exposure Detection  
- Packet-Level Data Reconstruction  
- Log Correlation & Analysis  
- Routing & Infrastructure Analysis  

---
 ## Why This Project Matters  

Unencrypted network traffic remains a critical security risk in many environments. This project demonstrates how attackers can extract credentials and recover sensitive data directly from packet captures when secure protocols are not enforced. It highlights the importance of encryption, network visibility, and log correlation in detecting and preventing data exposure within modern security operations.

## Conclusion  

This investigation demonstrated how insecure protocols, lack of encryption, and weak network visibility can expose sensitive data to interception and analysis. By correlating packet captures, firewall logs, and routing configurations, the analysis provided a complete view of network behavior and uncovered critical risks, including credential exposure and data reconstruction. The findings reinforce the need for secure communication protocols, continuous monitoring, and layered defensive controls to protect data in transit and reduce the risk of compromise.

## Disclaimer  
This project was conducted in a controlled environment using simulated network traffic for defensive security and forensic analysis purposes.
