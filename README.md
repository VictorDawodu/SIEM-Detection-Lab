# SIEM Detection Lab

A home detection-engineering lab built on Wazuh 4.14. The goal is not to
install a SIEM but to use one: ingest real attack telemetry, write and tune
custom detection rules, validate coverage against MITRE ATT&CK, and document
both the detections and the gaps.

## Objective

Deploy a Wazuh SIEM, collect telemetry from Windows and Linux endpoints plus
an internet-exposed SSH honeypot, and build detections for credential-access
and initial-access techniques. Measure what is caught, and document what is
not.

## Architecture

| Host | OS | Role | Network |
|------|----|------|---------|
| `wazuh-server` | Ubuntu 24.04 LTS | Wazuh indexer, manager, dashboard | 192.168.56.10 (host-only) |
| `win-victim` | Windows 11 Enterprise | Monitored endpoint, Sysmon | 192.168.56.x (host-only) + NAT |
| `honeypot` | Ubuntu (cloud) | Cowrie SSH honeypot | Public IP |

Endpoints run the Wazuh agent and report to the manager on 1514/tcp. The
honeypot ships Cowrie's JSON session log to the same manager.

## Detection coverage

Coverage is tracked against MITRE ATT&CK. "Gap" entries are deliberate and
documented — see `documents/detection-notes.md` for the reasoning behind each.

| ATT&CK ID | Technique | Platform | Status | Rules |
|-----------|-----------|----------|--------|-------|
| T1110.001 | Brute Force: Password Guessing | Linux | Detected | 5710, 5503, 2502 |
| T1078 | Valid Accounts | Linux | Not started | — |
| T1105 | Ingress Tool Transfer | Linux | Not started | — |
| T1059.001 | Command and Scripting Interpreter: PowerShell | Windows | Not started | — |
| T1053.005 | Scheduled Task/Job | Windows | Not started | — |
| T1547.001 | Registry Run Keys / Startup Folder | Windows | Not started | — |
| T1003.001 | OS Credential Dumping: LSASS Memory | Windows | Not started | — |
| T1136.001 | Create Account: Local Account | Windows | Not started | — |

**Current: 1 of 8 detected.**

## Findings

<!-- Fill in once the honeypot has collected data. Keep it factual. -->

- Authentication attempts captured: _TBD_
- Unique source IPs: _TBD_
- Custom rules written: _TBD_
- Alert volume before / after tuning: _TBD_

## Documentation

- [`documents/detection-notes.md`](documents/detection-notes.md) — per-technique
  validation notes, rules that fired, and identified gaps
- [`documents/incident-report-001.md`](documents/incident-report-001.md) — full
  incident write-up of one observed intrusion chain

## Repository layout

```
├── documents/            Detection notes and incident reports
├── rules/           Custom Wazuh rules (local_rules.xml)
├── configs/         Sysmon config, ossec.conf snippets
└── screenshots/     Dashboard and alert evidence
```

## Build log

| Date | Milestone |
|------|-----------|
| 2026-09-11 | Wazuh 4.14.7 all-in-one deployed on Ubuntu 24.04 |
| 2026-09-11 | First detection validated: SSH brute force (T1110.001) |

## Notes on scope

This lab monitors systems I control. The honeypot is isolated, runs no real
shell, has egress filtering applied, and shares no credentials with any other
host. Adversary emulation is limited to the host-only network segment.

Attack traffic observed against the honeypot is commodity automated activity
— credential stuffing and scanning consistent with internet background
radiation. It is not attributed to any specific actor.
