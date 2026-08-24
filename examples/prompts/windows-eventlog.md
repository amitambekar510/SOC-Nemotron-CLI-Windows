# Windows Event Log Analysis

## Use Case
Parse Windows Event Logs (EVTX), extract Event IDs, source IPs, user accounts, and generate Sigma rules.

## Prompt
```powershell
opencode "Read {{EVTX_FILE}}, extract all Event IDs {{EVENT_IDS}}, extract source IPs, user accounts, and timestamps. Defang IPs and output to {{OUTPUT_FILE}}.json with fields: event_id, timestamp, source_ip, user, logon_type, status, message."
```

## Example Usage
```powershell
opencode "Read Security.evtx, extract all Event ID 4624 (Logon) and 4625 (Failed Logon) events. Extract source IPs, usernames, logon types, and timestamps. Defang IPs. Output to logon_analysis.json with fields: event_id, timestamp, source_ip, user, logon_type, status, message."
```

## Expected Output Format
```json
[
  {
    "event_id": 4624,
    "timestamp": "2024-01-15T10:30:45.123Z",
    "source_ip": "192.168.1[.]100",
    "user": "admin",
    "logon_type": 10,
    "status": "success",
    "message": "An account was successfully logged on."
  }
]
```

## Skill Level
- **Beginner** - Basic EVTX parsing with `Get-WinEvent`
- **Intermediate** - Multi-log correlation, Sigma rule generation
- **Expert** - Automated threat hunting pipelines