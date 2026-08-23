# IOC Extraction & Firewall Blocklist

## Use Case
Extract indicators of compromise from threat intelligence feeds and generate firewall-ready blocklists.

## Prompt
```bash
opencode "Read {{LOG_FILE}}, extract all {{IOC_TYPE}} (IPv4 addresses, domains, SHA256 hashes, emails), defang them (e.g., 192.168.1[.]1, example[.]com), and structure into {{OUTPUT_FILE}}.json with fields: type, value, source, confidence, tags."
```

## Example Usage
```bash
opencode "Read threat_feed_2024_01_15.txt, extract all IOCs (IPv4 addresses, domains, SHA256 hashes, emails), defang them, and structure into firewall_blocklist_2024_01_15.json with fields: type, value, source, confidence, tags."
```

## Expected Output Format
```json
[
  {
    "type": "ipv4",
    "value": "192.168.1[.]100",
    "source": "threat_feed_2024_01_15.txt",
    "confidence": "high",
    "tags": ["brute-force", "ssh", "botnet"]
  },
  {
    "type": "domain",
    "value": "malicious[.]example[.]com",
    "source": "threat_feed_2024_01_15.txt",
    "confidence": "medium",
    "tags": ["c2", "phishing"]
  }
]
```

## Skill Level
- **Beginner** - Basic IOC extraction
- **Intermediate** - Add enrichment (VT, AbuseIPDB lookups)
- **Expert** - Automated blocklist deployment to firewall APIs