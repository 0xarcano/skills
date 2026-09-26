# Connectivity gate

Focus: who the wallet trusts for chain state and sessions—RPC endpoints, chain metadata, WalletConnect (or similar) origins, and **local** bridges to extension companions.

## Checks

### RPC and providers

- Default RPC endpoints are documented; custom RPC addition warns about trust (malicious nodes can lie about balances, receipts, and some sim inputs).
- Secrets (API keys in RPC URLs) are not leaked to dApps, logs, telemetry, or companion processes.
- Requests that reveal addresses / account activity to RPC are minimized where the product claims privacy (see also [privacy.md](privacy.md)).

### Chain configuration

- Add/switch chain flows (EIP-3085/3326 analogues or app settings): UI shows chainId, RPC URL, explorers; block obvious spoofing (e.g. chainId mismatch with displayed name) where detectable.
- Active chain used for signing matches what the confirm UI displays.

### WalletConnect / session protocols

- Pairing and session proposals show dApp name, URL/origin, and requested methods/chains before approve.
- Session misuse: methods that sign or send require the same consent bar as in-app provider calls.
- Session storage: disconnect revokes; stale sessions do not silently retain signing capability after user intent to revoke.

### Local IPC / socket bridges

- Local listeners (Unix sockets, named pipes, loopback HTTP, native messaging to an extension) authenticate peers and validate payloads.
- Companion bridges cannot rewrite RPC/chain lists or approve sessions without the desktop consent bar.
- Treat extension companions as untrusted peers; full extension review → `wallet-audit-extension-eoa`.

### Network errors and failover

- Failover RPC lists cannot be silently rewritten by untrusted pages or companions.
- Remote config / auto-update channels that can rewrite RPC or chain lists need integrity checks (see thin standard pass for update signing).

## Severity hints

Untrusted party can point signing at wrong chain or keep a WC/local session that signs without re-consent → **High** / **Critical**. Merely using a third-party RPC by default → often informational / **Low** unless keys leak via URL or logs.
