# Investigation Guide: Suspicious Addition to Local Administrators Group

## Alert Context
This detection identifies when an account is added to the local **Administrators** group. This may indicate privilege escalation after initial access or misuse of administrative tooling.

---

## Immediate Triage Questions
1. **Who added the account?** (SubjectUserName)
2. **Which account was added?** (MemberName / TargetUserName fields depending on log source)
3. **Which host generated the event?** (Computer / hostname)
4. **When did it happen?** Is it within an approved change window?
5. **Is the added account expected to be admin?** (role, department, ticket approval)

---

## Key Evidence to Collect
- Event details for **4732** (group membership change)
- Any nearby:
  - **4624** successful logons for the subject account
  - **4672** special privileges assigned to new logon (high privilege session indicator)
  - Additional **4732/4733** activity (multiple group changes)

---

## Investigation Pivot Strategy
- Search for other admin group changes by the same **SubjectUserName** in the last 24 hours.
- Check whether the **added account** logged in shortly after being promoted.
- Look for remote execution patterns (e.g., admin share access, service creation) after the change.
- Identify if multiple endpoints were modified (sign of widespread compromise).

---

## Indicators of Compromise
- Admin group membership change performed by an unusual account.
- Change occurs outside normal working hours or change window.
- Added account is newly created or rarely used.
- Immediate suspicious activity after elevation (lateral movement, credential dumping, new services).

---

## Escalation Criteria
Escalate to Incident Response if:
- The actor account is not an approved admin or no change ticket exists.
- The added account gains privileged access unexpectedly.
- There is evidence of post-change malicious activity.
- Multiple systems show similar admin group modifications.

---

## MITRE ATT&CK Mapping
- T1068 – Exploitation for Privilege Escalation
- T1098 – Account Manipulation
