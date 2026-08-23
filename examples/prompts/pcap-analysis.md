# PCAP Metadata Extraction & Analysis

## Use Case
Extract conversation summaries, top talkers, DNS queries, and suspicious patterns from PCAP files.

## Prompt
```bash
opencode "Read {{PCAP_FILE}}, extract conversation summary (top 20 by bytes/packets), top talkers (IP + port), DNS queries (query/response), HTTP hosts/URLs, TLS SNI, and suspicious patterns (port scans, beaconing, large transfers, known bad IPs). Output summary as {{OUTPUT_FILE}}.md with sections: executive summary, conversation table, DNS analysis, HTTP analysis, TLS analysis, anomalies, IOCs."
```

## Example Usage
```bash
opencode "Read capture_2024_01_15.pcap, extract conversation summary (top 20 by bytes/packets), top talkers (IP + port), DNS queries (query/response), HTTP hosts/URLs, TLS SNI, and suspicious patterns (port scans, beaconing, large transfers, known bad IPs). Output summary as pcap_analysis_2024_01_15.md with sections: executive summary, conversation table, DNS analysis, HTTP analysis, TLS analysis, anomalies, IOCs."
```

## Expected Output Format
```markdown
# PCAP Analysis Report

## Executive Summary
- File: capture_2024_01_15.pcap
- Duration: 02:15:33
- Total Packets: 1,245,678
- Total Bytes: 2.3 GB
- Unique IPs: 342

## Top 10 Conversations
| Rank | Src IP | Dst IP | Protocol | Packets | Bytes |
|------|--------|--------|----------|---------|-------|
| 1 | 192.168.1.50 | 203.0.113.45 | TCP/443 | 45,231 | 892 MB |
| 2 | 10.0.0.25 | 198.51.100.10 | TCP/80 | 32,109 | 456 MB |

## DNS Analysis
- Total Queries: 12,453
- Unique Domains: 1,204
- Suspicious: 3 (dga-domain[.]xyz, fast-flux[.]net)

## HTTP Analysis
- Total Requests: 8,921
- Unique Hosts: 234
- Suspicious: 2 (phishing-site[.]com, malware-drop[.]xyz)

## TLS Analysis
- Total Handshakes: 5,432
- SNI Anomalies: 1 (self-signed cert for internal IP)

## Anomalies Detected
1. **Port Scan** - 192.168.1.100 → 10.0.0.0/24 (1000+ SYN packets)
2. **Beaconing** - 10.0.0.50 → 203.0.113.45 every 60s ± 2s
3. **Large Transfer** - 192.168.1.50 → 203.0.113.45 (892 MB in 45 min)

## IOCs Extracted
- IPs: 203.0.113.45, 198.51.100.10
- Domains: dga-domain[.]xyz, fast-flux[.]net, phishing-site[.]com, malware-drop[.]xyz
```

## Skill Level
- **Beginner** - Basic metadata extraction
- **Intermediate** - Anomaly detection, correlation
- **Expert** - Custom protocol parsers, encrypted traffic analysis