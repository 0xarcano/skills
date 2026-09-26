# wallet-audit-desktop-eoa Specification

## Purpose

Guides AI agents through authorized security and privacy audits of non-custodial desktop/Electron EOA/HD wallets, combining thin standard app review with desktop-specialized custody, process/IPC isolation, signing-consent, connectivity, and privacy gates, and emitting the family-standard markdown Wallet Audit Report.

## Requirements

### Requirement: Skill package location and identity
The catalog SHALL publish the skill at `skills/wallet-audit-desktop-eoa/` with frontmatter `name` matching the folder name, following the repository skill template conventions.

#### Scenario: Skill is discoverable in the catalog
- **WHEN** an agent or user looks up catalog skills under `skills/`
- **THEN** `skills/wallet-audit-desktop-eoa/SKILL.md` exists and its frontmatter `name` is `wallet-audit-desktop-eoa`

### Requirement: Description triggers for desktop/Electron EOA wallets
The skill description SHALL be written in third person, state WHAT the skill does and WHEN to use it, and include trigger terms for non-custodial desktop/Electron EOA wallets (including Frame desktop/app, Electron wallet clients, and similar native desktop EOA/HD surfaces).

#### Scenario: Description matches authorized desktop-wallet audit request
- **WHEN** a user asks to audit a non-custodial desktop/Electron EOA wallet such as the Frame desktop app
- **THEN** the skill description is specific enough that an agent can select this skill rather than an extension, mobile, hardware, AA, or custodial audit skill

### Requirement: Scoped hybrid audit workflow
The skill instructions SHALL require the agent to: (1) confirm the target is an in-scope non-custodial desktop/Electron EOA/HD wallet under authorized review, (2) refuse or redirect out-of-scope targets (browser-extension primary surface, mobile, hardware, AA/MPC, custodial, chain/protocol-only), (3) run specialized wallet gates for custody, process/IPC isolation, consent/signing, connectivity, and privacy, (4) apply a thin standard security/privacy pass without reprinting general ASVS textbooks, and (5) produce the family-standard markdown wallet audit report.

#### Scenario: In-scope desktop audit
- **WHEN** the agent is asked to audit an authorized desktop/Electron EOA wallet codebase or package
- **THEN** the agent follows the hybrid workflow (classify → specialized gates → standard pass → standard markdown report)

#### Scenario: Out-of-scope browser extension
- **WHEN** the primary target is a browser-extension wallet (e.g. Rabby or Frame extension) rather than a desktop app
- **THEN** the skill instructs the agent to treat that target as out of scope for this skill and point to `wallet-audit-extension-eoa`

#### Scenario: Extension companion noted but not fully verified
- **WHEN** an in-scope desktop wallet communicates with a browser-extension companion or injected provider bridge
- **THEN** the skill instructs the agent to treat the extension as an untrusted peer trust boundary for desktop-side findings and NOT claim full extension verification under this skill

### Requirement: Progressive disclosure of specialized references
Long specialized check material SHALL live under `references/` linked one level deep from `SKILL.md`, covering at least custody/vault (including OS/keychain and on-disk secrets), process/IPC isolation (Electron main/renderer, preload, contextIsolation, deep links), signing consent (including blind signing and EIP-712 domain binding), RPC/WalletConnect connectivity, privacy/telemetry, findings/severity rubric, and the family-standard markdown report template.

#### Scenario: Agent needs deep isolation guidance
- **WHEN** the agent reaches the process/IPC isolation gate during an audit
- **THEN** `SKILL.md` points to a one-level-deep reference file with specialized Electron/desktop isolation checks rather than embedding the full checklist in `SKILL.md`

### Requirement: Family-standard markdown wallet audit report
The skill SHALL provide a markdown report template and SHALL require agents to emit audit results using the **same section headings and finding field set** as the family standard established by `wallet-audit-extension-eoa`. The report MUST include these top-level sections in order:

1. **Title** — `# Wallet Audit Report`
2. **Metadata** — target name, version/commit, skill id, surface, custody model, audit date, authorization/scope statement
3. **Executive Summary** — short overall risk posture and finding counts by severity
4. **Scope and Method** — in scope, out of scope, gates performed, limitations / not verified
5. **Findings Summary** — table with columns: ID, Title, Severity, Wallet impact, Gate
6. **Findings** — one subsection per finding with fields: Severity, ID, Title, Asset, Evidence, Wallet impact, Description, Remediation
7. **Gate Coverage** — status/notes per specialized gate (gate *names* MAY reflect the desktop surface; the section heading MUST remain)
8. **Standard Security and Privacy Pass** — brief notes or finding cross-references from the thin standard pass
9. **Residual Risks and Recommendations** — open risks and prioritized next steps
10. **Appendix** (optional) — supporting detail

Each finding SHALL include at least: id, title, asset, evidence, severity, wallet_impact, description, and remediation. Severity guidance SHALL elevate issues that expose seed/keys, enable unauthorized signing, or break origin/consent binding.

#### Scenario: Critical custody finding
- **WHEN** the agent discovers plaintext seed or private key material in logs, on-disk storage, IPC payloads, or export paths accessible to a less-trusted context
- **THEN** the skill’s severity rubric classifies the issue at the highest severity tier with explicit wallet impact on key custody, and the finding appears under **Findings** using the required fields

#### Scenario: Report uses the family-standard outline
- **WHEN** the agent completes an audit using this skill
- **THEN** the output is a markdown document that includes the required section headings in order (not only freeform prose or an alternate schema such as YAML-only findings)

#### Scenario: Report differs from extension skill only in content
- **WHEN** comparing this skill’s report template to `wallet-audit-extension-eoa`
- **THEN** section headings and finding fields match; only defaults such as skill id, surface metadata, and gate coverage row names may differ

### Requirement: Defensive authorized-use framing
The skill SHALL frame its use as authorized security review of a wallet under test and MUST NOT instruct agents to build exploit kits, phishing campaigns, or unauthorized attack procedures against third-party wallets.

#### Scenario: User requests offensive tooling
- **WHEN** a user asks for exploit payloads or unauthorized attack procedures against a wallet
- **THEN** the skill’s framing directs the agent to refuse that use and stay within authorized audit/review guidance
