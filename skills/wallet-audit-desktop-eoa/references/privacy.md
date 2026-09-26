# Privacy gate

Focus: data the wallet emits that can link users, deanonymize addresses, or exfiltrate sensitive material—distinct from custody loss but often adjacent. Desktop adds crash reporters and auto-update channels.

## Checks

### Telemetry and analytics

- Inventory analytics SDKs, crash reporters, and feature flags.
- Ensure events do not include seed, private keys, passwords, full addresses if avoidable, signed payloads, or raw WC session secrets.
- Opt-in vs opt-out matches product claims; document defaults in the report.

### Crash reporter and auto-update

- Crash dumps / minidumps must not include vault plaintext, seed, or unlock secrets.
- Auto-update / sparkle / electron-updater diagnostics and error reports scrub secrets; update metadata channels are integrity-protected (cross-check thin standard pass).

### RPC and indexer leakage

- Note which account queries hit third-party RPC/indexers (balance, history, simulation).
- Multi-account wallets: whether querying one account reveals the set of user accounts to the provider.

### Fingerprinting

- Provider / local API surfaces should not expose stable unique install IDs to untrusted peers beyond what the product protocol requires.
- Version strings and experimental APIs that ease tracking are noted if excessive.

### Local artifacts

- Screenshots of recovery (product guidance), OS-level backups of app data, Time Machine / cloud sync of vault paths—cross-check with [custody.md](custody.md).

### Third-party embeds

- In-app browsers, iframes, or remote UI that load untrusted origins under elevated privilege—treat as high privacy and XSS risk (cross-check [isolation.md](isolation.md)).

## Severity hints

Seed/key or password in telemetry or crash dumps → **Critical**. Address graphs or unnecessary PII to third parties contrary to claims → **Medium** / **High**. Benign anonymized metrics with opt-out → often **Low** / note in Standard Pass.
