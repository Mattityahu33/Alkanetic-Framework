---
id: "SOP-DEP-001"
title: "Deploy Next.js to Cloudflare Workers"
category: "sop"
type: "sop"
status: "review"
owner: "Alkanetic Engineering"
version: "0.1.0"
created: "2026-11-22"
last_updated: "2026-11-22"
review_due: "TBD"
related_documents: ["DEP-GD-001", "TPL-DEP-001", "DEP-REF-001", "CL-DEP-001", "AI-TPL-001"]
dependencies: ["Cloudflare Workers", "Next.js", "OpenNext", "pnpm"]
tags: ["cloudflare", "nextjs", "deployment"]
---

# Deploy Next.js to Cloudflare Workers

## Purpose

Provide a reusable sop for delivering an existing Next.js application to Cloudflare Workers with OpenNext.

## Procedure

1. Confirm the target Worker, deploy branch, cloud account, backend environment, and approvals. Keep unrelated domains and production resources outside the change.
2. Check the OpenNext manifest peer ranges, Next.js release notes, and Wrangler's Node requirement. Pin compatible releases and the pnpm version. Generate the lockfile and prove a clean frozen install.
3. Apply the [configuration template](../templates/cloudflare-workers-nextjs.md). Inspect the bundle and run the [release checklist](../checklists/cloudflare-workers-nextjs.md).
4. Have the environment owner scope the Workers Builds trigger to the approved branch, disable unwanted previews, and set the exact build and deploy commands. Use a deploy identity scoped to the target Worker where the account supports it.
5. Set public backend URLs in Build Variables and mirror them in runtime settings where required. Set the canonical app origin and auth secret on the auth backend. Protect a private dev hostname with Access before making it reachable. Review DNS conflicts and certificate issuance before attaching the custom domain.
6. With release approval, run the deploy command or let the approved branch trigger run it. Record the Git revision, Worker version, backend revision, and previous version ID. Verify the hosted checklist with synthetic accounts.
7. If a release fails, stop further releases. Confirm the affected Worker and known-good version, then run `pnpm exec wrangler rollback <version-id>` from its config directory or select that version in the dashboard. Recheck routes and auth. Restore dashboard settings separately if they changed. Revert or fix source before resuming automated deployment.

Cloudflare Access protects the routed app. Independently assess direct backend endpoints. Keep app role and ownership enforcement in the backend.

[Cloudflare Workers Builds](https://developers.cloudflare.com/workers/ci-cd/builds/configuration/) · [Workers rollbacks](https://developers.cloudflare.com/workers/configuration/versions-and-deployments/rollbacks/)

## Status

In review. The referenced application build and local workerd workflow were validated with synthetic fixtures. Hosted deployment, TLS, Cloudflare Access and real upstream authentication still require validation for each target.
