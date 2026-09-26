# Consent / signing gate

Focus: the human must authorize what the chain will execute. Decode quality, blind signing, EIP-712 domain binding, and approval UX are the usual failure modes—same bar as extension wallets; UI lives in desktop windows rather than extension popups.

## Checks

### Transaction and message decode

- Confirm UI shows human-meaningful summary (to, value, asset, function, spender) derived from the **same payload** that will be signed—not a parallel “simulation-only” object that can diverge.
- Raw hex / unparsed calldata is labeled as risky; discourage blind confirm.
- Typed data (`eth_signTypedData*`) displays primary type fields and **domain** (name, version, chainId, verifyingContract).

### EIP-712 / domain binding

- Domain `chainId` and `verifyingContract` are shown and checked against the active network / expected contract where applicable.
- Users cannot be tricked into signing a permit or order for the wrong chain or contract via missing domain display.

### Dangerous methods

- Prefer disallowing or strongly warning on legacy `eth_sign` / arbitrary personal_sign of opaque attacker-chosen blobs that can be reused as transactions or authenticators.
- `eth_signTransaction` / send flows must not skip confirm UI for untrusted origins or IPC peers.

### Approvals and permits

- ERC-20 `approve` / `increaseAllowance`, Permit2, EIP-2612 permits: show spender, amount (unlimited vs finite), and token.
- Unlimited approvals are explicitly called out.
- Batch / multi-call payloads still surface each material side effect.

### Simulation vs signature

- If the wallet simulates first: document whether simulation failure blocks signing; flag paths where UI shows a benign sim but signs a different payload.

### Desktop UI ownership

- Confirm / unlock windows are owned by the trusted app surface—not an embeddable webview controlled by a remote origin or companion without the same consent bar.

## Severity hints

Confirm UI can disagree with signed bytes, or an origin/IPC peer can obtain signatures without clear consent → **Critical** / **High**. Poor decode with residual raw display → **Medium** unless paired with auto-approve.
