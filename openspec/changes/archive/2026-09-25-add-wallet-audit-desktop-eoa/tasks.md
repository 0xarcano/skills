## 1. Scaffold skill package

- [x] 1.1 Copy `templates/skill` to `skills/wallet-audit-desktop-eoa/`
- [x] 1.2 Set frontmatter `name: wallet-audit-desktop-eoa`, keep `disable-model-invocation: true`, and write third-person WHAT/WHEN description with Frame desktop / Electron EOA trigger terms
- [x] 1.3 Create `references/` directory for progressive-disclosure files

## 2. SKILL.md workflow and scope

- [x] 2.1 Write Instructions for hybrid flow: classify/authorize → specialized gates → thin standard pass → family-standard markdown report
- [x] 2.2 Document in-scope vs out-of-scope (extension sibling `wallet-audit-extension-eoa`, mobile, hardware, AA/MPC, custodial, protocol-only) and extension-companion trust-boundary rules
- [x] 2.3 Add authorized-review framing (no exploit kits / unauthorized attack procedures)
- [x] 2.4 Require output to follow `references/report-template.md` with the same headings/fields as the extension family standard (content-only variance)
- [x] 2.5 Add Examples for in-scope desktop audit and out-of-scope extension redirect
- [x] 2.6 Link all `references/*.md` files one level deep from Additional resources

## 3. Specialized reference gates

- [x] 3.1 Write `references/custody.md` (on-disk vault, OS keychain/keystore, export, clipboard, IPC/memory leak surfaces)
- [x] 3.2 Write `references/isolation.md` (Electron main/renderer/preload, contextIsolation, nodeIntegration, IPC validation, deep links / protocol handlers)
- [x] 3.3 Write `references/consent-signing.md` (decode UX vs payload, blind signing, EIP-712 domain binding, approvals)
- [x] 3.4 Write `references/connectivity.md` (RPC trust, chain config spoofing, WalletConnect, local IPC/socket bridges to extension companions)
- [x] 3.5 Write `references/privacy.md` (telemetry, crash reporter, auto-update, RPC query leakage, fingerprinting)

## 4. Report standard, severity, polish, sibling link

- [x] 4.1 Write `references/report-template.md` with the family markdown outline (Metadata through Appendix), desktop metadata defaults, and matching finding subsection fields
- [x] 4.2 Write `references/findings-severity.md` with required finding fields and wallet-impact severity rubric aligned to the family report
- [x] 4.3 Side-by-side check that report section headings and finding fields match `skills/wallet-audit-extension-eoa/references/report-template.md`
- [x] 4.4 Optionally update extension skill redirect text to name `wallet-audit-desktop-eoa` as available
- [x] 4.5 Sanity-check skill against authoring checklist (path/name match, description WHAT+WHEN, concise SKILL.md, one-level links, not under `.cursor/skills/`)
