---
id: "DEP-GD-001"
title: "Cloudflare Workers and Next.js quick start"
category: "deployment"
type: "guide"
status: "review"
owner: "Alkanetic Engineering"
version: "0.1.0"
created: "2026-11-22"
last_updated: "2026-11-22"
review_due: "TBD"
related_documents: ["SOP-DEP-001", "TPL-DEP-001", "DEP-REF-001", "CL-DEP-001", "AI-TPL-001"]
dependencies: ["Cloudflare Workers", "Next.js", "OpenNext", "pnpm"]
tags: ["cloudflare", "nextjs", "deployment"]
---

# Cloudflare Workers and Next.js quick start

## Purpose

Provide a reusable guide for delivering an existing Next.js application to Cloudflare Workers with OpenNext.

## Local workflow

Use the repo's pinned package manager and compatible Node version. Apply the [configuration template](../templates/cloudflare-workers-nextjs.md) and supply approved nonproduction public backend URLs in the shell or an ignored `.env.local`.

```sh
pnpm install --frozen-lockfile
pnpm exec tsc --noEmit --incremental false
pnpm run lint
pnpm run build
pnpm run build:cf
pnpm run preview:cf --port 8787
```

Before preview, run the repository's in-memory security tests. With preview running, visit `http://127.0.0.1:8787` and check static assets, dynamic routes, error states, and same-origin auth forwarding. Use a local fixture or an approved isolated backend. A local mock verifies forwarding and response handling. Use a dedicated backend and HTTPS to test real sessions.

Record the Worker artifact size with `OPEN_NEXT_DEPLOY=true pnpm exec wrangler deploy --dry-run --outdir .wrangler/dry-run`. The environment switch prevents Wrangler delegating the dry run to an adapter deploy command. For the reviewed release procedure, see the [SOP](../sop/cloudflare-workers-nextjs.md).

[Cloudflare OpenNext guide](https://developers.cloudflare.com/workers/framework-guides/web-apps/opennext/) · [OpenNext environment variables](https://opennext.js.org/cloudflare/howtos/env-vars)

## Status

In review. The referenced application build and local workerd workflow were validated with synthetic fixtures. Hosted deployment, TLS, Cloudflare Access and real upstream authentication still require validation for each target.
