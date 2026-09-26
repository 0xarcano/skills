# Isolation gate (process / IPC)

Focus: desktop/Electron trust boundaries between renderer UI, preload, main process, and any local companions. Less-trusted code must not read vault secrets or spoof confirm UI / signing.

## Architecture to map

```
Renderer UI  ↔  preload (bridge)  ↔  main process  ↔  vault / RPC / WC / OS keychain
                      ↕
              deep links / protocol handlers / local sockets / extension companion
```

Document message directions, what each layer can access, and where signing happens.

## Checks

### Electron process model

- `contextIsolation: true` (or equivalent) for wallet UI windows; `nodeIntegration` disabled in renderers that display dApp content or untrusted HTML.
- Preload exposes a **minimal** API surface; no blanket `require` / Node primitives to the page.
- Remote module / deprecated bridges that punch renderer→main holes are absent or tightly gated.
- WebPreferences reviewed per window type (confirm UI vs embedded browser vs settings).

### IPC validation

- Every privileged IPC channel authenticates sender / frame and validates message shape; reject unexpected channels and oversized/untrusted structured data.
- Signing, unlock, export, and vault-read operations must not be invokable from arbitrary renderer content without going through consent UI owned by the trusted process.
- Prototype pollution / untrusted clone of request objects cannot escalate to signing without user consent.

### Deep links and protocol handlers

- Custom URL schemes / deep links into unlock, export, or signing flows are gated; parameters cannot silently authorize transactions.
- Open-external / navigate handlers do not load untrusted remote UI with main-process privileges.

### Extension / companion bridge

- If present, treat the browser extension (or other companion) as untrusted for this skill: validate messages, never send raw seed unless product design explicitly requires it and UX makes that clear. Full extension audit → `wallet-audit-extension-eoa`.

## Severity hints

Broken process/IPC binding that allows a renderer or companion to trigger silent signing or read vault material → **Critical** / **High**. Over-broad preload APIs without compensating controls → often **Medium** (elevate if combined with XSS in a privileged window).
