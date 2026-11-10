# APIsec Surface org scan

Nightly scan of your GitHub organization with APIsec Surface. This repository holds only the caller
workflow; the scan logic is in [apisec-inc/apisec-orchestrator](https://github.com/apisec-inc/apisec-orchestrator).

## Setup

1. Give the workflow read access to your repositories. Choose one of the auth options below.
   **GitHub App auth is preferred.**
2. Add the secret `APISEC_TOKEN` (an APIsec token with **Create App** and **Get App**) and the variables
   `APISEC_ENDPOINT` (e.g. `https://api.apisecapps.com`) and `APISEC_REGISTRATION_CODE` (the code APIsec
   gave you). Use Settings → Secrets and variables → Actions, on this repository or at org level.
3. Actions → **APIsec Surface org scan** → **Run workflow**. Enable **dry_run** first to check setup
   (nothing is uploaded), then run without it. After that, scans run nightly at 02:00 UTC.

## Auth options

### GitHub App (preferred)

Use the Surface Code GitHub App that connects your org to APIsec. It belongs to the org rather than a
person, its key doesn't expire, each job gets a short-lived token, and the repositories selected on its
installation are what APIsec lists and what gets scanned.

1. In the app's settings, add **Contents: Read-only** to its repository permissions, then approve the
   new permission on the org's installation of the app.
2. Generate a private key for this workflow. The key you gave APIsec stays there; APIsec uses it only for
   metadata, never for code.
3. Add the variable `ORCHESTRATOR_APP_ID` (the app's App ID) and the secret
   `ORCHESTRATOR_APP_PRIVATE_KEY` (the full `.pem` file).

To keep APIsec's key away from code entirely, you can use a separate scan-only app instead. See
[GitHub access](https://github.com/apisec-inc/apisec-orchestrator#github-access).

### Personal access token

Add the secret `ORG_READ_TOKEN`: a fine-grained PAT for the org with **Contents: read** and
**Metadata: read** on the repositories to scan. It belongs to the user who creates it and stops working
when it expires or that user loses access to the org. If both are set, the GitHub App is used.

## Runners

Jobs run on GitHub-hosted runners by default. Set the variable `ORCHESTRATOR_RUNNER` to `self-hosted`
(runners labelled `self-hosted` and `apisec`), or to a runner label such as a larger runner's name.
Other options: [Optional variables](https://github.com/apisec-inc/apisec-orchestrator#optional-variables).
