# Provenance — ERPNext (`v16.53.0-CE-ubuntu24.04-r4`)

Every item below is copied from a record in this archive; the record is named in brackets.

## Source

- Upstream repository: https://github.com/frappe/erpnext
- Revision built: `v16.53.0` (commit `9cd11b19575bfc34f092a24f6c8b368c4dd69481`)
- Source tree: `e9e194e2af7ed58c0f42e27a67378f1df9b975c9ba880bc0f3cdd898c7896209` over 5581 files [`docs/provenance/SOURCE_TREE_HASH.json`]
- Community Edition only: enterprise code is removed or refused before the build (CE audit at acquire).

## Build

- Method: `source-rebuild-python`; base image `ubuntu:24.04`
- Compiled with `--network=none` from vendored source, dependencies and base images; BuildKit pinned to `moby/buildkit:v0.31.2` (shipped in `toolchain/`).
- SOURCE_DATE_EPOCH: `1795408350` [`SOURCE_DATE_EPOCH.txt`]
- Frozen inputs: [`docs/provenance/FREEZE_MANIFEST.json`], build recipe: [`docs/provenance/BUILD_RECIPE.json`].

## Output

- Published image: `readystack/erpnext:v16.53.0-CE-ubuntu24.04-r4` — index digest `sha256:ab0775d305877fe21a2db96618d88adbdcfafe44fe491ebc5197bc771a1c4b7f` [`docs/provenance/LOCKED_DIGEST.txt`]
- linux/amd64 image digest `sha256:aa463aa8378d3754d58d66ff7de68e860255a84cb69f65d6c54da3b7ad8275e4` — reproduced from this archive before publishing [`docs/provenance/REPRO_VERIFICATION.json`].

## Attestations and signature

- SBOM + SLSA provenance attached to the image: attached: an SPDX SBOM and SLSA v1 provenance [`docs/provenance/SCOUT_VERDICT.json`]
- cosign signature by the ReadyStack release key: verified before publishing. Check it: `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/erpnext:v16.53.0-CE-ubuntu24.04-r4`

## Pinned inputs, and why

- 17 pinned inputs, each with where it came from, why this one, how it was checked and when it was decided: `docs/PINS.md` [`docs/provenance/PINS.json`] (upstream source 2, base and build images 1, image digests 1, language runtimes and toolchains 2, files the vendor stage downloads 1, pins in the kit's dockerfiles 4, readystack's build engine 1, dependencies upstream chose 2, services the release checks run beside 3).

## Build trail

- How this release passed through the ReadyStack harness, record by record (every chain, drive, stage, review round, defect and check, each naming the record it is copied from): `ReadyStack-erpnext-v16.53.0-CE-ubuntu24.04-r4.trail.json`, published beside this archive and signed with the release key (`ReadyStack-erpnext-v16.53.0-CE-ubuntu24.04-r4.trail.json.sigstore`), and readable at https://readystack.dev/products/erpnext/trail/v16.53.0-CE-ubuntu24.04-r4.

