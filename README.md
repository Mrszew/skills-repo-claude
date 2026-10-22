# Skills Hub — moje zestawienie

Lista repozytoriów, skilli i narzędzi przydatnych przy pracy z Claude Code i agentami AI.
Każdy wpis: do czego służy, jak go użyć i **czy jest bezpieczny**.

Repo jest jednocześnie **pluginem Claude Code**. Każdy, kto ma dostęp do repo, może go zainstalować
i Claude będzie polecał narzędzia z tego katalogu, zawsze z oceną bezpieczeństwa i odnośnikiem do wpisu.

👉 Pełny katalog z detalami: [skills/skills-hub/CATALOG.md](skills/skills-hub/CATALOG.md)

## Skille w hubie

| Nazwa | Do czego | Ocena | Na co uważać / czemu nie safe |
|-------|----------|-------|-------------------------------|
| [find-skills](skills/skills-hub/entries/find-skills.md) | Szukanie i instalacja skilli z skills.sh (`npx skills find`) | ✅ Safe | Sam skill to czysty tekst. Ale proponuje instalację `-g -y` (globalnie, bez pytania) — nie zgadzać się na auto-instalację, każdy znaleziony skill najpierw zweryfikować. |
| [skills.sh API](skills/skills-hub/entries/skills-sh-api.md) | Katalog 600k+ skilli: szukanie, szczegóły, audyt bezpieczeństwa | ✅ Safe | Oficjalne API Vercela, tylko odczyt, token OIDC (bez stałego sekretu). To, że skill jest w katalogu, nie znaczy że jest bezpieczny — sprawdzać endpoint `audit`. |
| [claude-red](skills/skills-hub/entries/claude-red.md) | ~100 skilli metodyki pentestu (web, AD, cloud, exploit-dev, wireless...) | ⚠️ Uważaj | **Dual-use ofensywny** — legalne tylko przy autoryzowanych testach (zgoda + scope). Domyślnie instaluje **globalnie** (dawać `--target ./.claude/skills`). Zawiera przykładowe payloady (`curl\|bash`, „ignore previous instructions”) — nie odpalać na ślepo. |
| [MoneyPrinterTurbo](skills/skills-hub/entries/moneyprinterturbo.md) | Automatyczne short video z tematu (skrypt, footage, lektor, napisy) | ⚠️ Uważaj | **WebUI i API bez logowania** — nie wystawiać na sieć (każdy zużyje twoje klucze). Klucze API w `config.toml`. Paczka PyPI od osoby trzeciej (używać `mpt`). Tryb agenta pobiera instrukcje z sieci. Muzyka z YouTube = ryzyko praw autorskich. |

> **Co znaczy ⚠️ Uważaj:** narzędzie jest zasadniczo OK i da się używać, ale ma konkretne ryzyka
> (otwarte porty, klucze w plaintext, treść dual-use, zdalne instrukcje). Kolumna wyżej mówi, na co
> patrzeć. Pełne uzasadnienie oceny jest w sekcji „Bezpieczeństwo” w każdym wpisie (`entries/<nazwa>.md`).

## Instalacja

Wymaga [Claude Code](https://claude.com/claude-code). Repo jest publiczne, więc nie trzeba dostępu do konta.

**Opcja A: dla siebie, we wszystkich projektach**

```bash
claude plugin marketplace add Mrszew/skills-repo-claude
claude plugin install skills-hub@mrszew-hub --scope user
```

**Opcja B: dla całego zespołu w konkretnym projekcie.** Dodaj do `.claude/settings.json` w repo projektu
i zacommituj. Każdy, kto otworzy projekt w Claude Code, dostanie propozycję instalacji huba:

```json
{
  "extraKnownMarketplaces": {
    "mrszew-hub": {
      "source": { "source": "github", "repo": "Mrszew/skills-repo-claude" }
    }
  },
  "enabledPlugins": {
    "skills-hub@mrszew-hub": true
  }
}
```

**Aktualizacja** (po nowych wpisach w repo), potem restart Claude Code:

```bash
claude plugin marketplace update mrszew-hub
claude plugin update skills-hub@mrszew-hub
```

## Użycie

Zapytaj w dowolnym projekcie, np. *„czy mam coś do generowania wideo?”*, *„czy X jest safe?”*,
albo wywołaj `/skills-hub`. Claude odpowie w formacie:

> Z skills-hub: **MoneyPrinterTurbo** — generowanie short video z tematu. Ocena: ⚠️ Uważaj (WebUI bez autoryzacji, klucze w config.toml). Wpis: `entries/moneyprinterturbo.md`

Zasady huba (w [SKILL.md](skills/skills-hub/SKILL.md)):
- polecenia najpierw z katalogu, zawsze z oceną bezpieczeństwa i odnośnikiem do wpisu;
- to, czego nie ma w hubie, Claude oznacza jako **niesprawdzone**;
- narzędzia instaluje **tylko per projekt**, nigdy globalnie (chyba że wprost o to poprosisz);
- nic oznaczonego ⚠️/❌ bez potwierdzenia.

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
4. Podbij `version` w [.claude-plugin/plugin.json](.claude-plugin/plugin.json) (np. 0.1.1 → 0.1.2), inaczej
   zainstalowane kopie się nie odświeżą.
5. Push (właściciel) albo fork + Pull Request (pozostali).

Albo po prostu poproś Claude w dowolnym projekcie: *„dodaj X do skills hub”*.

## Checklista bezpieczeństwa (przed instalacją skilla / repo)

- [ ] Kto jest autorem? Znana organizacja / aktywny maintainer?
- [ ] Licencja (MIT/Apache = OK; brak licencji = uwaga)
- [ ] Aktywność repo (ostatni commit, issues, gwiazdki)
- [ ] Audyt na skills.sh: `GET /api/v1/skills/audit/{source}/{skill}` (Snyk, Socket — pass/warn/fail)
- [ ] Przeczytany `SKILL.md` i skrypty — brak `curl | sh`, pobierania zdalnych instrukcji, wysyłania danych na zewnątrz
- [ ] Jakie klucze API / sekrety wymaga i gdzie je trzyma
- [ ] Czy otwiera porty / serwer (WebUI, API) — bind tylko na `127.0.0.1`
- [ ] Prompt injection: czy skill każe agentowi pobierać i wykonywać treści z internetu
