---
name: wallet-audit-desktop-eoa
description: >-
  Audits non-custodial desktop/Electron EOA/HD wallets (Frame desktop/app,
  Electron wallet clients, similar native desktop EOA surfaces) using specialized
  custody, process/IPC isolation, signing-consent, connectivity, and privacy
  gates plus a thin standard security/privacy pass. Emits the family-standard
  markdown Wallet Audit Report. Use when the user asks to security- or
  privacy-audit an authorized desktop or Electron wallet app—not browser
  extensions, mobile, hardware, AA/MPC, or custodial apps.
license: MIT
disable-model-invocation: true
metadata:
  author: arcano
---

# Wallet audit — desktop EOA

Authorized security and privacy review of **non-custodial desktop/Electron EOA/HD wallets**. Do not build exploit kits, phishing campaigns, or unauthorized attack procedures.

## Scope

**In scope:** Desktop or Electron packages that hold an HD/EOA vault (Frame **app**, similar Electron wallet clients, comparable native desktop EOA surfaces).

**Out of scope (redirect):**

| Target | Action |
|--------|--------|
| Browser extension (e.g. Rabby, Frame **extension**) | Use sibling `wallet-audit-extension-eoa`; do not audit under this skill |
| Mobile, hardware, AA/MPC, custodial, chain/protocol-only | Out of scope; say so and stop or use another skill |

**Extension / companion bridge:** If the desktop app talks to a browser-extension companion or injected provider bridge, treat the extension as an **untrusted peer**. Record desktop-side trust-boundary findings only. Do **not** claim full extension verification.

## Instructions

1. **Classify and authorize** — Confirm the artifact is an in-scope desktop/Electron wallet under authorized review. If out of scope, redirect per the table above. If the user asks for exploits or unauthorized attacks, refuse and stay on audit/review guidance.

2. **Specialized gates** (mandatory; read each reference as you go):
   - [Custody](references/custody.md) — on-disk vault, OS keychain, export, clipboard, IPC/memory leaks
   - [Isolation](references/isolation.md) — Electron main/renderer/preload, IPC, deep links
   - [Consent / signing](references/consent-signing.md) — decode, blind sign, EIP-712, approvals
   - [Connectivity](references/connectivity.md) — RPC, chain config, WalletConnect, local bridges
   - [Privacy](references/privacy.md) — telemetry, crash reporter, auto-update, RPC leakage

3. **Thin standard pass** — Desktop/app hygiene only as it affects wallet risk (auto-update integrity, code signing, dependency supply chain, privileged Electron flags, secrets in repo). Do not reprint ASVS or a full Electron hardening textbook. Score findings with [findings-severity](references/findings-severity.md).

4. **Report** — Emit results **only** as the markdown document in [report-template.md](references/report-template.md). Keep section headings and finding fields identical to the family standard. Sibling `wallet-audit-*` skills must reuse this structure and change content only.

## Examples

**In-scope:** User asks to audit the Frame **desktop** (or similar Electron EOA wallet) source/package under authorization → run the hybrid workflow → produce `# Wallet Audit Report` per the template.

**Out-of-scope extension:** User asks to audit Rabby or Frame **extension** → state this skill covers the desktop surface only; point to `wallet-audit-extension-eoa`; do not pretend to complete an extension audit here.

## Additional resources

- [references/custody.md](references/custody.md)
- [references/isolation.md](references/isolation.md)
- [references/consent-signing.md](references/consent-signing.md)
- [references/connectivity.md](references/connectivity.md)
- [references/privacy.md](references/privacy.md)
- [references/findings-severity.md](references/findings-severity.md)
- [references/report-template.md](references/report-template.md)
