# ERPNext: ReadyStack build kit

The offline build kit for the Docker image `readystack/erpnext:v16.53.0-CE-ubuntu24.04-r4`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [v16.53.0-CE-ubuntu24.04-r4](https://github.com/readystack-dev/erpnext/releases/tag/v16.53.0-CE-ubuntu24.04-r4)
- Image: [`docker.io/readystack/erpnext:v16.53.0-CE-ubuntu24.04-r4`](https://hub.docker.com/r/readystack/erpnext/tags), manifest digest `sha256:aa463aa8378d3754d58d66ff7de68e860255a84cb69f65d6c54da3b7ad8275e4`
- Product page: https://readystack.dev/products/erpnext
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=erpnext

ERPNext is distributed under its upstream licence (GPL-3.0-only); the kit contains upstream's source under that licence, and each vendored component under its own.

## Download

From the [v16.53.0-CE-ubuntu24.04-r4 release](https://github.com/readystack-dev/erpnext/releases/tag/v16.53.0-CE-ubuntu24.04-r4): `ReadyStack-erpnext-v16.53.0-CE-ubuntu24.04-r4.tar.gz` (753.8 MB), SHA-256 `9025e9d77b7788f78ca105887e749065bf72b611b6650cbb50b46752b272c47f`.

```sh
sha256sum --check --ignore-missing SHA256SUMS
```

## Verify and rebuild

The rebuild statement is signed with the ReadyStack release key. Check the signature before you rely on it:

```sh
cosign verify-blob --key https://readystack.dev/keys/cosign.pub \
  --bundle ReadyStack-erpnext-v16.53.0-CE-ubuntu24.04-r4.rebuild.json.sigstore ReadyStack-erpnext-v16.53.0-CE-ubuntu24.04-r4.rebuild.json
```

Unpack with `-p` so file modes are kept, then follow the kit's own README.md and docs/REBUILD.md:

```sh
tar -xpzf ReadyStack-erpnext-v16.53.0-CE-ubuntu24.04-r4.tar.gz
cd v16.53.0-CE-ubuntu24.04-r4
less README.md docs/REBUILD.md
```

The build trail (`ReadyStack-erpnext-v16.53.0-CE-ubuntu24.04-r4.trail.json`, signed the same way, and its Markdown copy) records how this release was built and checked.

## This repository

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/erpnext/recipe. The complete kit is the release download. Each release is a tag here.
