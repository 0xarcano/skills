## Context

See proposal.md for motivation. This repo is an Agent Skills catalog: published skills live under `skills/<name>/` from `templates/skill/`, with concise `SKILL.md` and optional `references/`. No catalog skills exist yet; this change adds the first domain skill and the family-standard wallet audit report outline.

Constraints: extension-only v1 (Chromium and Firefox WebExtensions); desktop (Frame app, Electron) is a sibling skill; hardware/AA/MPC/mobile/custodial out of scope. Agents are strongest on readable artifacts (source, manifests, configs)—design for that, not silicon or live phishing campaigns.

## Goals / Non-Goals

**Goals:**

- Ship a usable hybrid audit skill agents can apply to Rabby-class and Frame **extension** targets (including Firefox builds).
- Keep `SKILL.md` short; put specialized depth in `references/`.
- Define a **canonical markdown audit report** that sibling `wallet-audit-*` skills reuse with the same headings (content-only variance).
- Make sibling boundaries obvious in description and out-of-scope handling.

**Non-Goals:**

- Implementing desktop/mobile/AA/MPC/hardware sibling skills in this change.
- Bundling runnable exploit scanners or offensive payloads.
- Replacing professional human audits or claiming formal certification.
- Full OWASP ASVS reprint inside the skill.
- Alternate report formats (YAML-only, HTML, PDF) as the primary agent output.

## Decisions

### D1: Skill identity `wallet-audit-extension-eoa`

- **Choice:** Folder and frontmatter name `wallet-audit-extension-eoa`.
- **Why:** Encodes surface (extension) + account model (EOA) so siblings (`wallet-audit-desktop-eoa`, etc.) do not collide; description carries MetaMask/Rabby/Frame-extension / Firefox trigger terms.
- **Alternatives:** `wallet-audit` (too broad once siblings exist); `metamask-class-wallet-audit` (brand-locked).

### D2: Hybrid workflow (classify → specialized gates → thin standard pass → report)

- **Choice:** Mandatory specialized gates for custody, isolation, consent, connectivity, privacy; then a thin standard extension/app security and privacy pass; standard markdown report last.
- **Why:** Matches exploration consensus—wallet fund-loss paths are not covered by generic ASVS alone; pure threat-model-only is too vague for consistent agent runs.
- **Alternatives:** Checklist-only dump; threat-model-first without gates.

### D3: Progressive disclosure layout

```
skills/wallet-audit-extension-eoa/
  SKILL.md                 # workflow, scope, report pointer, links
  references/
    custody.md             # seed/vault/export/clipboard
    isolation.md           # WebExtensions / MV3 + Firefox notes, provider inject
    consent-signing.md     # decode, blind sign, EIP-712, approvals
    connectivity.md        # RPC, chain config, WalletConnect
    privacy.md             # telemetry, RPC leakage, fingerprinting
    findings-severity.md   # severity rubric + finding field definitions
    report-template.md     # canonical markdown report (family standard)
```

- **Why:** Keeps `SKILL.md` under catalog size norms; agents load only the gate they are on; report template is copyable by siblings.
- **Alternatives:** Single monolithic `SKILL.md`; shared cross-skill package now (defer physical extraction until a second sibling exists—structure is already the standard).

### D4: Family-standard markdown report (not YAML-primary)

- **Choice:** Primary audit output is markdown using fixed section headings (see spec). Finding rows/sections use: id, title, asset, evidence, severity, wallet_impact, description, remediation.
- **Why:** Human-readable, diff-friendly, consistent across sibling skills; YAML-only findings rejected as the primary contract.
- **Sibling rule:** Future `wallet-audit-*` skills MUST keep the same heading outline and finding fields; only fill different content (surface metadata, gate coverage rows, finding text).
- **Canonical outline:**

```markdown
# Wallet Audit Report

## Metadata
## Executive Summary
## Scope and Method
## Findings Summary
## Findings
## Gate Coverage
## Standard Security and Privacy Pass
## Residual Risks and Recommendations
## Appendix   <!-- optional -->
```

- **Alternatives considered:** YAML frontmatter + freeform body; per-skill custom report shapes (rejected—breaks comparability).

### D5: Companion/native bridge handling

- **Choice:** In-scope for **extension-side** trust-boundary findings only; do not claim desktop verification.
- **Why:** Frame-shaped products share a brand across two surfaces; separate skills per primary surface.

### D6: `disable-model-invocation: true` initially

- **Choice:** Match template default so the skill is explicitly invoked / selected, not ambient-applied to every crypto mention.
- **Why:** Wallet audit is high-stakes and easy to mis-trigger; user/agent should opt in.
- **Alternatives:** Auto-invoke on wallet keywords (risk of noisy/wrong application).

### D7: Cross-browser extension wording

- **Choice:** Isolation reference covers WebExtensions patterns for Chromium and Firefox; call out MV3 service-worker specifics where they differ.
- **Why:** Proposal scope is browser-extension, not Chrome-only.

## Risks / Trade-offs

| Risk | Mitigation |
|------|------------|
| Skill becomes a generic Chrome-extension checklist | Lead with specialized gates; standard pass is explicitly “thin” and wallet-scored; Firefox called out in isolation ref |
| Agents overclaim (e.g. “verified hardware display”) | Hard non-goals + companion-bridge language in workflow |
| Reference drift / timelessness | Prefer durable patterns over vendor CVE lists; no “before date X” instructions |
| Sibling report drift | Spec requires identical headings/fields; `report-template.md` is the copy source until a shared package is extracted |
| Offensive misuse | Authorized-review framing; no exploit PoC instructions in skill body |

## Migration Plan

- Add skill under `skills/wallet-audit-extension-eoa/` from template; no migration of existing catalog content.
- Rollback: delete the skill directory (no runtime coupling).
- Future siblings: copy `references/report-template.md` (or later extract to a shared path) and keep headings/fields identical; optionally extract shared severity + report into a common package once two siblings exist.

## Open Questions

- None blocking. Optional later: extract `report-template.md` + severity rubric to a shared catalog path when the desktop sibling ships.
