## Purpose

Guides AI agents through authorized security and privacy audits of non-custodial browser-extension EOA/HD wallets, combining thin standard app review with MetaMask-class specialized gates and a family-standard markdown wallet audit report.

## ADDED Requirements

### Requirement: Skill package location and identity
The catalog SHALL publish the skill at `skills/wallet-audit-extension-eoa/` with frontmatter `name` matching the folder name, following the repository skill template conventions.

#### Scenario: Skill is discoverable in the catalog
- **WHEN** an agent or user looks up catalog skills under `skills/`
- **THEN** `skills/wallet-audit-extension-eoa/SKILL.md` exists and its frontmatter `name` is `wallet-audit-extension-eoa`

### Requirement: Description triggers for MetaMask-class extensions
The skill description SHALL be written in third person, state WHAT the skill does and WHEN to use it, and include trigger terms for non-custodial browser-extension EOA wallets (including MetaMask-class, Rabby-class, Frame extension, and Firefox WebExtension builds of the same class).

#### Scenario: Description matches authorized extension-wallet audit request
- **WHEN** a user asks to audit a non-custodial browser-extension EOA wallet such as Rabby or a Frame extension
- **THEN** the skill description is specific enough that an agent can select this skill rather than a desktop, mobile, hardware, AA, or custodial audit skill

### Requirement: Scoped hybrid audit workflow
The skill instructions SHALL require the agent to: (1) confirm the target is an in-scope non-custodial browser-extension EOA/HD wallet under authorized review, (2) refuse or redirect out-of-scope targets (desktop/Electron primary surface, mobile, hardware, AA/MPC, custodial, chain/protocol-only), (3) run specialized wallet gates for custody, isolation, consent/signing, connectivity, and privacy, (4) apply a thin standard security/privacy pass without reprinting general ASVS textbooks, and (5) produce the standard markdown wallet audit report.

#### Scenario: In-scope extension audit
- **WHEN** the agent is asked to audit an authorized browser-extension EOA wallet codebase or package
- **THEN** the agent follows the hybrid workflow (classify → specialized gates → standard pass → standard markdown report)

#### Scenario: Out-of-scope desktop wallet
- **WHEN** the primary target is a desktop/Electron wallet (e.g. Frame desktop app) rather than a browser extension
- **THEN** the skill instructs the agent to treat that target as out of scope for this skill and point to a separate desktop wallet-audit skill when available

#### Scenario: Companion bridge noted but not fully verified
- **WHEN** an in-scope extension communicates with a native/desktop companion
- **THEN** the skill instructs the agent to treat the companion as an untrusted peer trust boundary for extension-side findings and NOT claim full desktop or hardware verification under this skill

### Requirement: Progressive disclosure of specialized references
Long specialized check material SHALL live under `references/` linked one level deep from `SKILL.md`, covering at least custody/vault, extension isolation/provider injection, signing consent (including blind signing and EIP-712 domain binding), RPC/WalletConnect connectivity, privacy/telemetry, findings/severity rubric, and the canonical markdown report template.

#### Scenario: Agent needs deep signing guidance
- **WHEN** the agent reaches the consent/signing gate during an audit
- **THEN** `SKILL.md` points to a one-level-deep reference file with specialized signing checks rather than embedding the full checklist in `SKILL.md`

### Requirement: Standard markdown wallet audit report
The skill SHALL provide a canonical markdown report template and SHALL require agents to emit audit results in that structure. The report MUST include these top-level sections in order:

1. **Title** — `# Wallet Audit Report`
2. **Metadata** — target name, version/commit, skill id, surface, custody model, audit date, authorization/scope statement
3. **Executive Summary** — short overall risk posture and finding counts by severity
4. **Scope and Method** — in scope, out of scope, gates performed, limitations / not verified
5. **Findings Summary** — table with columns: ID, Title, Severity, Wallet impact, Gate
6. **Findings** — one subsection per finding with fields: Severity, ID, Title, Asset, Evidence, Wallet impact, Description, Remediation
7. **Gate Coverage** — status/notes per specialized gate (gate *names* may differ by skill; the section heading MUST remain)
8. **Standard Security and Privacy Pass** — brief notes or finding cross-references from the thin standard pass
9. **Residual Risks and Recommendations** — open risks and prioritized next steps
10. **Appendix** (optional) — supporting detail

Each finding SHALL include at least: id, title, asset, evidence, severity, wallet_impact, description, and remediation. Severity guidance SHALL elevate issues that expose seed/keys, enable unauthorized signing, or break origin/consent binding.

#### Scenario: Critical custody finding
- **WHEN** the agent discovers plaintext seed or private key material in logs, storage, or export paths accessible to a less-trusted context
- **THEN** the skill’s severity rubric classifies the issue at the highest severity tier with explicit wallet impact on key custody, and the finding appears under **Findings** using the required fields

#### Scenario: Report uses the standard outline
- **WHEN** the agent completes an audit using this skill
- **THEN** the output is a markdown document that includes the required section headings in order (not only freeform prose or an alternate schema such as YAML-only findings)

### Requirement: Family-standard report for sibling wallet-audit skills
The markdown report structure defined by this skill SHALL be the standard for related `wallet-audit-*` catalog skills. Sibling skills MUST keep the same section headings and finding field set; they MAY change only the filled-in content (target metadata, gate names/notes inside Gate Coverage, finding bodies, and skill-specific scope language).

#### Scenario: Future desktop skill reuses report outline
- **WHEN** a sibling skill such as `wallet-audit-desktop-eoa` is authored
- **THEN** it MUST instruct agents to emit the same markdown report section structure and finding fields, varying only content appropriate to that surface

### Requirement: Defensive authorized-use framing
The skill SHALL frame its use as authorized security review of a wallet under test and MUST NOT instruct agents to build exploit kits, phishing campaigns, or unauthorized attack procedures against third-party wallets.

#### Scenario: User requests offensive tooling
- **WHEN** a user asks for exploit payloads or unauthorized attack procedures against a wallet
- **THEN** the skill’s framing directs the agent to refuse that use and stay within authorized audit/review guidance
