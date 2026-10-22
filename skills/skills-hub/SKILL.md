---
name: skills-hub
description: Curated hub of vetted skills, repos, APIs and tools, each with what it is for, how to use it, and a safety rating (Safe / Careful / Unsafe). Use when the user asks for a tool, skill, repo or API for a task (e.g. video generation, finding skills), asks "what do I have for X", "is X safe", wants to add a new entry to the hub, or before installing or recommending any third-party skill/repo.
---

# Skills Hub

Curated catalog of tools and skills. Source of truth: `CATALOG.md` in this skill's directory,
with one detailed file per tool in `entries/`.

## Rules

1. **Recommend from the hub first.** Before suggesting any skill/repo/tool, check `CATALOG.md`.
2. **Always cite the hub and the rating** when suggesting something from it, in this form:

   > Z skills-hub: **<Nazwa>** — <do czego>. Ocena: <✅/⚠️/❌> <uwagi>. Wpis: `entries/<plik>.md`

   If nothing in the hub fits and you suggest something outside it, say explicitly that it is
   **not in the hub and not vetted**, and offer to vet and add it.
3. **Never install globally** (`-g`, `--scope user`, `~/.claude/skills`, `~/.agents/skills`).
   Install per project only (e.g. `npx skills add <src> --skill <name>` without `-g`, run in the
   project root; `claude plugin install ... --scope project`). Global only if the user explicitly asks.
4. Never install or run anything rated ⚠️/❌ without the user's confirmation after showing the caveats.

## Looking something up

1. Read `CATALOG.md` (table: name, category, purpose, safety, entry file).
2. Open the matching `entries/<name>.md` for usage and safety details.
3. Answer using the citation format from rule 2.

## Adding or vetting a new entry

The installed copy of this plugin is a read-only cache. Edit the hub repo instead:
https://github.com/Mrszew/skills-repo-claude. Owner pushes directly; anyone else forks and opens a PR.

To vet a candidate:

1. Gather facts: author, license, stars, last activity (`gh api repos/<owner>/<repo>`), README.
2. For skills listed on skills.sh, check the audit endpoint
   (`GET https://skills.sh/api/v1/skills/audit/{source}/{skill}`, see `entries/skills-sh-api.md`).
3. Read the `SKILL.md` / scripts. Red flags: `curl | sh`, fetching remote instructions at runtime,
   sending data to external hosts, unauthenticated servers bound to `0.0.0.0`, secrets in plain config.
4. Copy `entries/_TEMPLATE.md` to `entries/<name>.md`, fill it in, add a row to `CATALOG.md`.
   Entries are written in Polish. Install commands in entries must be per-project, not global.
5. Ratings: ✅ Safe, ⚠️ Uważaj (usable with caveats), ❌ Unsafe (sandbox only), ❔ Niesprawdzone.
6. Bump `version` in `.claude-plugin/plugin.json` (patch), commit, push. Installed copies refresh with
   `claude plugin marketplace update mrszew-hub && claude plugin update skills-hub@mrszew-hub`
   (restart Claude Code after).
