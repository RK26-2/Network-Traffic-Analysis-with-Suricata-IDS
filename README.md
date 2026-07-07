# Hands-On Network Traffic Analysis with Suricata IDS

## Project Overview
This project demonstrates an end-to-end workflow for network threat detection and log forensics using Suricata IDS. Acting as a Security Analyst, I verified custom detection signatures, simulated corporate network traffic using packet captures (`.pcap`), and utilised advanced command-line parsing to isolate high-value alert metadata.

---

## Core Tasks Executed

### 1. Rule Diagnostics
I inspected custom Suricata signatures (`sid:12345`) to identify active triggers targeting outbound unencrypted HTTP `GET` traffic leaving the internal network environment.


### 2. Traffic Simulation & Alert Validation
I processed a sample network PCAP file through the Suricata engine while bypassing checksum errors to ensure complete log generation. I then interrogated the resulting `fast.log` file system layer to verify real-time alert triggers and connection endpoints.


### 3. Advanced JSON Parsing & Session Reconstruction
I leveraged `jq` commands on dense `eve.json` logs to strip out clutter and isolate specific event parameters like IPs, timestamps, and protocols. By pivoting on a unique `flow_id` attribute, I was able to string together and reconstruct an entire TCP session lifecycle for deep-dive investigation.

---

## Lessons Learned & Post-Incident Review
This project taught me a lot about tuning rules and managing logs. First, the custom rule I tested is way too broad for a real network. It alerts on *every* single HTTP GET request, which would cause massive alert fatigue for a real SOC team. In the future, rules need to be much more specific, targeting things like malicious User-Agents or bad domains. 

On the logging side, I learned that raw JSON files are a nightmare to read manually during an active incident. However, using `jq` to filter by `flow_id` completely changed the look. It made it incredibly easy to piece the whole network conversation back together. Finally, seeing clear-text HTTP traffic on Port 80 is a reminder that organisations need to enforce HTTPS across the board to protect data from sniffing.

---

## Project Deliverables
The comprehensive operational review, risk metrics, and mitigation strategies resulting from this analysis have been compiled into a formal document:

📄 **[Download the Official SOC Incident Report (PDF)](./Network-Traffic-Analysis-with-Suricata-IDS.pdf)**

**Snapshots**

[Images](./image)
