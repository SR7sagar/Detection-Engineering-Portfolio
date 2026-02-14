  # Investigation Guide: Multiple Failed Logins Followed by Successful Authentication

## Alert Context

This detection identifies potential brute force or password spraying activity where multiple failed authentication attempts are followed by a successful login from the same source IP address within a defined timeframe.

This pattern may indicate:
- Credential brute forcing
- Password spraying
- Account compromise using valid credentials

---

## Initial Triage Steps

1. Identify the affected user account.
2. Confirm the source IP address (internal vs external).
3. Perform IP reputation check.
4. Validate login geography and ASN.
5. Determine whether MFA was enabled and successfully completed.
6. Compare login timing against known user behavior baseline.

---

## Investigation Pivot Strategy

If suspicious:

- Review all authentication attempts from the same IP within 24 hours.
- Check if multiple accounts were targeted from that IP.
- Inspect endpoint telemetry linked to the user.
- Look for privilege escalation events.
- Check for unusual file access or data exfiltration attempts.

---

## Indicators of Confirmed Compromise

- Login from unfamiliar country or TOR/VPN provider.
- High-value account targeted (admin, service account).
- Post-authentication lateral movement activity.
- Unusual PowerShell or process execution events after login.

---

## Escalation Criteria

Escalate to Incident Response if:

- Source IP is malicious or high-risk.
- The account has elevated privileges.
- Suspicious activity occurs post-authentication.
- Multiple users show similar activity patterns.

---

## MITRE ATT&CK Mapping

- T1110 – Brute Force
- T1078 – Valid Accounts
