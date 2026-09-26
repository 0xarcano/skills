# Connectivity gate

Focus: who the wallet trusts for chain state and sessions—RPC endpoints, chain metadata, and WalletConnect (or similar) origins.

## Checks

### RPC and providers

- Default RPC endpoints are documented; custom RPC addition warns about trust (malicious nodes can lie about balances, receipts, and some sim inputs).
- Secrets (API keys in RPC URLs) are not leaked to dApps, logs, or telemetry.
- Requests that reveal addresses / account activity to RPC are minimized where the product claims privacy (see also [privacy.md](privacy.md)).

### Chain configuration

- `wallet_addEthereumChain` / `wallet_switchEthereumChain` (and equivalents): UI shows chainId, RPC URL, explorers; block obvious spoofing (e.g. chainId mismatch with displayed name) where detectable.
- Active chain used for signing matches what the confirm UI displays.

### WalletConnect / session protocols

- Pairing and session proposals show dApp name, URL/origin, and requested methods/chains before approve.
- Session misuse: methods that sign or send require the same consent bar as inpage provider calls.
- Session storage: disconnect revokes; stale sessions do not silently retain signing capability after user intent to revoke.

### Network errors and failover

- Failover RPC lists cannot be silently rewritten by untrusted pages.
- MITM on extension update / config channels is out of band but note if remote config can rewrite RPC or chain lists without integrity checks.

## Severity hints

Untrusted party can point signing at wrong chain or keep a WC session that signs without re-consent → **High** / **Critical**. Merely using a third-party RPC by default → often informational / **Low** unless keys leak via URL or logs.
