## Why

The extension EOA skill (`wallet-audit-extension-eoa`) intentionally redirects Frame-class **desktop/Electron** targets to a sibling skill that does not yet exist. Agents auditing non-custodial desktop wallets need the same hybrid playbook and **family-standard markdown report**, but with gates tuned to Electron process boundaries, IPC, OS key material storage, and deep-link surfaces—not WebExtensions/`window.ethereum` injection.

## What Changes

- Add catalog skill `wallet-audit-desktop-eoa` under `skills/` for authorized audits of **non-custodial desktop/Electron EOA/HD wallets** (e.g. Frame **app**, similar Electron wallet clients).
- Skill content: workflow in `SKILL.md`, progressive-disclosure references for desktop-adapted specialized gates (custody, process/IPC isolation, consent/signing, connectivity, privacy), severity rubric, and the **same canonical markdown report outline** as the extension sibling (content-only variance).
- Explicit non-goals: browser-extension primary surface (use `wallet-audit-extension-eoa`), mobile, hardware, AA/MPC, custodial apps, chain/protocol-only audits.
- Optionally tighten the extension skill’s out-of-scope redirect text to name this sibling as available (no requirement change beyond cross-link polish).
- No changes to OpenSpec tooling or skill-authoring template layout conventions.

## Capabilities

### New Capabilities

- `wallet-audit-desktop-eoa`: Catalog skill that guides agents through a hybrid audit of non-custodial desktop/Electron EOA wallets—classify target, run specialized desktop gates, apply a thin standard security/privacy pass, and emit the **family-standard markdown Wallet Audit Report** with wallet-impact severity.

### Modified Capabilities

- (none)

## Impact

- New path: `skills/wallet-audit-desktop-eoa/` (`SKILL.md`, `references/` including a report template that mirrors the family outline with desktop metadata defaults).
- Reuses the report contract already established by `wallet-audit-extension-eoa` / `openspec/specs/wallet-audit-extension-eoa`.
- Consumers: agents auditing authorized desktop wallet source/packages (e.g. Frame desktop app, Electron EOA clients).
- Deferred siblings remain: mobile, AA, MPC, hardware.
