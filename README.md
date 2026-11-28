[![ReadyStack](https://readystack.dev/logo.svg)](https://readystack.dev)

**Stable, Open-source Releases, Automated** · [readystack.dev](https://readystack.dev)

[![Docker Hub](https://img.shields.io/badge/Docker%20Hub-readystack%2Ferpnext-2496ED?logo=docker&logoColor=white)](https://hub.docker.com/r/readystack/erpnext) [![Docker pulls](https://img.shields.io/docker/pulls/readystack/erpnext)](https://hub.docker.com/r/readystack/erpnext) [![Grade at release](https://img.shields.io/badge/grade%20at%20release-A%20%2894%25%29-2ea44f)](https://readystack.dev/products/erpnext) [![Signed: cosign](https://img.shields.io/badge/signed-cosign-2ea44f)](https://readystack.dev/keys/cosign.pub) ![SBOM: SPDX](https://img.shields.io/badge/SBOM-SPDX-2ea44f) ![Provenance: SLSA v1](https://img.shields.io/badge/provenance-SLSA%20v1-2ea44f) ![Offline rebuild: verified](https://img.shields.io/badge/offline%20rebuild-verified-2ea44f)

# ERPNext: ReadyStack build kit

The offline build kit for the Docker image `readystack/erpnext:v16.53.0-CE-ubuntu24.04-r6`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [v16.53.0-CE-ubuntu24.04-r6](https://github.com/readystack-dev/erpnext/releases/tag/v16.53.0-CE-ubuntu24.04-r6)
- Image: [`docker.io/readystack/erpnext:v16.53.0-CE-ubuntu24.04-r6`](https://hub.docker.com/r/readystack/erpnext/tags), manifest digest `sha256:0fd4fdd89e041ec75003bd6e88429c2e9fca22d1ae14342faa7285472fc12824`
- Product page: https://readystack.dev/products/erpnext
- Source and build recipe: https://readystack.dev/products/erpnext/recipe
- Build trail: https://readystack.dev/products/erpnext/trail/v16.53.0-CE-ubuntu24.04-r6
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=erpnext

## The image

ONE product container (supervisord runs the Frappe web backend [gunicorn], the Socket.IO realtime node process, one RQ background worker for the long, default and short queues, the scheduler, and the nginx desk frontend on :8080) PLUS two required datastore sidecars the customer provides: a MariaDB 11.x server and Redis (a cache instance + a queue instance; the queue instance also backs Socket.IO). NOT a single self-contained image — Frappe/ERPNext is fundamentally multi-service. The image has neither wkhtmltopdf nor Chromium: PDFs of the Standard and classic print formats fail, while Print Format Builder formats whose PDF Renderer is Typst, or WeasyPrint for a format already stored on it, render to PDF inside the image.

## Who uses ERPNext and why

Businesses that want accounting, inventory, sales, manufacturing and projects in one system.

ERPNext is an open-source ERP: invoices, stock, sales orders, suppliers, production, assets and project timesheets in one application instead of separate tools.

A typical use: A small manufacturer tracks orders in spreadsheets, stock in another tool and invoices in a third. In ERPNext sales orders, stock levels, material consumption and invoices live in one system, so the books, the warehouse and the production floor work from the same records.

From the upstream project's own description: https://github.com/frappe/erpnext.

## This release

- Docker Scout policy grade at release: **A** (94%), graded 2026-11-27 with `docker scout policy` (CLI 1.26.0, docker-default configuration).
  - Docker Scout counts 162 packages with copyleft licences (GPL, LGPL, MPL), 155 of them operating-system packages (it counts only packages whose licence it can read; the SBOM lists every component).
- Signed with ReadyStack's release key (fingerprint `04daa92344a52dbc`): https://readystack.dev/keys/cosign.pub.
- Runs as a non-root user (`frappe`).
- Attestations on the image: an SPDX SBOM and SLSA provenance v1.
- Rebuilt from this kit with network egress blocked on 2026-11-27; the rebuilt image digest is the published one.
- Base: Ubuntu 24.04.

The current grade, measured again every day, is on https://readystack.dev/products/erpnext.

ERPNext is distributed under its upstream licence (GPL-3.0-only); the kit contains upstream's source under that licence, and each vendored component under its own.

## Download

From the [v16.53.0-CE-ubuntu24.04-r6 release](https://github.com/readystack-dev/erpnext/releases/tag/v16.53.0-CE-ubuntu24.04-r6): `ReadyStack-erpnext-v16.53.0-CE-ubuntu24.04-r6.tar.gz` (755.1 MB), SHA-256 `707056a16be9a188e7921c02aacf53442b358bedb90f159f95371d74023a1d61`.

```sh
sha256sum --check --ignore-missing SHA256SUMS
```

## Verify and rebuild

The rebuild statement is signed with the ReadyStack release key. Check the signature before you rely on it:

```sh
cosign verify-blob --key https://readystack.dev/keys/cosign.pub \
  --bundle ReadyStack-erpnext-v16.53.0-CE-ubuntu24.04-r6.rebuild.json.sigstore ReadyStack-erpnext-v16.53.0-CE-ubuntu24.04-r6.rebuild.json
```

Unpack with `-p` so file modes are kept, then follow the kit's own README.md and docs/REBUILD.md:

```sh
tar -xpzf ReadyStack-erpnext-v16.53.0-CE-ubuntu24.04-r6.tar.gz
cd v16.53.0-CE-ubuntu24.04-r6
less README.md docs/REBUILD.md
```

The build trail (`ReadyStack-erpnext-v16.53.0-CE-ubuntu24.04-r6.trail.json`, signed the same way, and its Markdown copy) records how this release was built and checked.

## This repository

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/erpnext/recipe. The complete kit is the release download. Each release is a tag here. How to report a vulnerability: [SECURITY.md](SECURITY.md).

## About ReadyStack

**Stable, Open-source Releases, Automated.** ReadyStack releases popular open-source apps every week with every available critical and high security fix applied, plus full documentation, reference data, tests and a build recipe that recreates each release bit-for-bit. Each release is rebuilt from its pinned inputs with the network off, checked against its published digest, signed, and scanned and graded again every day. The images and build kits are free, and ReadyStack is soon to be a nonprofit.

[readystack.dev](https://readystack.dev) · [All products](https://readystack.dev/products.html) · [Build kits on GitHub](https://github.com/readystack-dev) · [Defect log](https://readystack.dev/defects.html) · contact@readystack.dev

— ReadyStack · https://readystack.dev
