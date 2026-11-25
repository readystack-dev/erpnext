# ERPNext v16.53.0 — ReadyStack release `v16.53.0-CE-ubuntu24.04-r5`

Generated 2026-11-25 from this release's build records and strategy. Statements that come from a single record name it in brackets; the others come from this release's strategy and build log.

## Release

- **Image:** `readystack/erpnext:v16.53.0-CE-ubuntu24.04-r5` (linux/amd64). Index digest `sha256:41e34d729bf700e9b43c69bae9a4069b5f595f4e08c12d90bf979d3e999b953b` [`docs/provenance/LOCKED_DIGEST.txt`].
- **Image manifest digest:** `sha256:3cfcd1c83ef25cf820885ff4a9e73f64bf8e46a3b4d053d09c6cd6380e066909` [`TARGET_DIGEST.txt`].
- **Upstream:** ERPNext v16.53.0 built from source at `v16.53.0` of https://github.com/frappe/erpnext — upstream notes: https://github.com/frappe/erpnext/releases/tag/v16.53.0 [`docs/provenance/BUILD_RECIPE.json`].
- **Base image:** `ubuntu:24.04`; runtime user `frappe`.
- **Build:** `source-rebuild-python`, compiled offline with `--network=none`.
- **Supersedes:** ReadyStack release `v16.53.0-CE-ubuntu24.04-r4`.

## What changed in this release

- Upstream version unchanged (v16.53.0); ReadyStack rebuild.
- ERPNext v16.53.0 is unchanged from the release this supersedes (v16.53.0-CE-ubuntu24.04-r4); this release rebuilds it. Changes: libssh-4 moves from 0.10.6-2ubuntu0.5 to 0.10.6-2ubuntu0.6 (USN-9187-1). Settings, ports and data volumes are those of v16.53.0-CE-ubuntu24.04-r4: replace the container with this image on the same volumes.

## Security status at release (measured 2026-11-25)

- **Docker Scout:** 0 fixable critical/high vulnerabilities after 1 OpenVEX statement of ours (`docs/security/VEX.openvex.json`; Docker Scout's default policy does not read them and counts it as fixable); runs as `frappe` (non-root); SBOM + provenance attestations present (SPDX SBOM + SLSA v1) [`docs/provenance/SCOUT_VERDICT.json`].
- **OSV cross-check:** no fixable critical/high vulnerability beyond Docker Scout's findings.
- **Signature:** cosign signature verified by ReadyStack's release gate before publishing; check it yourself with `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/erpnext:v16.53.0-CE-ubuntu24.04-r5` (signatures are recorded in the public Sigstore transparency log).
- **ReadyStack release check at release:** passed (ReadyStack's own test, not a Docker Scout grade). Vulnerabilities are disclosed every day and the image never changes, so it is re-checked daily, beside Docker Scout's own dated grade, at https://readystack.dev/queue.
- **Before exposing this service:** Frappe's bench command writes every command line it runs, in clear text, to /home/frappe/frappe-bench/logs/bench.log (mode 644) inside the container. The entrypoint's first-boot `bench new-site` passes the Administrator password (ADMIN_PASSWORD or the generated one) and DB_ROOT_PASSWORD, your MariaDB root password, as arguments, so both are stored in plain text in that file, as is any secret you later pass to a bench command as an argument (set-admin-password '<new password>', restore --db-root-password, set-config encryption_key). The file is in the container's own filesystem, not in the sites volume: after the first boot, re-create the container (`docker stop` and `docker rm`, then the same `docker run` command; the site, its data and its passwords are kept, and the new bench.log does not have them), type a new Administrator password at the set-admin-password prompt (bench.log then records the command, not the password), and do not copy that logs directory out of the container.

## Reproducibility

Rebuilds offline from this archive to the identical image digest `sha256:3cfcd1c83ef25cf820885ff4a9e73f64bf8e46a3b4d053d09c6cd6380e066909`: run `./BUILD_OFFLINE.sh`, then `./VERIFY_OFFLINE.sh` (add `--online` to confirm the Docker Hub tag holds the same digest). Before publishing, ReadyStack rebuilt the kit with `./BUILD_OFFLINE.sh` and compared the result with the published digest [`docs/provenance/REPRO_VERIFICATION.json`], then ran `./BUILD_OFFLINE.sh` and `./VERIFY_OFFLINE.sh` from this archive (without `--online`).

## Validation

- 3 of 3 use cases passed (3 authored) against the running image [`docs/validation/test-results.json`].
- The cases are `GET /api/method/ping` (200), `GET /api/method/frappe.auth.get_logged_user` (200), `GET /api/method/frappe.client.get_count?doctype=Company` (200); the suite checks nothing else.

## Known issues

- **medium** (upstream): Secret written in plain text or to the log by default [`RSD-erpnext-a400902f2b`]
- **low** (ReadyStack package): Admin handbook: Round 2 finding still open (RSD-erpnext-bc6dd51421): the product's backup writes only the database dump, site_config_backup.json and the files tarballs, and restore reads only those, so it cannot… [`RSD-erpnext-0e3bedb805`] (carried from `v16.53.0-CE-ubuntu24.04-r1`, recorded there as `RSD-erpnext-bc6dd51421`)

## Verify this archive

```
sha256sum -c CHECKSUMS.sha256
./BUILD_OFFLINE.sh && ./VERIFY_OFFLINE.sh --online
cosign verify --key https://readystack.dev/keys/cosign.pub readystack/erpnext:v16.53.0-CE-ubuntu24.04-r5
```

ReadyStack records every signature in the public Sigstore transparency log (Rekor), so the command needs no extra flags.

