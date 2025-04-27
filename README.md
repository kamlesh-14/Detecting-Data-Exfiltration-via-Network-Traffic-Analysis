# Detecting-Data-Exfiltration-via-Network-Traffic-Analysis


## Project Objective
Detect unauthorized data transfer (data exfiltration) by analyzing network traffic using Wireshark.

---

## Tools Used
- Wireshark
- Kali Linux (Attacker Machine)
- Metasploitable 2 (Victim Machine)
- Netcat (for simulating data exfiltration)

---

## Steps Performed

1. **Lab Setup**:
   - Set up Kali Linux and Metasploitable 2 on VirtualBox with the same NAT network.

2. **Simulated Data Exfiltration**:
   - Used `netcat` to send a sensitive file from the attacker to the victim over a non-standard port (1234).

3. **Traffic Capture**:
   - Started capturing traffic using Wireshark.
   - Applied filter: `tcp.port == 1234`

4. **Traffic Analysis**:
   - Identified TCP traffic on port 1234.
   - Inspected packets and observed the transfer of sensitive data in the payload.

---

## Observations

- **Non-Standard Port Usage**:
  - The attacker used **TCP port 1234**, which is not typically used for standard services.

- **Cleartext Data Transfer**:
  - Sensitive information like **passwords** was observed being sent without any encryption. You can look into screenshot, the orange highlighted box shows the info of the file shared into clear text.

- **Packet Analysis**:
  - Using the **Follow TCP Stream** feature, the sensitive file content could be reconstructed from the captured packets.

- **Indicators of Exfiltration**:
  - Abnormal communication between two internal IPs.
  - Presence of large payloads in TCP packets.
  - TCP flags `[PSH, ACK]` indicated active data transfer rather than simple connection establishment.

- **Captured Evidence**:
  - Wireshark screenshot shows the data payload containing:
    > "this is a sensitive file containing passwords"

---

## Conclusion

By analyzing network traffic using Wireshark, we successfully detected a simulated data exfiltration attempt.
This project demonstrates how SOC Analysts can identify abnormal data flows, unauthorized communications, and signs of data breaches by closely inspecting network activity.

---
