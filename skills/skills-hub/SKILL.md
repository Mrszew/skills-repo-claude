---
name: skills-hub
description: Marcel's personal catalog of vetted skills, repos, APIs and tools, each with what it is for, how to use it, and a safety rating (Safe / Careful / Unsafe). Use when the user asks for a tool, skill, repo or API for a task (e.g. video generation, finding skills), asks "what do I have for X", "is X safe", wants to add a new entry to the hub, or before installing a third-party skill/repo.
---

# Skills Hub

Personal catalog of tools and skills. Source of truth: `CATALOG.md` in this skill's directory,
with one detailed file per tool in `entries/`.

## Looking something up

1. Read `CATALOG.md` (table: name, category, purpose, safety, entry file).
2. Open the matching `entries/<name>.md` for usage and safety details.
3. Always surface the safety rating and its caveats (⚠️ notes) to the user before recommending
   install or use. Never install or run anything from an ⚠️/❌ entry without the user's confirmation.

## Adding or vetting a new entry

The installed copy of this plugin is a read-only cache. Edit the hub repo instead:
`https://github.com/Mrszew/skills-repo-claude` (local clone, if present:
`~/Desktop/skill:repo/skills-repo-claude`). After pushing, the user runs
`claude plugin marketplace update mrszew-hub` to refresh.

To vet a candidate:

1. Gather facts: author, license, stars, last activity (`gh api repos/<owner>/<repo>`), README.
2. For skills listed on skills.sh, check the audit endpoint
   (`GET https://skills.sh/api/v1/skills/audit/{source}/{skill}`, see `entries/skills-sh-api.md`).
3. Read the `SKILL.md` / scripts. Red flags: `curl | sh`, fetching remote instructions at runtime,
   sending data to external hosts, unauthenticated servers bound to `0.0.0.0`, secrets in plain config.
4. Copy `entries/_TEMPLATE.md` to `entries/<name>.md`, fill it in, add a row to `CATALOG.md`.
   Entries are written in Polish.
5. Ratings: ✅ Safe, ⚠️ Uważaj (usable with caveats), ❌ Unsafe (sandbox only), ❔ Niesprawdzone.
