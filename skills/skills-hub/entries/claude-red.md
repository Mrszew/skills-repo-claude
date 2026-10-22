# claude-red

- **Link:** https://github.com/SnailSploit/claude-red
- **Kategoria:** Zbiór skilli (Claude) — bezpieczeństwo ofensywne / pentest
- **Autor:** SnailSploit (Kai Aizen), https://snailsploit.com
- **Licencja:** MIT
- **Popularność:** ~7.8k ⭐, ~100 skilli, aktywne (stan na 2026-10-22)
- **Sprawdzone:** 2026-10-22
- **Bezpieczeństwo:** ⚠️ Uważaj (dual-use ofensywny — tylko autoryzowane testy)

## Do czego to jest

Biblioteka plików `SKILL.md`, które „primują” Claude metodyką ofensywnego bezpieczeństwa dla
konkretnej powierzchni ataku: web (SQLi, XSS, SSRF, XXE, RCE, deserializacja...), Active Directory,
cloud, kontenery/k8s, exploit-dev, fuzzing, wireless, mobile, recon/OSINT, raportowanie i inne.
To wiedza/checklisty, nie gotowe narzędzia ani exploity.

## Jak użyć

Skille mieszczą się w katalogu `Skills/<kategoria>/<skill>/SKILL.md`.
`install.sh` tylko kopiuje pliki (bez pobierania kodu z sieci).

**Domyślnie instaluje globalnie (`~/.claude/skills/claude-red`) — tego unikamy.**
Instalować per projekt, wskazując katalog projektu i najlepiej jedną kategorię:

```bash
git clone https://github.com/SnailSploit/claude-red.git
cd claude-red
./install.sh --list                                   # lista kategorii
./install.sh --target ./.claude/skills --category web --dry-run
./install.sh --target ./.claude/skills --category web
```

## Bezpieczeństwo

- ✅ MIT, popularne, znany autor. `install.sh` to zwykłe kopiowanie plików — bez `curl|bash`,
  bez zdalnego wykonania, bez ukrytego unicode / prompt injection wymierzonego w agenta.
- ⚠️ **Treść dual-use ofensywna.** Używać tylko przy autoryzowanych testach: pisemna zgoda,
  ustalony zakres (scope), rules of engagement. Bez tego użycie technik może być nielegalne.
- ⚠️ **Domyślna instalacja jest globalna** — podawać `--target ./.claude/skills` w projekcie.
- ⚠️ Instaluje dużo skilli naraz (kontekst + ryzyko). Brać tylko potrzebną `--category`.
- ⚠️ Pliki zawierają przykładowe payloady z ciągami typu „ignore previous instructions” oraz
  `curl ... | bash` jako treść dydaktyczną — nie uruchamiać ich na ślepo; to przykłady do testów
  cudzych systemów, nie komendy do odpalenia u siebie.
- ℹ️ Repo nie ma audytu na skills.sh (nie jest tam publikowane).

## Notatki

- Dobre jako „ściąga” przy legalnym pentescie. Do defensywy/edukacji też OK.
- Przy realnym zleceniu trzymać zakres i logi; raportowanie ma osobny skill (`utility/offensive-reporting`).
