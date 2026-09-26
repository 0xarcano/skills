# Findings and severity

Use these fields and tiers in every finding under the [report template](report-template.md). Sibling `wallet-audit-*` skills must keep the same field set.

## Required finding fields

| Field | Meaning |
|-------|---------|
| **ID** | Stable short id (e.g. `EXT-CUS-01`) |
| **Title** | One-line summary |
| **Asset** | Component (vault, inpage, confirm UI, WC, RPC config, …) |
| **Evidence** | Path, manifest key, code location, or config reference |
| **Severity** | Critical / High / Medium / Low / Informational |
| **Wallet impact** | Effect on keys, funds, or user consent |
| **Description** | What is wrong and how it manifests |
| **Remediation** | Concrete fix direction |

## Severity rubric (wallet-impact biased)

| Severity | Typical wallet impact |
|----------|------------------------|
| **Critical** | Seed/private key exposure to a less-trusted context; silent or forged signing; broken origin/consent binding that moves funds or grants unbounded approvals without informed user action |
| **High** | Practical path to unauthorized signing, vault unlock bypass, or malicious chain/session control with realistic user interaction |
| **Medium** | Meaningful weakness requiring additional conditions (XSS in semi-privileged page, confusing decode, over-broad permissions) |
| **Low** | Hardening gap, defense-in-depth, limited exploitability |
| **Informational** | Notes, residual risk, design observations without a clear exploit path |

Elevate when multiple medium issues chain into custody or consent failure. Do not inflate generic web findings unless they touch keys, signing, or consent.
