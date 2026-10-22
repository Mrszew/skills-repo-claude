# skills.sh API

- **Link:** https://skills.sh/docs/api (ogłoszenie: Vercel changelog, 5 cze 2026)
- **Kategoria:** API / katalog skilli
- **Autor:** Vercel (skills.sh)
- **Sprawdzone:** 2026-10-22
- **Bezpieczeństwo:** ✅ Safe

## Do czego to jest

Publiczne API katalogu skills.sh — ponad 600 000 skilli z ekosystemu open source.
Wyszukiwanie skilli, szczegóły (liczba instalacji, hash, pliki) oraz **wyniki audytu bezpieczeństwa**
(Snyk, Socket: pass / warn / fail). Idealne do weryfikacji skilli przed dodaniem ich do tego zestawienia.

## Endpointy

Base URL: `https://skills.sh/api/v1`

| Endpoint | Opis |
|----------|------|
| `GET /skills` | Ranking (`all-time`, `trending`, `hot`), filtr `source`, paginacja `page`, `per_page` (max 500) |
| `GET /skills/search?q=...` | Wyszukiwanie (min. 2 znaki), `limit` (max 200), `owner` |
| `GET /skills/curated` | Oficjalne skille first-party |
| `GET /skills/{source}/{skill}` | Szczegóły skilla + zawartość plików |
| `GET /skills/audit/{source}/{skill}` | Audyt bezpieczeństwa |

Błędy: `400`, `401` (brak/zły token), `404`, `429` (rate limit, nagłówek `Retry-After`), `503`.

## Autoryzacja

Token **Vercel OIDC** projektu — bez rejestracji i bez stałego klucza API.
Token krótkotrwały (rotacja ~12 h), przypisany do teamu i projektu.
Limit: **600 req/min na team + projekt** (nagłówki `X-RateLimit-*`).

1. Projekt na Vercelu → Settings → OIDC Federation (włączyć).
2. Lokalnie: `vercel link` → `vercel env pull` (daje `VERCEL_OIDC_TOKEN` w `.env.local`).

## Jak użyć

```ts
import { getVercelOidcToken } from '@vercel/oidc';

const token = await getVercelOidcToken();
const res = await fetch('https://skills.sh/api/v1/skills?per_page=10', {
  headers: { Authorization: `Bearer ${token}` },
});
```

```bash
# wyszukiwanie
curl "https://skills.sh/api/v1/skills/search?q=react%20native&owner=expo&limit=5" \
  -H "Authorization: Bearer $VERCEL_OIDC_TOKEN"

# audyt skilla przed instalacją
curl "https://skills.sh/api/v1/skills/audit/vercel-labs/skills/find-skills" \
  -H "Authorization: Bearer $VERCEL_OIDC_TOKEN"
```

## Bezpieczeństwo

- Oficjalne API Vercela, tylko odczyt.
- Brak długożyjącego sekretu — token OIDC rotowany automatycznie. Nie commitować `.env.local`.
- Uwaga: to że skill jest w katalogu ≠ że jest bezpieczny. Zawsze sprawdzić endpoint `audit` i przeczytać `SKILL.md`.

## Notatki

- Wymaga projektu na Vercelu (OIDC). Do szybkiego testu wystarczy pusty projekt + `vercel env pull`.
