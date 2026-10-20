# APIsec Surface org scan

Nightly scan of your GitHub organization with APIsec Surface.

1. Add secrets `APISEC_TOKEN` (APIsec token) and `ORG_READ_TOKEN` (fine-grained GitHub PAT for the org with
   **Contents: read** and **Metadata: read**).
2. Add the variable `APISEC_ENDPOINT`, e.g. `https://api.apisecapps.com`.
3. Actions → **APIsec Surface org scan** → **Run workflow**. Optionally enable **dry_run** first to verify
   setup; run again without it to upload results to APIsec.

Setup, options, and troubleshooting: [apisec-inc/apisec-orchestrator](https://github.com/apisec-inc/apisec-orchestrator).
