# Custody gate

Focus: how seed phrases, private keys, and encrypted vaults are generated, stored, unlocked, exported, and cleared on a **desktop/Electron** surface. Highest severity when secrets reach a less-trusted context (renderer, IPC peer, world-readable disk, logs).

## Checks

### Generation and entropy

- Mnemonic / key generation uses a CSPRNG; no weak `Math.random`, predictable timestamps, or user-supplied entropy without clear warnings.
- Derivation paths (BIP-32/39/44 or project equivalent) are intentional; surprising default paths are documented.

### Vault at rest

- Seed/private keys are encrypted at rest on disk (app data dir, user profile paths)—not plaintext JSON/files.
- Prefer OS keychain / keystore / DPAPI (or equivalent) for wrapping keys where the product claims it; document what actually protects the vault key.
- Encryption keys derive from user secret (password / OS unlock) with a modern KDF; plaintext vault password or raw seed must not persist unlocked longer than the unlock session requires.
- Unlocked vault state is not written to world-readable locations, shared sync folders, or crash dumps without encryption.

### Export and recovery UX

- Export seed / private key requires explicit, hard-to-misfire confirmation and re-auth.
- Recovery screens warn against screenshots; prefer reveal-on-hold / segmented display where feasible.
- Clipboard writes of seed/key are minimized, time-bounded, and cleared when possible; logging must never include seed/key material.

### Leak surfaces (desktop-specific)

- Search logs, analytics, crash reporters, auto-update diagnostics, and debug flags for mnemonic, private key, or vault plaintext.
- Renderer / preload processes and untrusted IPC peers must not receive raw seed/keys.
- Memory: note if secrets are held longer than needed in renderer-accessible memory or passed through IPC channels that less-trusted code can observe.
- Backup / sync / cloud features (if any) keep the same encryption bar as local vault.

## Severity hints

See [findings-severity.md](findings-severity.md). Plaintext seed/key in a less-trusted context → **Critical**.
