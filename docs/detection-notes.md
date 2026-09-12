# Detection notes

Per-technique validation records. One entry per ATT&CK technique, written at
the time the detection was tested. Each entry records what was executed, what
fired, why it fired, and what the detection would miss.

---

## T1110.001 — Brute Force: Password Guessing

**Status:** Detected
**Platform:** Linux (Ubuntu 24.04 LTS)
**Date validated:** 2026-09-11

### Test performed

Five consecutive failed SSH authentication attempts as a non-existent user
(`fakeuser`) from 192.168.56.1 against the Wazuh server, within a ~20 second
window.

### Rules that fired

| Rule ID | Level | Type | Description |
|---------|-------|------|-------------|
| 5710 | 5 | Atomic | sshd: attempt to login using a non-existent user |
| 5503 | 5 | Atomic | PAM: user login failed |
| 2502 | 10 | Correlation | User missed the password more than one time |

### Data source

`journald` → `wazuh-logcollector` → `wazuh-analysisd` → alerts.log / indexer

### Analysis

Rules 5710 and 5503 are atomic: each evaluates a single log line in isolation
and is scored at level 5, because one failed login is indistinguishable from
ordinary user error and is not actionable on its own.

Rule 2502 is frequency-based. It fires only when repeated failures accumulate
from the same source within a defined time window, and is scored at level 10
as a result. This is the alert an analyst would action.

The two rule types serve different purposes: the atomic rules build the
evidence trail used during investigation, while the correlation rule provides
the trigger. A detection strategy that relied only on atomic rules would bury
the signal; one that relied only on correlation would lose the detail needed
to scope the incident.

Alerts were automatically tagged with PCI DSS, HIPAA, NIST 800-53, GDPR and
TSC control mappings by the default Wazuh ruleset.

### Gap identified

Correlation depends on repeated failures from a single source against a single
host within the rule's time window. A low-and-slow spray — one attempt per
source IP, or attempts spaced beyond the correlation window — would produce
only level 5 atomic events and never escalate.

**Possible mitigation (not yet implemented):** an aggregation rule keyed on
target username rather than source IP, to catch distributed attempts against
a single account.

### Evidence

`screenshots/t1110-brute-force.png`

---

## TEMPLATE — copy this block for each new technique

## TXXXX.XXX — Technique name

**Status:** Detected | Partial | Gap
**Platform:**
**Date validated:**

### Test performed

<!-- What exactly was executed. Be specific enough that someone could repeat
     it: the command, the source, the target, the timing. -->

### Rules that fired

| Rule ID | Level | Type | Description |
|---------|-------|------|-------------|
| | | | |

<!-- If nothing fired, say so plainly and record it as a Gap. A documented
     gap is a valid result. -->

### Data source

<!-- Which log channel or module produced the telemetry. If the detection
     required extra configuration (Sysmon event ID, auditd rule, localfile
     block), note it here — this is what makes the detection reproducible. -->

### Analysis

<!-- Why this fired, or why it didn't. What the rule is actually keying on.
     Whether it is atomic or correlation-based, and what that implies. -->

### Gap identified

<!-- What this detection would miss. Every detection has an evasion. Naming
     it is the point of this section — do not leave it blank. -->

### Evidence

<!-- screenshots/filename.png -->
