# SIEM-Detection-Lab
## Objective
Deploy a Wazuh SIEM, ingest real attack telemetry from an
internet-exposed honeypot, and build/tune custom detection
rules against observed adversary behaviour.

## Target detection coverage
| ATT&CK ID | Technique | Platform | Status |
|-----------|-----------|----------|--------|
| T1110.001 | Brute Force: Password Guessing | Linux | Not started |
| T1078 | Valid Accounts | Linux | Not started |
| T1105 | Ingress Tool Transfer | Linux | Not started |
| T1059.001 | PowerShell | Windows | Not started |
| T1053.005 | Scheduled Task | Windows | Not started |
| T1547.001 | Registry Run Key Persistence | Windows | Not started |
| T1003.001 | LSASS Memory | Windows | Not started |
| T1136.001 | Create Local Account | Windows | Not started |

## Success criteria
- Every technique above is Detected, Partial, or a documented Gap
- At least one full intrusion chain documented end to end
- False-positive rate measured before and after tuning

## Status
Phase 0 complete — scope defined. Lab build in progress.
