# Skills Hub — moje zestawienie

Lista repozytoriów, skilli i narzędzi przydatnych przy pracy z Claude Code i agentami AI.
Każdy wpis: do czego służy, jak go użyć i **czy jest bezpieczny**.

Repo jest jednocześnie **pluginem Claude Code** — po instalacji skill `skills-hub` jest dostępny
w każdym projekcie, więc Claude zna ten katalog wszędzie.

👉 **Katalog: [skills/skills-hub/CATALOG.md](skills/skills-hub/CATALOG.md)**

## Instalacja (raz na komputer, działa we wszystkich projektach)

```bash
claude plugin marketplace add Mrszew/skills-repo-claude
claude plugin install skills-hub@mrszew-hub --scope user
```

Aktualizacja po pushu nowych wpisów:

```bash
claude plugin marketplace update mrszew-hub
```

Użycie w dowolnym projekcie: zapytaj np. *„czy mam coś do generowania wideo?”*, *„czy X jest safe?”*,
albo wywołaj `/skills-hub`.

Tylko dla jednego projektu (zamiast user scope) — w danym repo:

```bash
claude plugin install skills-hub@mrszew-hub --scope project
```

## Struktura

```
.claude-plugin/
  marketplace.json      # marketplace "mrszew-hub"
  plugin.json           # plugin "skills-hub"
skills/skills-hub/
  SKILL.md              # instrukcje dla Claude
  CATALOG.md            # tabela wszystkich wpisów
  entries/              # szczegóły per narzędzie (+ _TEMPLATE.md)
```

## Legenda bezpieczeństwa

| Ocena | Znaczenie |
|-------|-----------|
| ✅ Safe | Zaufane źródło, brak niepokojących uprawnień, można używać bez większych obaw |
| ⚠️ Uważaj | Zasadniczo OK, ale ma ryzyka (klucze API, otwarte porty, zdalne instrukcje) — czytaj uwagi |
| ❌ Unsafe | Nie używać / tylko w izolowanym środowisku (VM, sandbox) |
| ❔ Niesprawdzone | Jeszcze nie zweryfikowane |

## Jak dodać nowy wpis

1. Skopiuj [skills/skills-hub/entries/_TEMPLATE.md](skills/skills-hub/entries/_TEMPLATE.md) do `entries/<nazwa>.md`.
2. Uzupełnij opis i sekcję bezpieczeństwa (checklista poniżej).
3. Dodaj wiersz do [CATALOG.md](skills/skills-hub/CATALOG.md).
4. Push → `claude plugin marketplace update mrszew-hub`.

Albo po prostu poproś Claude w dowolnym projekcie: *„dodaj X do mojego skills hub”*.

## Checklista bezpieczeństwa (przed instalacją skilla / repo)

- [ ] Kto jest autorem? Znana organizacja / aktywny maintainer?
- [ ] Licencja (MIT/Apache = OK; brak licencji = uwaga)
- [ ] Aktywność repo (ostatni commit, issues, gwiazdki)
- [ ] Audyt na skills.sh: `GET /api/v1/skills/audit/{source}/{skill}` (Snyk, Socket — pass/warn/fail)
- [ ] Przeczytany `SKILL.md` i skrypty — brak `curl | sh`, pobierania zdalnych instrukcji, wysyłania danych na zewnątrz
- [ ] Jakie klucze API / sekrety wymaga i gdzie je trzyma
- [ ] Czy otwiera porty / serwer (WebUI, API) — bind tylko na `127.0.0.1`
- [ ] Prompt injection: czy skill każe agentowi pobierać i wykonywać treści z internetu
