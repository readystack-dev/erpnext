# ERPNext: ReadyStack build kit

The offline build kit for the Docker image `readystack/erpnext:v16.53.0-CE-ubuntu24.04-r5`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [v16.53.0-CE-ubuntu24.04-r5](https://github.com/readystack-dev/erpnext/releases/tag/v16.53.0-CE-ubuntu24.04-r5)
- Image: [`docker.io/readystack/erpnext:v16.53.0-CE-ubuntu24.04-r5`](https://hub.docker.com/r/readystack/erpnext/tags), manifest digest `sha256:3cfcd1c83ef25cf820885ff4a9e73f64bf8e46a3b4d053d09c6cd6380e066909`
- Product page: https://readystack.dev/products/erpnext
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=erpnext

ERPNext is distributed under its upstream licence (GPL-3.0-only); the kit contains upstream's source under that licence, and each vendored component under its own.

## Download

From the [v16.53.0-CE-ubuntu24.04-r5 release](https://github.com/readystack-dev/erpnext/releases/tag/v16.53.0-CE-ubuntu24.04-r5): `ReadyStack-erpnext-v16.53.0-CE-ubuntu24.04-r5.tar.gz` (753.9 MB), SHA-256 `5bc0e915118bf9583cfbf847748fdfebb9ab16571b9c323037549968867bfa10`.

```sh
sha256sum --check --ignore-missing SHA256SUMS
```

## Verify and rebuild

The rebuild statement is signed with the ReadyStack release key. Check the signature before you rely on it:

```sh
cosign verify-blob --key https://readystack.dev/keys/cosign.pub \
  --bundle ReadyStack-erpnext-v16.53.0-CE-ubuntu24.04-r5.rebuild.json.sigstore ReadyStack-erpnext-v16.53.0-CE-ubuntu24.04-r5.rebuild.json
```

Unpack with `-p` so file modes are kept, then follow the kit's own README.md and docs/REBUILD.md:

```sh
tar -xpzf ReadyStack-erpnext-v16.53.0-CE-ubuntu24.04-r5.tar.gz
cd v16.53.0-CE-ubuntu24.04-r5
less README.md docs/REBUILD.md
```

The build trail (`ReadyStack-erpnext-v16.53.0-CE-ubuntu24.04-r5.trail.json`, signed the same way, and its Markdown copy) records how this release was built and checked.

## This repository

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/erpnext/recipe. The complete kit is the release download. Each release is a tag here.
