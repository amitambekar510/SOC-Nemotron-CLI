# Sigma Detection Rule Authoring

## Use Case
Generate valid Sigma detection rules from malicious activity logs with MITRE ATT&CK mapping.

## Prompt
```bash
opencode "Analyze {{LOG_FILE}} and generate a valid Sigma detection rule targeting {{ATTACK_TECHNIQUE}} with MITRE ATT&CK mapping. Include: title, id (UUID), status, description, logsource, detection logic (selection/condition), level, tags with MITRE ATT&CK IDs, false positive considerations, and test cases."
```

## Example Usage
```bash
opencode "Analyze malicious_ps_execution.log and generate a valid Sigma detection rule targeting obfuscated PowerShell commands with MITRE ATT&CK mapping. Include: title, id, status, description, logsource, detection logic, level, tags with MITRE ATT&CK IDs, false positive considerations, and test cases."
```

## Expected Output Format
```yaml
title: Obfuscated PowerShell Execution Detected
id: a1b2c3d4-e5f6-7890-abcd-ef1234567890
status: experimental
description: Detects encoded/obfuscated PowerShell command-line patterns commonly used to evade logging and bypass execution policies.
author: SOC-Nemotron-CLI
date: 2024/01/15
logsource:
  category: process_creation
  product: windows
detection:
  selection:
    Image|endswith: '\powershell.exe'
    CommandLine|contains:
      - '-enc'
      - '-EncodedCommand'
      - 'IEX('
      - 'Invoke-Expression'
      - 'FromBase64String'
      - 'System.Text.Encoding'
      - '-nop'
      - '-w hidden'
      - '-windowstyle hidden'
  condition: selection
level: high
tags:
  - attack.execution
  - attack.t1059.001
  - attack.t1027
falsepositives:
  - Legitimate administrative scripts using encoded commands
  - Automated deployment tools using encoded PowerShell
level: high
```

## Skill Level
- **Beginner** - Basic rule generation from single log
- **Intermediate** - Multi-log correlation, false positive tuning
- **Expert** - Cross-platform rules, CI/CD integration, automated testing