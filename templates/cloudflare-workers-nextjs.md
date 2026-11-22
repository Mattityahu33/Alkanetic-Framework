---
id: "TPL-DEP-001"
title: "OpenNext and Wrangler configuration templates"
category: "templates"
type: "template"
status: "review"
owner: "Alkanetic Engineering"
version: "0.1.0"
created: "2026-11-22"
last_updated: "2026-11-22"
review_due: "TBD"
related_documents: ["SOP-DEP-001", "DEP-GD-001", "DEP-REF-001", "CL-DEP-001", "AI-TPL-001"]
dependencies: ["Cloudflare Workers", "Next.js", "OpenNext", "pnpm"]
tags: ["cloudflare", "nextjs", "deployment"]
---

# OpenNext and Wrangler configuration templates

## Purpose

Provide a reusable template for delivering an existing Next.js application to Cloudflare Workers with OpenNext.

## Package configuration

Locally validated example pins on Node 24.22.3 and pnpm 11.21.0: Next.js and eslint-config-next `16.4.6`, `@opennextjs/cloudflare` `1.20.18`, Wrangler `4.166.0`, and transitive workerd `1.20261119.1`. Verify current peer ranges and supported patches before reuse. Merge with existing entries.

```json
{
  "scripts": {
    "build": "next build",
    "build:cf": "opennextjs-cloudflare build",
    "preview:cf": "opennextjs-cloudflare preview",
    "deploy:cf": "opennextjs-cloudflare deploy"
  }
}
```

In `pnpm-workspace.yaml`, add `workerd: true` below the existing `allowBuilds:` after reviewing the pinned dependency. Keep existing approvals. In `open-next.config.ts`:

```ts
import { defineCloudflareConfig } from "@opennextjs/cloudflare";

export default defineCloudflareConfig();
```

## Worker configuration

Replace both occurrences of `example-app-dev` in `wrangler.jsonc`. The compatibility profile is the locally tested example. The `keep_names` setting protects serialized inline scripts such as next-themes from references to esbuild's out-of-scope name helper. Check the current adapter and Workers compatibility guidance when changing the profile. Use `keep_vars` when runtime public vars are dashboard-managed. For infrastructure-managed vars, choose a single source of truth.

```jsonc
{
  "$schema": "./node_modules/wrangler/config-schema.json",
  "name": "example-app-dev",
  "main": ".open-next/worker.js",
  "compatibility_date": "2026-08-03",
  "compatibility_flags": ["nodejs_compat", "global_fetch_strictly_public"],
  "workers_dev": false,
  "preview_urls": false,
  "keep_vars": true,
  "keep_names": false,
  "assets": { "directory": ".open-next/assets", "binding": "ASSETS" },
  "services": [
    { "binding": "WORKER_SELF_REFERENCE", "service": "example-app-dev" }
  ],
  "observability": { "enabled": true, "head_sampling_rate": 0.1 }
}
```

Ignore `.open-next/`, `.wrangler/`, `.dev.vars*`, and real `.env*` files in Git. Allow only a scrubbed `.env.example`. Exclude build output from linters. If using Convex, an example can show `NEXT_PUBLIC_CONVEX_URL=https://example.convex.cloud` and `NEXT_PUBLIC_CONVEX_SITE_URL=https://example.convex.site`. Set real hosted values through build and Worker settings. Keep `SITE_URL` and `BETTER_AUTH_SECRET` on the dedicated Convex deployment.

[OpenNext setup](https://opennext.js.org/cloudflare/get-started) · [Wrangler configuration reference](https://developers.cloudflare.com/workers/wrangler/configuration/)

## Status

In review. The referenced application build and local workerd workflow were validated with synthetic fixtures. Hosted deployment, TLS, Cloudflare Access and real upstream authentication still require validation for each target.
