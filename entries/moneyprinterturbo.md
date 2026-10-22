# MoneyPrinterTurbo

- **Link:** https://github.com/harry0703/MoneyPrinterTurbo ([README EN](https://github.com/harry0703/MoneyPrinterTurbo/blob/main/README-en.md))
- **Kategoria:** Narzędzie — generowanie short video AI
- **Licencja:** MIT
- **Popularność:** ~134k ⭐, aktywnie rozwijane (stan na 2026-10-22)
- **Sprawdzone:** 2026-10-22
- **Bezpieczeństwo:** ⚠️ Uważaj

## Do czego to jest

Generator krótkich filmów „all-in-one”: podajesz temat/słowo kluczowe, a narzędzie samo pisze skrypt (LLM),
dobiera footage, nagrywa lektora (TTS), dodaje napisy i muzykę, renderuje wideo.

- Interfejsy: WebUI, REST API, CLI (batch), workflow dla agenta AI (Skill document)
- LLM: wielu dostawców, bramki OpenAI-compatible, lokalnie Ollama
- Footage: własne pliki, Pexels, Pixabay, Coverr, generatory AI (Seedance, MiniMax, MuAPI)
- Audio: Edge TTS (bez klucza), inne TTS, napisy przez Whisper
- Formaty: 9:16, 16:9, 1:1; publikacja na TikTok / Instagram / YouTube Shorts

## Jak użyć

Wymagania: Python 3.11+, min. 4 rdzenie / 4 GB RAM (GPU opcjonalnie).

```bash
# Docker (WebUI :8501, API :8080)
git clone https://github.com/harry0703/MoneyPrinterTurbo.git
cd MoneyPrinterTurbo
docker compose -f docker-compose.release.yml up

# albo pip (oficjalna paczka to "mpt"!)
pip install mpt
```

Klucze API (LLM, Pexels/Pixabay itd.) wpisuje się w WebUI → Basic Settings / `config.toml`.

## Bezpieczeństwo

- ✅ Popularne repo, licencja MIT, otwarty kod.
- ⚠️ **Brak autoryzacji w WebUI/API** — nie wystawiać na sieć (`MPT_WEBUI_HOST=0.0.0.0`) ani na publiczny serwer. Każdy z dostępem zużywa Twoje klucze API.
- ⚠️ Klucze API trzymane w `config.toml` — nie commitować, uważać przy eksporcie ustawień (eksport zawiera klucze).
- ⚠️ CORS ≠ kontrola dostępu (curl/Postman go omijają).
- ⚠️ **Paczka PyPI `MoneyPrinterTurbo` jest od osoby trzeciej** — instalować `mpt` albo z repo.
- ⚠️ Workflow „AI Agent” każe agentowi pobrać Skill document z raw GitHub i wykonywać komendy — przeczytać go przed użyciem (ryzyko prompt injection, jeśli plik się zmieni).
- ⚠️ Domyślna muzyka w tle pochodzi z YouTube — możliwe problemy z prawami autorskimi przy publikacji.
- ℹ️ README zawiera dużo linków sponsorowanych/afiliacyjnych — nie wpływa na działanie.

## Notatki

- Najbezpieczniej: Docker lokalnie, porty tylko na `127.0.0.1`, osobne klucze API z limitami wydatków.
