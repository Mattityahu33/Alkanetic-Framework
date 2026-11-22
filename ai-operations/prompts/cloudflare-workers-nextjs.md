---
id: "AI-TPL-001"
title: "Coding agent prompt for Next.js on Cloudflare Workers"
category: "ai-operations"
type: "template"
status: "review"
owner: "Alkanetic AI Operations"
version: "0.1.0"
created: "2026-11-22"
last_updated: "2026-11-22"
review_due: "TBD"
related_documents: ["SOP-DEP-001", "DEP-GD-001", "TPL-DEP-001", "DEP-REF-001", "CL-DEP-001"]
dependencies: ["Cloudflare Workers", "Next.js", "OpenNext", "pnpm"]
tags: ["cloudflare", "nextjs", "deployment"]
---

# Coding agent prompt for Next.js on Cloudflare Workers

## Purpose

Provide a reusable template for delivering an existing Next.js application to Cloudflare Workers with OpenNext.

## Prompt

> Read repository instructions and inspect build, auth, and deployment configuration. Work on a dedicated branch. Confirm official Next.js, OpenNext, Wrangler and pnpm requirements before pinning versions. Use the repository's package manager and approve only named native builds after review.
>
> Target the specified isolated Worker and backend. Keep existing application authorization. Identify build-time public variables, runtime bindings, and which service owns each secret. Avoid putting secrets in documentation or client assets. Do not modify DNS, publish a Worker, or use real data without explicit approval.
>
> Run a fresh frozen install, TypeScript, lint, relevant security tests, native build, adapter build and local workerd preview. Probe static assets, dynamic routes, empty query data, and HTTP auth forwarding using synthetic fixtures. Record the actual commands, results, and any untested live validation.
>
> Document each root cause and fix, the build and deployment settings, and a rollback path. Prepare the review branch and pull request per the owner's publication scope. Report what awaits live approval and verification.

Use with the [deployment SOP](../../sop/cloudflare-workers-nextjs.md) and [release checklist](../../checklists/cloudflare-workers-nextjs.md).

## Status

In review. The referenced application build and local workerd workflow were validated with synthetic fixtures. Hosted deployment, TLS, Cloudflare Access and real upstream authentication still require validation for each target.
