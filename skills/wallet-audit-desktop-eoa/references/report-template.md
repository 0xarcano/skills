# Wallet Audit Report — template

**Family standard:** All related `wallet-audit-*` catalog skills MUST emit this markdown structure (same headings and finding fields). Change **content only** (metadata values, gate names/notes, finding bodies, skill-specific scope language). Do not rename sections or switch to YAML-only / ad-hoc formats as the primary output.

Copy this outline and fill every required section. Omit **Appendix** only if empty.

```markdown
# Wallet Audit Report

## Metadata

| Field | Value |
|-------|-------|
| Target name | |
| Version / commit | |
| Skill id | wallet-audit-desktop-eoa |
| Surface | desktop / Electron |
| Custody model | non-custodial EOA/HD |
| Audit date | |
| Authorization / scope | Authorized review of [artifact]. |

## Executive Summary

<!-- Short overall risk posture (2–4 sentences). -->

| Severity | Count |
|----------|------:|
| Critical | 0 |
| High | 0 |
| Medium | 0 |
| Low | 0 |
| Informational | 0 |

## Scope and Method

**In scope:**

**Out of scope:**

**Gates performed:** Custody, Process/IPC isolation, Consent/signing, Connectivity, Privacy, thin standard security/privacy pass.

**Limitations / not verified:**

## Findings Summary

| ID | Title | Severity | Wallet impact | Gate |
|----|-------|----------|---------------|------|
| | | | | |

## Findings

### [SEVERITY] ID — Title

- **Asset:**
- **Evidence:**
- **Wallet impact:**
- **Description:**
- **Remediation:**

<!-- Repeat one subsection per finding. -->

## Gate Coverage

| Gate | Status | Notes |
|------|--------|-------|
| Custody | Reviewed / Partial / Skipped | |
| Process / IPC isolation | | |
| Consent / signing | | |
| Connectivity | | |
| Privacy | | |

<!-- Sibling skills may rename gate *rows* to match their surface; keep this section heading. -->

## Standard Security and Privacy Pass

<!-- Brief notes or cross-references to finding IDs (auto-update, code signing, deps, Electron flags, secrets in repo). -->

## Residual Risks and Recommendations

1.
2.
3.

## Appendix

<!-- Optional: threat sketches, Electron WebPreferences excerpts, build hashes. -->
```
