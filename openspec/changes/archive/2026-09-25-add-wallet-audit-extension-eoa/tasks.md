## 1. Scaffold skill package

- [x] 1.1 Copy `templates/skill` to `skills/wallet-audit-extension-eoa/`
- [x] 1.2 Set frontmatter `name: wallet-audit-extension-eoa`, keep `disable-model-invocation: true`, and write third-person WHAT/WHEN description with MetaMask-class / Rabby / Frame extension / Firefox WebExtension trigger terms
- [x] 1.3 Create `references/` directory for progressive-disclosure files

## 2. SKILL.md workflow and scope

- [x] 2.1 Write Instructions for hybrid flow: classify/authorize → specialized gates → thin standard pass → standard markdown report
- [x] 2.2 Document in-scope vs out-of-scope (desktop sibling, mobile, hardware, AA/MPC, custodial, protocol-only) and companion-bridge trust-boundary rules
- [x] 2.3 Add authorized-review framing (no exploit kits / unauthorized attack procedures)
- [x] 2.4 Require output to follow `references/report-template.md` and note that sibling `wallet-audit-*` skills must keep the same report structure
- [x] 2.5 Add Examples for in-scope extension audit and out-of-scope desktop redirect
- [x] 2.6 Link all `references/*.md` files one level deep from Additional resources

## 3. Specialized reference gates

- [x] 3.1 Write `references/custody.md` (seed/vault/export/clipboard/screenshot risks)
- [x] 3.2 Write `references/isolation.md` (WebExtensions for Chromium + Firefox; MV3 service worker / permissions where distinct; content script / background / inpage provider isolation)
- [x] 3.3 Write `references/consent-signing.md` (decode UX, blind signing, EIP-712 domain binding, approvals)
- [x] 3.4 Write `references/connectivity.md` (RPC trust, chain config spoofing, WalletConnect origin/session)
- [x] 3.5 Write `references/privacy.md` (telemetry, RPC query leakage, fingerprinting via provider)

## 4. Report standard, severity, and polish

- [x] 4.1 Write `references/report-template.md` with the canonical markdown outline (Metadata through Appendix) and placeholder finding subsection fields
- [x] 4.2 Write `references/findings-severity.md` with required finding fields and wallet-impact severity rubric aligned to the report template
- [x] 4.3 Document in SKILL.md / report template that future `wallet-audit-*` skills reuse this structure and change content only
- [x] 4.4 Sanity-check skill against authoring checklist (path/name match, description WHAT+WHEN, concise SKILL.md, one-level links, not under `.cursor/skills/`)
