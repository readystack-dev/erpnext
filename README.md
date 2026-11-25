# ERPNext: ReadyStack build kit

The offline build kit for the Docker image `readystack/erpnext:v16.53.0-CE-ubuntu24.04-r5`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [v16.53.0-CE-ubuntu24.04-r5](https://github.com/readystack-dev/erpnext/releases/tag/v16.53.0-CE-ubuntu24.04-r5)
- Image: [`docker.io/readystack/erpnext:v16.53.0-CE-ubuntu24.04-r5`](https://hub.docker.com/r/readystack/erpnext/tags), manifest digest `sha256:3cfcd1c83ef25cf820885ff4a9e73f64bf8e46a3b4d053d09c6cd6380e066909`
- Product page: https://readystack.dev/products/erpnext
- Source and build recipe: https://readystack.dev/products/erpnext/recipe
- Build trail: https://readystack.dev/products/erpnext/trail/v16.53.0-CE-ubuntu24.04-r5
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=erpnext

## The image

ONE product container (supervisord runs the Frappe web backend [gunicorn], the Socket.IO realtime node process, one RQ background worker for the long, default and short queues, the scheduler, and the nginx desk frontend on :8080) PLUS two required datastore sidecars the customer provides: a MariaDB 11.x server and Redis (a cache instance + a queue instance; the queue instance also backs Socket.IO). NOT a single self-contained image — Frappe/ERPNext is fundamentally multi-service. The image has neither wkhtmltopdf nor Chromium: PDFs of the Standard and classic print formats fail, while Print Format Builder formats whose PDF Renderer is Typst, or WeasyPrint for a format already stored on it, render to PDF inside the image.

## Who uses ERPNext and why

Businesses that want accounting, inventory, sales, manufacturing and projects in one system.

ERPNext is an open-source ERP: invoices, stock, sales orders, suppliers, production, assets and project timesheets in one application instead of separate tools.

A typical use: A small manufacturer tracks orders in spreadsheets, stock in another tool and invoices in a third. In ERPNext sales orders, stock levels, material consumption and invoices live in one system, so the books, the warehouse and the production floor work from the same records.

From the upstream project's own description: https://github.com/frappe/erpnext.

## This release

- Docker Scout policy grade at release: **A** (94%), graded 2026-11-25 with `docker scout policy` (CLI 1.26.0, docker-default configuration).
  - Docker Scout counts 162 packages with copyleft licences (GPL, LGPL, MPL), 155 of them operating-system packages (it counts only packages whose licence it can read; the SBOM lists every component).
- Signed with ReadyStack's release key (fingerprint `04daa92344a52dbc`): https://readystack.dev/keys/cosign.pub.
- Runs as a non-root user (`frappe`).
- Attestations on the image: an SPDX SBOM and SLSA provenance v1.
- Rebuilt from this kit with network egress blocked on 2026-11-25; the rebuilt image digest is the published one.
- Base: Ubuntu 24.04.

The current grade, measured again every day, is on https://readystack.dev/products/erpnext.

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

— ReadyStack · https://readystack.dev
