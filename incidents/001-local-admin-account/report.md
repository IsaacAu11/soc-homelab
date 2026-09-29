# Incident Report: Local Admin Account Creation

**Date/time:** 2026-09-29, 18:xx BST
**Affected host:** <agent.name> (Windows 10 VM)
**Detection source:** Wazuh rule <rule.id>, level <rule.level>
**MITRE ATT&CK:** <rule.mitre.id and technique name>

## Summary
- A new local account was created and added to the Administrators 


## Timeline
| Time | Event |
|------|-------|
| Sep 29, 2026 @ 18:43:30.528 | Account `testuser` created |
| Sep 29, 2026 @ 18:44:26.278 | `testuser` added to Administrators |

## Investigation
- What the alert showed (account name, who made the change, which process)
- What you checked (other events around that time, failed logons, new processes)
- Whether the activity was expected

## Response actions
- Real incident: disable or delete the account, reset credentials, review other activity from that account, isolate the host if needed.
- Here: account deleted with `net user testuser /delete`.

## Lessons learned / detection notes
- Was the rule level appropriate?
- What extra logging would help?
