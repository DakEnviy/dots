---
name: update-config-docs
description: "Update CONFIGS.md after material app configuration changes; run a full audit only when requested or documentation drift is suspected."
---

# Update Config Docs

Update `CONFIGS.md` only for material, user-visible application changes.

- Default: inspect current changes; trace affected apps through their templates, Fish integrations, lifecycle scripts, externals, prompt/data logic, and cross-tool consumers; update only affected claims.
- Full audit: use only when requested, earlier updates were missed, or drift is suspected; compare documentation with source in both directions.
- Preserve the document's structure, tone, and level of detail. Record relevant conditions; do not present implicit or environment-selected values as fixed.
- Verify local links and factual claims against source state.
