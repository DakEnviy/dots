---
name: update-dots-template
description: "Synchronize reusable framework changes from the primary chezmoi source-state repository into the minimal dots-template repository. Use after primary-repository changes, when template drift is suspected, or when asked to compare, audit, refresh, or update dots-template."
---

# Update Dots Template

Resolve the primary repository as the Git root containing this skill. Resolve the template repository from the user's request or current workspace context; if it is ambiguous, ask for its path before comparing or editing. Keep the template aligned with reusable framework improvements without copying personal configuration.

1. Default to a targeted audit: trace relevant primary-repository changes and history through the template's tracked files. Compare tracked paths only; never include `.git`. Run a full bidirectional audit only when requested or when drift is suspected.
2. Classify every difference before editing:
   - Port generic bootstrap, package-selection, binary/path detection, platform, external, prompt/data, and validation fixes.
   - Adapt examples, placeholders, the minimal app registry, and README instructions to the template's public contract.
   - Exclude personal apps and values, app-specific configs, images, `CONFIGS.md`, `TODO.md`, `AGENTS.md`, and `.agents/` unless explicitly requested.
3. Edit only the template by default; treat the primary repository as read-only. Never bulk-copy `apps.yaml` or whole directories. Preserve `<YOUR_NAME>`, `<YOUR_REPO_URL>`, and the minimal app registry.
4. Update the template README only when a transferred change alters its user-visible schema, setup, or extension contract.
5. Validate transferred behavior with isolated or synthetic data and cover empty install/configure branches when relevant. Avoid full primary-template renders; isolate the safe core or validate through the minimal template. Inspect the complete template diff and both repositories' final status.
6. Report what was ported, adapted, and intentionally excluded.
