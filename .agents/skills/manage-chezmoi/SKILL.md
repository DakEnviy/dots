---
name: manage-chezmoi
description: "Work safely with chezmoi source-state repositories: managed files, Go templates, special files, lifecycle scripts, externals, package/bootstrap logic, diagnostics, validation, and command behavior. Use for chezmoi changes or questions. Consult current official documentation for semantic, unfamiliar, safety-sensitive, or version-dependent behavior. Do not use for unrelated dotfile repositories."
---

# Manage chezmoi

1. Read every applicable `AGENTS.md` and inspect nearby repository patterns.
2. Distinguish source, target, and destination state before proposing or making a change.
3. Research chezmoi semantics when they affect the result.
4. Edit source state only and validate without mutating destination or host state unless explicitly authorized.
5. Report the result, checks, relevant documentation, and the repository-defined manual apply sequence.

## Research documentation

Read [references/docs-map.md](references/docs-map.md) when the request involves command behavior, source-state attributes, templates, special files, hooks, scripts, externals, application order, safety, or version-dependent behavior. Skip research only for mechanical edits whose correctness does not depend on chezmoi semantics.

- Search and open the relevant page on `chezmoi.io`; do not rely on search snippets.
- For CLI behavior, compare the current documentation with `chezmoi --version` and `chezmoi help <command>`.
- If versions differ, inspect official release history, the matching tag, or `twpayne/chezmoi` source and state the qualification.
- Use third-party sources only when primary sources are insufficient. Separate documented facts from local-code inferences and cite supporting pages next to the claims.

## Work safely

- Resolve source filenames through all chezmoi attributes and `.tmpl` before reasoning about target paths.
- Confirm documented semantics before changing lifecycle prefixes, application order, hooks, or external refresh behavior.
- Treat dry-run as protection from destination writes, not from hooks, prompts, secret-manager access, externals, or commands evaluated while reading source state.
- Render templates before language-specific linting and check all affected platform and configuration branches.
- Preserve the repository's distinction between fresh bootstrap and reconfiguration of an existing machine; use its documented workflow rather than inventing one.

Follow the repository's authorization boundary and validation commands. Never expose secrets, decrypted values, or generated host-specific state.
