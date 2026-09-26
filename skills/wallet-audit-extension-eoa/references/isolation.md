# Isolation gate

Focus: WebExtensions trust boundaries (Chromium and Firefox) between web pages, content/inpage scripts, and background / service worker. Provider injection must not let a page read vault secrets or spoof extension UI.

## Architecture to map

```
dApp page  ↔  inpage / content script  ↔  background (SW or page)  ↔  vault / RPC / WC
```

Document message directions, what each layer can access, and where signing happens.

## Checks

### Manifest and permissions (Chromium + Firefox)

- Prefer least privilege: host permissions, `storage`, `clipboardRead`/`Write`, `tabs`, native messaging only if justified.
- Review `externally_connectable` / equivalent: who may message the extension.
- MV3 (Chromium): service worker lifecycle—secrets must not assume long-lived in-memory SW state without re-unlock; alarms/keepalive must not weaken custody.
- Firefox: note `browser.*` vs `chrome.*` shims; background scripts vs MV3 SW if dual-targeted; verify the shipped `manifest.json` for each store build.

### Content script / inpage provider

- Injected `window.ethereum` (or equivalent) is a thin RPC facade; it must not hold seed/keys.
- Page-origin scripts cannot call privileged extension APIs directly.
- Message validation: every privileged request checks sender origin / tab id; reject unexpected senders.
- Prototype pollution / untrusted structured clone of request objects cannot escalate to signing without UI consent.

### UI surfaces

- Popup / notification / side panel that confirms transactions is extension-owned HTML, not page-controlled.
- Phishing: extension pages use extension origins (`chrome-extension://` / `moz-extension://`); deep links into unlock/export flows are gated.

### Native messaging / companion

- If present, treat the native host as untrusted for this skill: validate messages, never send raw seed unless product design explicitly requires it and UX makes that clear. Full companion audit → desktop sibling skill.

## Severity hints

Broken origin binding that allows a page to trigger silent signing or read vault material → **Critical** / **High**. Over-broad host permissions without compensating controls → often **Medium** (elevate if combined with XSS in a privileged page).
