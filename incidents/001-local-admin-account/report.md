# Incident Report: Local Admin Account Creation

**Date/time:** 2026-09-29, 18:43 BST\
**Affected host:** windows-victim (Windows 10 VM)\
**Detection source:** **Wazuh** rule 60109, level 8\
**MITRE ATT&CK:** T1098 Account Manipulation (Persistence))

## Summary

A new local account called `testuser` was created on the host and then added to the Administrators group. This was a planned test simulating an attacker setting up a backdoor admin account.

## Timeline

| Time | Event |
|------|-------|
| Sep 29, 2026 @ 18:43:30 | Account `testuser` created |
| Sep 29, 2026 @ 18:44:26 | `testuser` added to Administrators |

## Investigation

The account creation alert (rule 60109) shows that `vboxuser` created `testuser` from logon session `0xc4ae8`. The event does not record which process ran the command, so I could not confirm that from the alert alone.

I checked the surrounding events on the host for anything unusual and found nothing beyond my own testing. The activity was expected, since I ran `net user` and `net localgroup administrators` myself to simulate persistence. I classed it as a false positive.

## Response actions

On a real incident I would disable the account, reset the credentials of whoever created it, look for other new accounts or persistence and isolate the host if compromise was confirmed.

Here I removed the test account with `net user testuser /delete`.

## Lessons learned

- Rule 60109 fired at level 8. That felt low for a possible persistence step, so in a real environment I would want it raised or correlated with the admin group change.
- The two events alert separately. Linking them into one alert would make triage quicker.
