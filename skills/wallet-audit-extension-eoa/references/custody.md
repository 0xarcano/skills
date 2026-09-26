# Custody gate

Focus: how seed phrases, private keys, and encrypted vaults are generated, stored, unlocked, exported, and cleared. Highest severity when secrets reach a less-trusted context.

## Checks

### Generation and entropy

- Mnemonic / key generation uses a CSPRNG; no weak `Math.random`, predictable timestamps, or user-supplied entropy without clear warnings.
- Derivation paths (BIP-32/39/44 or project equivalent) are intentional; surprising default paths are documented.

### Vault at rest

- Seed/private keys are encrypted at rest (extension storage / IndexedDB / local files under the extension identity).
- Encryption keys derive from user secret (password / passkey) with a modern KDF; plaintext vault password or raw seed must not persist unlocked longer than the unlock session requires.
- Unlocked vault state is not written to world-readable locations or synced stores without encryption.

### Export and recovery UX

- Export seed / private key requires explicit, hard-to-misfire confirmation and re-auth.
- Recovery screens warn against screenshots; prefer reveal-on-hold / segmented display where feasible.
- Clipboard writes of seed/key are minimized, time-bounded, and cleared when possible; logging must never include seed/key material.

### Leak surfaces

- Search logs, analytics, crash reports, error reporters, and debug flags for mnemonic, private key, or vault plaintext.
- Content scripts and inpage scripts must not receive raw seed/keys.
- Backup / sync features (if any) keep the same encryption bar as local vault.

## Severity hints

See [findings-severity.md](findings-severity.md). Plaintext seed/key in a less-trusted context → **Critical**.
