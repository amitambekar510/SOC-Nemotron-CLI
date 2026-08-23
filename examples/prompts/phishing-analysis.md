# Phishing Email Header Analysis

## Use Case
Parse email headers, extract sender IP path, SPF/DKIM/DMARC results, and identify anomalies.

## Prompt
```bash
opencode "Read {{EML_FILE}}, parse all headers, extract: sender IP path (Received chain), SPF/DKIM/DMARC results, authentication results, message IDs, hop delays, and identify anomalies (SPF fail, DKIM mismatch, DMARC fail, suspicious routing, unusual delays, mismatched domains). Output as {{OUTPUT_FILE}}.json with fields: headers_parsed, spf_result, dkim_result, dmarc_result, ip_path, anomalies, risk_score."
```

## Example Usage
```bash
opencode "Read suspicious_email.eml, parse all headers, extract: sender IP path (Received chain), SPF/DKIM/DMARC results, authentication results, message IDs, hop delays, and identify anomalies (SPF fail, DKIM mismatch, DMARC fail, suspicious routing, unusual delays, mismatched domains). Output as phishing_analysis.json with fields: headers_parsed, spf_result, dkim_result, dmarc_result, ip_path, anomalies, risk_score."
```

## Expected Output Format
```json
{
  "headers_parsed": true,
  "spf_result": "fail",
  "dkim_result": "fail",
  "dmarc_result": "fail",
  "ip_path": [
    {"hop": 1, "from": "mail.suspicious[.]xyz (192.0.2.100)", "by": "mx.company[.]com", "delay_ms": 12},
    {"hop": 2, "from": "mx.company[.]com", "by": "internal.company[.]com", "delay_ms": 3}
  ],
  "anomalies": [
    {
      "type": "spf_fail",
      "description": "SPF check failed: 192.0.2.100 not authorized for suspicious[.]xyz",
      "severity": "high"
    },
    {
      "type": "dkim_mismatch",
      "description": "DKIM signature domain (attacker[.]com) != From domain (company[.]com)",
      "severity": "high"
    },
    {
      "type": "dmarc_fail",
      "description": "DMARC policy reject, both SPF and DKIM failed",
      "severity": "critical"
    },
    {
      "type": "suspicious_routing",
      "description": "Email routed through 3 unrelated countries before delivery",
      "severity": "medium"
    }
  ],
  "risk_score": 92,
  "recommendation": "Block sender domain/IP, update spam filters, user awareness training"
}
```

## Skill Level
- **Beginner** - Basic header parsing
- **Intermediate** - Authentication analysis, hop analysis
- **Expert** - ML-based classification, threat actor attribution