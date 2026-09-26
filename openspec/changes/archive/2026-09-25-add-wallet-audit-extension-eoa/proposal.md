## Why

AI agents auditing web3 wallets lack a focused, reusable playbook that combines standard app security/privacy review with MetaMask-class extension hazards (vault custody, provider isolation, signing consent, RPC/WC trust). Without a scoped catalog skill, audits drift into protocol, hardware, or custodial territory—or stay generic and miss wallet-specific fund-loss paths. Related wallet-audit skills also need one shared report shape so results stay comparable across surfaces (extension, desktop, etc.).

## What Changes

- Add a new catalog skill `wallet-audit-extension-eoa` under `skills/` for authorized audits of **non-custodial browser-extension EOA/HD wallets** (e.g. Rabby, MetaMask-class, Frame **extension**; Chromium and Firefox WebExtensions).
- Skill content: workflow instructions in `SKILL.md`, plus progressive-disclosure references for specialized gates (custody, isolation, consent, connectivity, privacy), severity rubric, and a **canonical markdown audit report template**.
- Establish that **all related `wallet-audit-*` skills** MUST emit results using this same markdown report structure (same section headings and finding fields); only target-specific content, gate lists, and findings text may change.
- Explicit non-goals in the skill: desktop/Electron wallets (sibling skill later), mobile, hardware, AA/MPC, custodial apps, chain/protocol contract audits.
- No changes to OpenSpec tooling, templates layout conventions, or existing skills.

## Capabilities

### New Capabilities

- `wallet-audit-extension-eoa`: Catalog skill that guides agents through a hybrid audit of non-custodial browser-extension EOA wallets—classify target, run specialized wallet gates, apply a thin standard security/privacy pass, and emit a **standard markdown wallet audit report** with wallet-impact severity. The report outline defined here is the family standard for future sibling wallet-audit skills.

### Modified Capabilities

- (none)

## Impact

- New path: `skills/wallet-audit-extension-eoa/` (`SKILL.md`, `references/` including `report-template.md`).
- Follows repo skill-authoring conventions (`templates/skill/`, third-person description, progressive disclosure).
- Consumers: agents auditing extension wallet source/packages under authorization (e.g. Rabby, Frame extension, Firefox builds of the same class).
- Deferred siblings (out of this change): `wallet-audit-desktop-eoa`, mobile, AA, MPC, hardware — each MUST reuse the same report markdown structure when added.
