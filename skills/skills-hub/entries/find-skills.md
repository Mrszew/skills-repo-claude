# find-skills

- **Link:** https://skills.sh/vercel-labs/skills/find-skills ([repo](https://github.com/vercel-labs/skills))
- **Kategoria:** Skill (Claude Code + inne agenty)
- **Autor:** Vercel Labs
- **Licencja:** MIT
- **Popularność:** ~36k ⭐ (stan na 2026-10-22)
- **Sprawdzone:** 2026-10-22
- **Bezpieczeństwo:** ✅ Safe

## Do czego to jest

Skill, który uczy agenta szukać i instalować inne skille z ekosystemu skills.sh.
Odpala się przy pytaniach typu „jak zrobić X”, „czy jest skill do X”. Szuka przez
`npx skills find <query>`, ocenia jakość (liczba instalacji, źródło, gwiazdki) i proponuje komendę instalacji.

## Jak użyć

```bash
# instalacja globalna (wszystkie projekty)
npx skills add https://github.com/vercel-labs/skills --skill find-skills -g -y
```

Ląduje w `~/.agents/skills/find-skills`, a dla Claude Code jest symlink w `~/.claude/skills/find-skills`.
Zainstalowane u mnie globalnie 2026-10-22.

Przydatne komendy CLI:

```bash
npx skills find <query> [--owner <owner>]   # szukanie
npx skills add <owner/repo@skill>           # instalacja
npx skills update                           # aktualizacja zainstalowanych
```

## Bezpieczeństwo

Audyt skills.sh (2026-09):

| Audytor | Wynik |
|---------|-------|
| Gen Agent Trust Hub | ✅ pass (SAFE) |
| Socket | ✅ pass, brak alertów |
| Snyk | ⚠️ warn: MEDIUM, 1 issue |
| Runlayer | ✅ pass |
| ZeroLeaks | ✅ pass (93/100) |

- Sam skill to tylko `SKILL.md` (tekst), bez skryptów.
- ⚠️ Ryzyko jest w tym, co skill instaluje: w kroku 6 proponuje `npx skills add ... -g -y`
  (globalnie i bez potwierdzenia). Instalowane skille działają z pełnymi uprawnieniami agenta.
  **Nie pozwalać na auto-instalację.** Każdy znaleziony skill najpierw sprawdzić checklistą z README
  i dodać do huba.
- Jego kryteria jakości (1K+ instalacji, znane źródło, 100+ ⭐) to nie to samo co audyt bezpieczeństwa.

## Notatki

- Dobrze działa razem ze `skills-hub`: find-skills znajduje kandydata, skills-hub go sprawdza i zapisuje.
