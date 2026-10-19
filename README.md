# Evidence Ledger

Append-only ledger for fingerprint-bound verification results.

Standalone ES module. No npm install required. Works in **Node.js 20+** and modern browsers (serve over HTTP for browser demos).

## Install / import

Copy the files into your project, or clone this repository:

```js
import { createEvidenceLedger } from './evidence-ledger.js';
import { fingerprint } from './artifact-freshness-guard.js';
const ledger=createEvidenceLedger();
ledger.append({id:'check-1',criterionId:'total',artifactId:'invoice.json',
  fingerprint:await fingerprint('{"total":42}'), passed:true,
  createdAt:new Date().toISOString(),details:'Trusted check passed'});
console.log(ledger.list());
```

## Use cases

### 1. Keep proof behind every passed check

- **Scenario:** An invoice verification changes from failed to passed.
- **Outcome:** Store both results with artifact fingerprints so the latest decision is inspectable.

### 2. Resume an interrupted review

- **Scenario:** A local session closes before a reviewer sees the evidence.
- **Outcome:** Reload persisted records with a localStorage-compatible adapter.

## Exports

- `validateEvidence`
- `createEvidenceLedger`

## Notes

- Keep API keys and secrets out of this module and out of browser storage.
- Treat verification callbacks, ledger writers, and permission checks as trusted application code.
- This library is intentional local reliability plumbing, not a claim of cryptographic attestation unless stated in the source comments.

## License

MIT
