# Incident Report 001 — [Short descriptive title]

**Status:** Draft — awaiting honeypot data
**Analyst:** [Your name]
**Report date:** YYYY-MM-DD
**Incident window:** YYYY-MM-DD HH:MM – HH:MM UTC
**Severity:** Low | Medium | High
**Classification:** [e.g. Unauthorized access attempt — commodity automated activity]

---

## 1. Executive summary

<!-- Three to four sentences. What happened, to what, when, and what the
     outcome was. Written so a non-technical reader gets the whole picture
     without reading further. No jargon, no adjectives. -->

---

## 2. Timeline

All times UTC.

| Time | Event | Source |
|------|-------|--------|
| | | |

<!-- Every entry must be traceable to a log line. If you inferred something
     rather than observed it, mark it clearly as an inference. -->

---

## 3. Affected asset

| Field | Value |
|-------|-------|
| Hostname | |
| Role | |
| Exposure | |
| Data at risk | |

---

## 4. Attacker infrastructure

| Field | Value |
|-------|-------|
| Source IP | |
| ASN / Provider | |
| Geolocation | |
| Reputation (AbuseIPDB) | |
| Reputation (GreyNoise) | |
| First seen | |
| Last seen | |
| Total attempts | |

<!-- Geolocation indicates where infrastructure is hosted, not where an
     operator is. State it that way. -->

---

## 5. Observed activity

### 5.1 Access attempt

<!-- Credentials attempted, rate, pattern. Note whether the username list
     suggests targeted or generic credential stuffing. -->

### 5.2 Post-access behaviour

<!-- Commands executed in the honeypot session, in order. Payload URLs
     (defanged: hxxp://). What the payload appeared to be, based on
     observation rather than assumption. -->

---

## 6. TTPs observed

| ATT&CK ID | Technique | Evidence |
|-----------|-----------|----------|
| | | |

---

## 7. Detection

| Rule ID | Level | Custom? | Description |
|---------|-------|---------|-------------|
| | | | |

**Time to detection:** <!-- from first event to first alert -->

<!-- Note which detections were built-in and which you wrote. If a stage of
     the chain was not detected, say so here — that is a finding, not a
     failure to hide. -->

---

## 8. Containment

<!-- What action was taken, automated or manual. If Active Response fired,
     give the rule and the block duration. If nothing was done because this
     was an observation honeypot, state that. -->

---

## 9. Assessment

<!-- What this activity was, and what it was not. Resist upgrading commodity
     scanning into something more dramatic. If the behaviour is consistent
     with automated botnet activity, say exactly that — it is the accurate
     finding and it reads as competence. -->

---

## 10. Lessons learned and recommendations

| # | Finding | Recommendation | Status |
|---|---------|----------------|--------|
| 1 | | | |

<!-- Recommendations should be specific and implementable. "Improve
     monitoring" is not a recommendation. "Add correlation rule keyed on
     destination username to catch distributed spray" is. -->

---

## Appendix A — Selected log evidence

```
<!-- Raw log lines supporting the timeline. Defang all URLs and IPs of
     external infrastructure. Redact anything from your own environment
     that should not be public. -->
```
