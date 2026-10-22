# Skills Repo — moje zestawienie

Lista repozytoriów, skilli i narzędzi przydatnych przy pracy z Claude Code i agentami AI.
Każdy wpis: do czego służy, jak go użyć i **czy jest bezpieczny**.

## Legenda bezpieczeństwa

| Ocena | Znaczenie |
|-------|-----------|
| ✅ Safe | Zaufane źródło, brak niepokojących uprawnień, można używać bez większych obaw |
| ⚠️ Uważaj | Zasadniczo OK, ale ma ryzyka (klucze API, otwarte porty, zdalne instrukcje) — czytaj uwagi |
| ❌ Unsafe | Nie używać / tylko w izolowanym środowisku (VM, sandbox) |
| ❔ Niesprawdzone | Jeszcze nie zweryfikowane |

## Zestawienie

| Nazwa | Kategoria | Do czego | Bezpieczeństwo | Szczegóły |
|-------|-----------|----------|----------------|-----------|
| [skills.sh API](https://skills.sh/docs/api) | API / katalog skilli | Wyszukiwanie 600k+ skilli, szczegóły, audyt bezpieczeństwa | ✅ Safe | [entries/skills-sh-api.md](entries/skills-sh-api.md) |
| [MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) | Generowanie wideo | Automatyczne short video z tematu (skrypt, footage, lektor, napisy) | ⚠️ Uważaj | [entries/moneyprinterturbo.md](entries/moneyprinterturbo.md) |

## Jak dodać nowy wpis

1. Skopiuj [entries/_TEMPLATE.md](entries/_TEMPLATE.md) do `entries/<nazwa>.md`.
2. Uzupełnij opis i sekcję bezpieczeństwa (checklista poniżej).
3. Dodaj wiersz do tabeli **Zestawienie** powyżej.

## Checklista bezpieczeństwa (przed instalacją skilla / repo)

- [ ] Kto jest autorem? Znana organizacja / aktywny maintainer?
- [ ] Licencja (MIT/Apache = OK; brak licencji = uwaga)
- [ ] Aktywność repo (ostatni commit, issues, gwiazdki)
- [ ] Audyt na skills.sh: `GET /api/v1/skills/audit/{source}/{skill}` (Snyk, Socket — pass/warn/fail)
- [ ] Przeczytany `SKILL.md` i skrypty — brak `curl | sh`, pobierania zdalnych instrukcji, wysyłania danych na zewnątrz
- [ ] Jakie klucze API / sekrety wymaga i gdzie je trzyma
- [ ] Czy otwiera porty / serwer (WebUI, API) — bind tylko na `127.0.0.1`
- [ ] Prompt injection: czy skill każe agentowi pobierać i wykonywać treści z internetu
