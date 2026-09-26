---
name: wallet-audit-extension-eoa
description: >-
  Audits non-custodial browser-extension EOA/HD wallets (MetaMask-class, Rabby,
  Frame extension, Chromium or Firefox WebExtensions) using specialized custody,
  isolation, signing-consent, connectivity, and privacy gates plus a thin
  standard security/privacy pass. Emits the family-standard markdown Wallet Audit
  Report. Use when the user asks to security- or privacy-audit an authorized
  browser extension wallet, injected window.ethereum provider vault, or similar
  extension package—not desktop/Electron, mobile, hardware, AA/MPC, or custodial apps.
license: MIT
disable-model-invocation: true
metadata:
  author: arcano
---

# Wallet audit — extension EOA

Authorized security and privacy review of **non-custodial browser-extension EOA/HD wallets**. Do not build exploit kits, phishing campaigns, or unauthorized attack procedures.

## Scope

**In scope:** Chromium or Firefox WebExtension packages that hold an HD/EOA vault and inject a provider (MetaMask-class, Rabby, Frame **extension**, etc.).

**Out of scope (redirect):**

| Target | Action |
|--------|--------|
| Desktop / Electron (e.g. Frame **app**) | Use sibling `wallet-audit-desktop-eoa`; do not audit under this skill |
| Mobile, hardware, AA/MPC, custodial, chain/protocol-only | Out of scope; say so and stop or use another skill |

**Companion / native bridge:** If the extension talks to a desktop companion, treat the companion as an **untrusted peer**. Record extension-side trust-boundary findings only. Do **not** claim desktop or hardware verification.

## Instructions

1. **Classify and authorize** — Confirm the artifact is an in-scope extension under authorized review. If out of scope, redirect per the table above. If the user asks for exploits or unauthorized attacks, refuse and stay on audit/review guidance.

2. **Specialized gates** (mandatory; read each reference as you go):
   - [Custody](references/custody.md) — seed/vault/export/clipboard
   - [Isolation](references/isolation.md) — WebExtensions, provider injection
   - [Consent / signing](references/consent-signing.md) — decode, blind sign, EIP-712, approvals
   - [Connectivity](references/connectivity.md) — RPC, chain config, WalletConnect
   - [Privacy](references/privacy.md) — telemetry, RPC leakage, fingerprinting

3. **Thin standard pass** — Extension/app hygiene only as it affects wallet risk (permissions sprawl, update integrity, dependency supply chain, CSP, secrets in repo). Do not reprint ASVS. Score findings with [findings-severity](references/findings-severity.md).

4. **Report** — Emit results **only** as the markdown document in [report-template.md](references/report-template.md). Keep section headings and finding fields identical. Sibling `wallet-audit-*` skills must reuse this structure and change content only.

## Examples

**In-scope:** User asks to audit the Rabby (or Frame extension) source/package under authorization → run the hybrid workflow → produce `# Wallet Audit Report` per the template.

**Out-of-scope desktop:** User asks to audit Frame **desktop** → state this skill covers the extension surface only; point to `wallet-audit-desktop-eoa`; do not pretend to complete a desktop audit here.

## Additional resources

- [references/custody.md](references/custody.md)
- [references/isolation.md](references/isolation.md)
- [references/consent-signing.md](references/consent-signing.md)
- [references/connectivity.md](references/connectivity.md)
- [references/privacy.md](references/privacy.md)
- [references/findings-severity.md](references/findings-severity.md)
- [references/report-template.md](references/report-template.md)
