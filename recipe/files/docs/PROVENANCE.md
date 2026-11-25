# Provenance — ERPNext (`v16.53.0-CE-ubuntu24.04-r5`)

Every item below is copied from a record in this archive; the record is named in brackets.

## Source

- Upstream repository: https://github.com/frappe/erpnext
- Revision built: `v16.53.0` (commit `9cd11b19575bfc34f092a24f6c8b368c4dd69481`)
- Source tree: `e9e194e2af7ed58c0f42e27a67378f1df9b975c9ba880bc0f3cdd898c7896209` over 5581 files [`docs/provenance/SOURCE_TREE_HASH.json`]
- Community Edition only: enterprise code is removed or refused before the build (CE audit at acquire).

## Build

- Method: `source-rebuild-python`; base image `ubuntu:24.04`
- Compiled with `--network=none` from vendored source, dependencies and base images; BuildKit pinned to `moby/buildkit:v0.31.2` (shipped in `toolchain/`).
- SOURCE_DATE_EPOCH: `1795543289` [`SOURCE_DATE_EPOCH.txt`]
- Frozen inputs: [`docs/provenance/FREEZE_MANIFEST.json`], build recipe: [`docs/provenance/BUILD_RECIPE.json`].

## Output

- Published image: `readystack/erpnext:v16.53.0-CE-ubuntu24.04-r5` — index digest `sha256:41e34d729bf700e9b43c69bae9a4069b5f595f4e08c12d90bf979d3e999b953b` [`docs/provenance/LOCKED_DIGEST.txt`]
- linux/amd64 image digest `sha256:3cfcd1c83ef25cf820885ff4a9e73f64bf8e46a3b4d053d09c6cd6380e066909` — reproduced from this archive before publishing [`docs/provenance/REPRO_VERIFICATION.json`].

## Attestations and signature

- SBOM + SLSA provenance attached to the image: attached: an SPDX SBOM and SLSA v1 provenance [`docs/provenance/SCOUT_VERDICT.json`]
- cosign signature by the ReadyStack release key: verified before publishing. Check it: `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/erpnext:v16.53.0-CE-ubuntu24.04-r5`

## Pinned inputs, and why

- 17 pinned inputs, each with where it came from, why this one, how it was checked and when it was decided: `docs/PINS.md` [`docs/provenance/PINS.json`] (upstream source 2, base and build images 1, image digests 1, language runtimes and toolchains 2, files the vendor stage downloads 1, pins in the kit's dockerfiles 4, readystack's build engine 1, dependencies upstream chose 2, services the release checks run beside 3).

## Build trail

- How this release passed through the ReadyStack harness, record by record (every chain, drive, stage, review round, defect and check, each naming the record it is copied from): `ReadyStack-erpnext-v16.53.0-CE-ubuntu24.04-r5.trail.json`, published beside this archive and signed with the release key (`ReadyStack-erpnext-v16.53.0-CE-ubuntu24.04-r5.trail.json.sigstore`), and readable at https://readystack.dev/products/erpnext/trail/v16.53.0-CE-ubuntu24.04-r5.

