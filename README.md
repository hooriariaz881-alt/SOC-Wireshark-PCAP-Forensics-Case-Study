 **SOC-Wireshark-PCAP-Forensics-Case-Study**
A hands-on network traffic forensics investigation using Wireshark to analyze a PCAP file, track a C2 server, and extract IOCs.
 🛡️ SOC Incident Investigation: **Network Traffic Forensics (PCAP Analysis)**

 📌 **Executive Summary**
This project demonstrates a hands-on network forensic investigation using **Wireshark**. The objective was to analyze a malicious packet capture (PCAP) file, identify an infected internal host, trace communication with a Command and Control (C2) server, and extract key Indicators of Compromise (IoCs).


🔍 **Investigation Steps & Findings**

 **Step 1:** Finding the Infected IP
  Analysis:
  Filtered the traffic to locate suspicious HTTP and TLS handshakes, discovering an internal IP engaging in anomalous external connections.
Infected IP: `10.1.21.58`
<img width="458" height="243" alt="image" src="https://github.com/user-attachments/assets/fdae3bc4-ded2-4fc4-9c36-8841feb9ff3c" />


 **Step 2:** Identifying MAC Address & Hostname
Analysis: Inspected NBNS (NetBIOS Name Service) traffic to determine the endpoint details.
  MAC Address: `00:21:5d:c8:0e:f2`
  Hostname: `DESKTOP-ES9F3ML<20>`
  <img width="465" height="196" alt="image" src="https://github.com/user-attachments/assets/5ebf001c-788d-45cb-bdcd-3a5871aec926" />


 **Step 3:** Determining Windows Username
Analysis: Analyzed Kerberos (`kerberos.CNameString`) traffic to trace user authentication details.
Username: `gwyatt`
<img width="461" height="257" alt="image" src="https://github.com/user-attachments/assets/5cb3a286-b0e1-413b-a23b-10d89a3683ee" />


**Step 4 & 5:** Identifying Primary C2 Server & Timeline
Analysis: Filtered specific IP traffic (`153.92.1.49`) to track the exact timeline of the first malicious callback[cite: 1].
  C2 Server IP: `153.92.1.49`
  First Activity Date: `2026-01-27`
  First Activity Time: `23:05:36`
<img width="459" height="259" alt="image" src="https://github.com/user-attachments/assets/1228a7a3-ba41-4069-83c6-b31d2f32a727" />

 **Step 6:** Secondary Malicious Domains
Domains Identified: 
  1. `hammernew.su`
  2. `heavylussy.su`

**step 7:** Threat Intelligence & VirusTotal Check
Analysis: Queried the C2 IP on VirusTotal to check security vendor reputation.
  Result: Flagged as malicious by multiple security vendors (Community Score / Detections confirmed).
<img width="458" height="235" alt="image" src="https://github.com/user-attachments/assets/9615287c-6e57-48f5-961d-89764a007ec0" />


 **🛠️ Tools Used**
Wireshark: Packet analysis, filtering (`ip.addr`, `kerberos`, NBNS), and stream tracking.
VirusTotal: Threat intelligence and IOC validation.

**💡 Mitigation & Recommendations**
1. Isolate the infected host (`10.1.21.58`) immediately from the network.
2. Block the malicious C2 IP (`153.92.1.49`) and associated domains at the firewall/perimeter level.
3. Perform a full disk scan on user `gwyatt`'s machine for persistence mechanisms.
