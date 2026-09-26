# Privacy gate

Focus: data the wallet emits that can link users, deanonymize addresses, or exfiltrate sensitive material—distinct from custody loss but often adjacent.

## Checks

### Telemetry and analytics

- Inventory analytics SDKs, crash reporters, and feature flags.
- Ensure events do not include seed, private keys, passwords, full addresses if avoidable, signed payloads, or raw WC session secrets.
- Opt-in vs opt-out matches product claims; document defaults in the report.

### RPC and indexer leakage

- Note which account queries hit third-party RPC/indexers (balance, history, simulation).
- Multi-account wallets: whether querying one account reveals the set of user accounts to the provider.

### Fingerprinting via provider

- Injected provider should not expose stable unique hardware/extension install IDs to pages beyond what EIP-1193 requires.
- Version strings and experimental APIs that ease tracking are noted if excessive.

### Local artifacts

- Screenshots of recovery (product guidance), OS-level backups of extension storage, and shared logging—cross-check with [custody.md](custody.md).

### Third-party embeds

- In-extension dApps, iframes, or remote UI that load untrusted origins under extension privilege—treat as high privacy and XSS risk.

## Severity hints

Seed/key or password in telemetry → **Critical**. Address graphs or unnecessary PII to third parties contrary to claims → **Medium** / **High**. Benign anonymized metrics with opt-out → often **Low** / note in Standard Pass.
