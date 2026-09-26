## Context

See proposal.md for motivation. The catalog already ships `skills/wallet-audit-extension-eoa/` with a family-standard markdown Wallet Audit Report. That skill redirects Frame-class **desktop/Electron** targets to `wallet-audit-desktop-eoa`, which this change adds.

Constraints: desktop/Electron primary surface only; browser-extension primary surface stays with the sibling skill; hardware/AA/MPC/mobile/custodial remain out of scope. Agents are strongest on readable artifacts (source, Electron configs, preload/IPC surfaces)—design for that, not silicon or live phishing campaigns. Do not invent a second report schema.

## Goals / Non-Goals

**Goals:**

- Ship a usable hybrid audit skill for Frame-class desktop/Electron EOA targets.
- Keep `SKILL.md` short; put specialized depth in `references/`.
- Reuse the **exact** family report headings and finding fields; change content only (surface metadata, gate row names, finding bodies).
- Make sibling boundaries obvious (extension ↔ desktop companion as untrusted peer).

**Non-Goals:**

- Replacing or rewriting `wallet-audit-extension-eoa` beyond optional redirect polish.
- Mobile / AA / MPC / hardware sibling skills in this change.
- Bundling runnable exploit scanners or offensive payloads.
- Claiming formal certification or full OS-level forensics depth.
- Full OWASP ASVS / Electron security checklist reprint inside the skill.
- Alternate primary report formats (YAML-only, HTML, PDF).

## Decisions

### D1: Skill identity `wallet-audit-desktop-eoa`

- **Choice:** Folder and frontmatter name `wallet-audit-desktop-eoa`.
- **Why:** Mirrors `wallet-audit-extension-eoa` (surface + account model); description carries Frame desktop / Electron EOA trigger terms.
- **Alternatives:** `wallet-audit-electron` (too framework-locked if native non-Electron desktops appear later); `wallet-audit-frame` (brand-locked).

### D2: Same hybrid workflow, desktop-adapted gates

- **Choice:** classify → specialized gates → thin standard pass → family markdown report.
- **Gate mapping vs extension sibling:**

| Gate | Extension focus | Desktop focus |
|------|-----------------|---------------|
| Custody | Extension vault / IndexedDB | On-disk vault, OS keychain/keystore, memory/IPC leakage, export UX |
| Isolation | WebExtensions / provider inject | Electron main/renderer/preload, `contextIsolation`, `nodeIntegration`, IPC validation, deep links / protocol handlers |
| Consent / signing | Popup decode vs payload | Desktop window UX vs signed payload; same EIP-712 / blind-sign / approvals concerns |
| Connectivity | RPC, chain config, WC | Same, plus local sockets/IPC bridges to extension companions |
| Privacy | Telemetry, RPC leakage | Same, plus OS/crash-reporter and auto-update telemetry scrubbing |

- **Why:** Fund-loss paths still dominate; desktop threat surface differs mainly in isolation/custody storage.
- **Alternatives:** Fork an entirely different gate set (rejected—hurts family comparability in Gate Coverage).

### D3: Progressive disclosure layout

```
skills/wallet-audit-desktop-eoa/
  SKILL.md
  references/
    custody.md
    isolation.md          # Electron/process/IPC (not WebExtensions)
    consent-signing.md
    connectivity.md
    privacy.md
    findings-severity.md  # same field set + wallet-impact rubric
    report-template.md    # family outline; desktop metadata defaults
```

- **Why:** Matches catalog norms and the extension sibling layout so agents and authors can switch surfaces without relearning structure.
- **Alternatives:** Shared `skills/_wallet-audit-common/` package now (defer physical extraction until a third sibling; copy report outline intentionally).

### D4: Family-standard report (content-only variance)

- **Choice:** Copy the extension report outline verbatim for section headings and finding fields; set Metadata defaults to `skill id: wallet-audit-desktop-eoa` and `surface: desktop/Electron` (or equivalent). Gate Coverage rows MAY use desktop gate names (e.g. “Process / IPC isolation”) under the same section heading.
- **Why:** Spec already requires siblings to keep the same structure; comparability across Frame extension vs Frame desktop audits.
- **Alternatives:** Pointer-only to the extension template file (rejected for catalog packaging independence; duplicate the outline text).

### D5: Companion/extension bridge handling

- **Choice:** In-scope for **desktop-side** trust-boundary findings only; redirect full extension review to `wallet-audit-extension-eoa`.
- **Why:** Symmetric with the extension skill’s companion rule; Frame-shaped products span two surfaces.

### D6: `disable-model-invocation: true`

- **Choice:** Match extension sibling / template default.
- **Why:** High-stakes skill; avoid ambient mis-trigger on generic “wallet” or “Electron” mentions.

### D7: Thin standard pass scope

- **Choice:** Desktop/app hygiene only as it affects wallet risk (auto-update integrity, code signing, dependency supply chain, privileged Electron flags, secrets in repo)—not a full Electron hardening textbook.
- **Why:** Keeps agent runs focused on fund-loss and consent failures.

## Risks / Trade-offs

| Risk | Mitigation |
|------|------------|
| Skill becomes a generic Electron checklist | Lead with specialized wallet gates; standard pass explicitly “thin” and wallet-scored |
| Agents overclaim OS/keychain or hardware verification | Hard non-goals + “limitations / not verified” language; companion redirect |
| Report drift from extension sibling | Spec scenario requires heading/field parity; tasks include side-by-side outline check |
| Duplicate severity/report docs diverge over time | Same field names and severity tiers; consider shared package only after a third sibling |

## Migration Plan

1. Implement skill package under `skills/wallet-audit-desktop-eoa/`.
2. Optionally update extension skill redirect wording from “when available” to the concrete sibling name (cosmetic; no delta to extension requirements required).
3. Archive/sync OpenSpec as usual after apply.
4. Rollback: remove the new skill directory; extension skill redirect remains valid either way.

## Open Questions

- None blocking. Native (non-Electron) desktop wallets can reuse this skill’s gates if process/IPC concepts map; if a large native-only class appears later, revisit naming—not required for v1 Frame/Electron targets.
