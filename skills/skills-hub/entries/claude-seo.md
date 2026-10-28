# claude-seo

- **Link:** https://github.com/AgriciDaniel/claude-seo
- **Kategoria:** Plugin Claude Code — SEO
- **Autor:** AgriciDaniel, https://claude-seo.md
- **Licencja:** MIT
- **Popularność:** ~22.9k ⭐, GitHub Trending, aktywne (stan na 2026-10-28)
- **Sprawdzone:** 2026-10-28
- **Bezpieczeństwo:** ✅ Safe (z uwagami poniżej)

## Do czego to jest

Darmowy plugin SEO do Claude Code. Dajesz adres strony, a on robi pełny audyt SEO (10–15 min)
i zwraca plan działania posortowany wg ważności. 26 pod-skilli + 19 pod-agentów: technical SEO,
Core Web Vitals, schema, E-E-A-T, GEO/AEO (cytowalność w AI search), backlinki, local/e-commerce SEO,
hreflang, raporty PDF/Excel. 9 opcjonalnych rozszerzeń na żywe dane SEO.

## Jak użyć

To plugin marketplace (jak nasz hub). Instalacja per projekt:

```bash
claude plugin marketplace add AgriciDaniel/claude-seo
claude plugin install claude-seo@claude-seo --scope project
```

Rdzeń działa bez żadnych kluczy API. Rozszerzenia (Ahrefs, DataForSEO, Firecrawl, Bing, Matomo...)
instaluje się osobno (`extensions/<nazwa>/install.sh`) i wymagają własnych kluczy.

## Bezpieczeństwo

- ✅ MIT, bardzo popularne, aktywnie rozwijane, autor dba o bezpieczeństwo
  (`plugin.json` wspomina utwardzone fetchery SSRF / DNS-rebinding).
- ⚠️ **Instaluje hook `PostToolUse`** uruchamiający skrypt Pythona (`validate-schema.py`) przy
  **każdym Edit/Write** w projekcie. To tylko walidacja schematu w obrębie pluginu, ale wiedz, że
  kod odpala się automatycznie po edycjach plików.
- ⚠️ **Rozszerzenia** mają własne `install.sh` / `install.ps1` i konfigurują serwery MCP oraz
  **płatne API** (Ahrefs, DataForSEO, Firecrawl itd.). Instalować tylko te, których potrzebujesz;
  przejrzeć skrypt przed uruchomieniem; klucze trzymać w zmiennych środowiskowych, nie w repo.
- ⚠️ Audyt SEO wysyła zapytania do zewnętrznych stron/usług — używać na stronach, do których masz prawo.
- ℹ️ Rdzeń pluginu nie wymaga kluczy i nie robi `curl|bash`.

## Notatki

- Mocne do audytu własnych/klienckich stron. Rozszerzenia bierz wybiórczo.
