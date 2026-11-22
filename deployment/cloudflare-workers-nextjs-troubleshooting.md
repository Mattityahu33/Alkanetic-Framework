---
id: "DEP-REF-001"
title: "Troubleshoot Next.js on Cloudflare Workers"
category: "deployment"
type: "reference"
status: "review"
owner: "Alkanetic Engineering"
version: "0.1.0"
created: "2026-11-22"
last_updated: "2026-11-22"
review_due: "TBD"
related_documents: ["SOP-DEP-001", "DEP-GD-001", "TPL-DEP-001", "CL-DEP-001", "AI-TPL-001"]
dependencies: ["Cloudflare Workers", "Next.js", "OpenNext", "pnpm"]
tags: ["cloudflare", "nextjs", "deployment"]
---

# Troubleshoot Next.js on Cloudflare Workers

## Purpose

Provide a reusable reference for delivering an existing Next.js application to Cloudflare Workers with OpenNext.

## Common failures

| Symptom | Cause or diagnostic | Resolution |
| --- | --- | --- |
| Incompatible Next.js peer | Installed Next.js falls below the adapter's release-specific range. | Check the adapter manifest. Pin a supported Next.js patch and align eslint-config-next. Regenerate the lockfile. |
| `ERR_PNPM_IGNORED_BUILDS` names workerd | pnpm has no explicit decision for the runtime package's postinstall. | Review that pinned package and approve only `workerd: true` in `allowBuilds`. Prove a fresh frozen install and actual workerd startup. |
| Wrangler cannot be resolved, or selects the wrong release | Wrangler is missing locally or was fetched implicitly. | Pin it in devDependencies within the OpenNext peer range. Verify the effective local CLI version and Node engine. |
| Corepack direct download fails | Tool bootstrap and registry clients can take different network paths. | Verify the registry, then use `npm exec --package=pnpm@<pinned-version> -- pnpm ...` if the normal npm connection works. Keep the project pin and TLS settings. |
| Convex URL missing or browser still calls old deployment | Next inlines direct `NEXT_PUBLIC_` reads at build time. | Set the correct endpoints in Workers Builds and rebuild. Check Worker runtime settings separately. Match the API and HTTP Actions origins to the same backend. |
| Auth forwarding works locally but hosted sessions fail | Check origin, auth secret, cookie attributes, and Access behavior. | Verify `SITE_URL` on the auth backend against the canonical HTTPS app URL. Test fresh signup, sign-in, reload, and logout with synthetic accounts. Keep role, origin and CSRF defenses intact. |
| Dynamic page renders a blank slug | Next's awaited params key must match the segment name in brackets. | Align the parameter name with the route and request a concrete slug in preview. |
| Blog fails when the query resolves to an empty or short array | Optional access to the array alone does not guard an out-of-range element. | Handle loading and empty arrays, and guard element access. Exercise zero, short, and full results in the browser. |
| Public Convex subscriptions never resolve for guests | A shared client configured with `expectAuth: true` waits for an initial token. | For mixed public/protected apps, use the default socket startup or give public queries a separate client. Verify protected queries still wait behind auth guards and enforce permissions on the backend. |
| `__name is not defined` in an inline next-themes script | Wrangler's default esbuild name preservation inserted a helper reference inside a function that next-themes serializes for the browser. | Use `keep_names: false` and retest pre-hydration theme selection and browser errors on the generated Worker. |

For startup errors, verify the compatibility profile and exact config paths. For limits errors, use the actual Cloudflare bundle, CPU and memory measurements. Treat live TLS, Access, cookies and edge limits as separate release checks.

## Status

In review. The referenced application build and local workerd workflow were validated with synthetic fixtures. Hosted deployment, TLS, Cloudflare Access and real upstream authentication still require validation for each target.
