---
id: "CL-DEP-001"
title: "Cloudflare Workers release checklist for Next.js"
category: "checklists"
type: "checklist"
status: "review"
owner: "Alkanetic Engineering"
version: "0.1.0"
created: "2026-11-22"
last_updated: "2026-11-22"
review_due: "TBD"
related_documents: ["SOP-DEP-001", "DEP-GD-001", "TPL-DEP-001", "DEP-REF-001", "AI-TPL-001"]
dependencies: ["Cloudflare Workers", "Next.js", "OpenNext", "pnpm"]
tags: ["cloudflare", "nextjs", "deployment"]
---

# Cloudflare Workers release checklist for Next.js

## Purpose

Provide a reusable checklist for delivering an existing Next.js application to Cloudflare Workers with OpenNext.

## Before release

- [ ] Repository instructions, approval, exact commit, Worker, branch and environment reviewed.
- [ ] Peer ranges, Node and pnpm pins checked. Fresh frozen install succeeds, including reviewed native postinstall scripts.
- [ ] TypeScript, lint, backend/security tests, native build, OpenNext build and local workerd smoke pass.
- [ ] Static assets, real path parameters, empty/short query results and forwarding of auth HTTP responses verified with isolated fixtures.
- [ ] Build public variables and runtime settings match the dedicated environment. Backend canonical origin and secret set on the backend. No credentials appear in source or artifacts.
- [ ] Account permissions, deploy branch, Access rules and custom domain conflicts checked. Alternate hostnames and preview deploys disabled or explicitly protected.
- [ ] Reviewed local bundle size and measured live CPU/startup requirements within target plan before broader rollout.
- [ ] Known-good version, rollback permissions and responsible operator recorded.

## After separately approved release

- [ ] Canonical TLS and Access allow/deny/expiry pass.
- [ ] Synthetic signup, login, session reload, logout, roles, ownership, and real-time backend operations pass.
- [ ] Direct backend public endpoints satisfy the agreed abuse-control policy.
- [ ] Correct version and backend revision recorded. Review logs and rollback if acceptance fails.

## Status

In review. The referenced application build and local workerd workflow were validated with synthetic fixtures. Hosted deployment, TLS, Cloudflare Access and real upstream authentication still require validation for each target.
