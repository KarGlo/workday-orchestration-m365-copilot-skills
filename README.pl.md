# Skille Workday Orchestration i WDCLI dla Microsoft 365 Copilot

[English](README.md) · **Polski**

Skille i instrukcje dla **agenta Microsoft 365 Copilot** (Agent Builder), który pomaga
projektować, budować, przeglądać i debugować **orkiestracje Workday** (Orchestration Builder,
aplikacje Extend i integration apps) oraz korzystać z **Workday Developer CLI (`wdcli`)**.

Repozytorium zawiera **wyłącznie tekst** — pliki Markdown i `.txt`. Żadnych skryptów ani plików
wykonywalnych. Gotowe paczki `.zip` w zakładce Releases zawierają te same pliki tekstowe.

> Projekt nieoficjalny — niezwiązany z Workday, Inc. ani z Microsoft, nieautoryzowany ani
> niewspierany przez nie. „Workday” jest znakiem towarowym Workday, Inc.

## Co jest w środku

```
agent/
├── agent-profile.md                 nazwa, opis, startery rozmów, zalecane ustawienia
├── instructions-with-skills.md      instrukcje agenta, wariant A (5 163 z 8 000 znaków)
└── instructions-without-skills.md   instrukcje agenta, wariant B (5 235 z 8 000 znaków)
skills/
├── workday-orchestration-design/            szablony, wyzwalacze, konfiguracja w tenancie, limity, cykl życia, 13 przepisów
├── workday-orchestration-steps/             wszystkie komponenty, zakładki i dostępność; poświadczenia, retry, polling
├── workday-orchestration-expressions/       składnia wyrażeń + katalog wszystkich 926 udokumentowanych funkcji
├── workday-orchestration-errors-debugging/  handlery błędów, logowanie, debugger, logi, statusy, diagnostyka
├── workday-orchestration-review/            lista kontrolna review i czytanie wyeksportowanych plików .orchestration
└── workday-wdcli/                           instalacja wdcli, logowanie, komendy, proxy, CI, stare wcpcli
LICENSE · NOTICE.md · licenses/
```

Każdy folder skilla ma `SKILL.md` (instrukcje, poniżej limitu 20 000 znaków) i folder
`references/` z plikami `.txt`, które skill czyta wtedy, gdy ich potrzebuje.

## Konfiguracja przez kopiuj-wklej (bez pobierania)

Każdy plik poniżej skopiujesz jako tekst w przeglądarce — nic nie zapisuje się na komputerze.
Przy każdym pliku otwórz link **tekst** i skopiuj całość (**Ctrl+A**, **Ctrl+C**) albo otwórz
nazwę pliku i użyj przycisku **Copy raw file** (ikona dwóch kwadratów) nad jego treścią.
Lista służy do konfiguracji z sekcji „Wariant A, gdy Skills przyjmuje pliki `.md`” poniżej.

- **Instructions** i **Skills**: wklej prosto w Agent Builder, jeśli ma pole tekstowe. Jeśli
  Skills przyjmuje tylko plik, wklej tekst do Notatnika i zapisz jako `SKILL.md`, ustawiając
  **Zapisz jako typ: Wszystkie pliki** (inaczej Notatnik dopisze `.txt`); każdy skill w osobnym
  folderze.
- **Attachments**: wklej każdy plik do Notatnika i zapisz pod **dokładnie** podaną nazwą — skille
  szukają plików po nazwie.
- `functions-structured-data.txt` ma około 54 KB; po wklejeniu sprawdź, czy dotarła też końcówka
  pliku.

| # | Plik | Gdzie trafia | Tekst |
| --- | --- | --- | --- |
| 1 | [`instructions-with-skills.md`](agent/instructions-with-skills.md) | **Instructions** — wklej tekst | [tekst](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/agent/instructions-with-skills.md) |
| 2 | [`workday-orchestration-design / SKILL.md`](skills/workday-orchestration-design/SKILL.md) | **Skills > Add** — wklej albo zapisz jako `SKILL.md` i wgraj | [tekst](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-design/SKILL.md) |
| 3 | [`workday-orchestration-steps / SKILL.md`](skills/workday-orchestration-steps/SKILL.md) | **Skills > Add** — wklej albo zapisz jako `SKILL.md` i wgraj | [tekst](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-steps/SKILL.md) |
| 4 | [`workday-orchestration-expressions / SKILL.md`](skills/workday-orchestration-expressions/SKILL.md) | **Skills > Add** — wklej albo zapisz jako `SKILL.md` i wgraj | [tekst](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-expressions/SKILL.md) |
| 5 | [`workday-orchestration-errors-debugging / SKILL.md`](skills/workday-orchestration-errors-debugging/SKILL.md) | **Skills > Add** — wklej albo zapisz jako `SKILL.md` i wgraj | [tekst](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-errors-debugging/SKILL.md) |
| 6 | [`workday-orchestration-review / SKILL.md`](skills/workday-orchestration-review/SKILL.md) | **Skills > Add** — wklej albo zapisz jako `SKILL.md` i wgraj | [tekst](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-review/SKILL.md) |
| 7 | [`workday-wdcli / SKILL.md`](skills/workday-wdcli/SKILL.md) | **Skills > Add** — wklej albo zapisz jako `SKILL.md` i wgraj | [tekst](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-wdcli/SKILL.md) |
| 8 | [`platform.txt`](skills/workday-orchestration-design/references/platform.txt) | **Knowledge > Attachments** — zapisz pod dokładnie tą nazwą i wgraj | [tekst](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-design/references/platform.txt) |
| 9 | [`recipes.txt`](skills/workday-orchestration-design/references/recipes.txt) | **Knowledge > Attachments** — zapisz pod dokładnie tą nazwą i wgraj | [tekst](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-design/references/recipes.txt) |
| 10 | [`steps.txt`](skills/workday-orchestration-steps/references/steps.txt) | **Knowledge > Attachments** — zapisz pod dokładnie tą nazwą i wgraj | [tekst](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-steps/references/steps.txt) |
| 11 | [`settings.txt`](skills/workday-orchestration-steps/references/settings.txt) | **Knowledge > Attachments** — zapisz pod dokładnie tą nazwą i wgraj | [tekst](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-steps/references/settings.txt) |
| 12 | [`syntax.txt`](skills/workday-orchestration-expressions/references/syntax.txt) | **Knowledge > Attachments** — zapisz pod dokładnie tą nazwą i wgraj | [tekst](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-expressions/references/syntax.txt) |
| 13 | [`functions-global.txt`](skills/workday-orchestration-expressions/references/functions-global.txt) | **Knowledge > Attachments** — zapisz pod dokładnie tą nazwą i wgraj | [tekst](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-expressions/references/functions-global.txt) |
| 14 | [`functions-strings-text.txt`](skills/workday-orchestration-expressions/references/functions-strings-text.txt) | **Knowledge > Attachments** — zapisz pod dokładnie tą nazwą i wgraj | [tekst](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-expressions/references/functions-strings-text.txt) |
| 15 | [`functions-structured-data.txt`](skills/workday-orchestration-expressions/references/functions-structured-data.txt) | **Knowledge > Attachments** — zapisz pod dokładnie tą nazwą i wgraj | [tekst](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-expressions/references/functions-structured-data.txt) |
| 16 | [`functions-numbers-dates-collections.txt`](skills/workday-orchestration-expressions/references/functions-numbers-dates-collections.txt) | **Knowledge > Attachments** — zapisz pod dokładnie tą nazwą i wgraj | [tekst](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-expressions/references/functions-numbers-dates-collections.txt) |
| 17 | [`errors-debugging.txt`](skills/workday-orchestration-errors-debugging/references/errors-debugging.txt) | **Knowledge > Attachments** — zapisz pod dokładnie tą nazwą i wgraj | [tekst](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-errors-debugging/references/errors-debugging.txt) |
| 18 | [`review.txt`](skills/workday-orchestration-review/references/review.txt) | **Knowledge > Attachments** — zapisz pod dokładnie tą nazwą i wgraj | [tekst](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-orchestration-review/references/review.txt) |
| 19 | [`wdcli.txt`](skills/workday-wdcli/references/wdcli.txt) | **Knowledge > Attachments** — zapisz pod dokładnie tą nazwą i wgraj | [tekst](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/skills/workday-wdcli/references/wdcli.txt) |
| 20 | [`agent-profile.md`](agent/agent-profile.md) | Name, Description, Starter prompts — przepisz | [tekst](https://raw.githubusercontent.com/KarGlo/workday-orchestration-m365-copilot-skills/main/agent/agent-profile.md) |

## Wybór wariantu

| | Wariant A — custom skills | Wariant B — pliki wiedzy |
| --- | --- | --- |
| Wymaga | licencji Microsoft 365 Copilot (lub pay-as-you-go) i organizacji w **Microsoft Frontier Program**; niedostępne przy Purview Information Barriers | licencji Microsoft 365 Copilot |
| Wgrywasz | 6 paczek `.zip` | 12 plików `.txt` |
| Instrukcje | `agent/instructions-with-skills.md` | `agent/instructions-without-skills.md` |
| Jakość | lepsza: szczegółowe procedury ładują się tylko wtedy, gdy są potrzebne | dobra: procedury skrócone w instrukcjach |
| Limity | 8 skilli na agenta, 50 MB na `.zip`, 25 MB na plik, 350 plików, głębokość 3 | 20 wgranych plików na agenta |

Custom skills to funkcja w wersji preview, a agent nie może jeszcze łączyć skilli z wgranymi
plikami — w jednym agencie wybierz jeden wariant.

## Konfiguracja wariantu A (skille)

1. **Pobierz paczki.** Ściągnij sześć plików `.zip` z najnowszego [release](../../releases).
   Albo zbuduj je sam: otwórz folder skilla, zaznacz **jego zawartość** (`SKILL.md` i
   `references`) i skompresuj (Windows: prawy przycisk > **Kompresuj do pliku ZIP** / **Wyślij
   do > Folder skompresowany (zip)**). `SKILL.md` musi leżeć w korzeniu archiwum — nie pakuj
   samego folderu. Na macOS Finder potrafi dodać ukryty folder `__MACOSX`; tam lepiej użyć paczek
   z release.
2. W Microsoft 365 Copilot (<https://m365.cloud.microsoft>) wybierz **Agents & Skills** >
   **New agent**, potem **Skip to configure**.
3. **Name** i **Description**: skopiuj z `agent/agent-profile.md`.
4. **Instructions**: wklej całe `agent/instructions-with-skills.md`.
5. **Skills** > **Add**: wgraj każdy `.zip` i przejrzyj nazwę, opis, instrukcje i pliki.
6. **Starter prompts**: dodaj sześć z `agent/agent-profile.md`.
7. Opcjonalnie **Knowledge**: publiczna strona `https://developer.workday.com/documentation`.
8. **Try it**: przetestuj startery, potem utwórz i udostępnij agenta.

## Wariant A, gdy Skills przyjmuje pliki `.md`

Niektóre wersje Agent Builder przyjmują w **Skills > Add** pojedynczy plik Markdown zamiast
`.zip`. Wtedy:

1. Pobierz `upload-files.zip` z najnowszego [release](../../releases) i rozpakuj. Zawiera
   `skills/<nazwa-skilla>/SKILL.md` (6 plików) i `knowledge/` (12 plików `.txt` z referencjami).
2. **New agent** > **Skip to configure**; Name i Description z `agent/agent-profile.md`.
3. **Instructions**: wklej `agent/instructions-with-skills.md`.
4. **Skills** > **Add**: wgraj kolejno sześć plików `SKILL.md`.
5. **Knowledge** > **Attachments**: wgraj wszystkie 12 plików z `knowledge/` — skille szukają ich
   tam po nazwie pliku.
6. Dodaj startery i przetestuj w **Try it**, np. „Które funkcje wyciągają wartość z odpowiedzi
   JSON?” — odpowiedź powinna cytować sygnatury z `functions-structured-data.txt`.

Microsoft wymienia „agentów ze skillami i wgranymi plikami jednocześnie” jako znane ograniczenie
wersji preview. Jeśli agent nie chce się zapisać albo ignoruje załączniki, wrzuć 12 plików `.txt`
do folderu w OneDrive lub SharePoint i dodaj go przez **Add knowledge**, albo użyj wariantu B.

## Konfiguracja wariantu B (pliki wiedzy)

1. Pobierz repozytorium (**Code > Download ZIP**) i rozpakuj.
2. **New agent** > **Skip to configure**; Name i Description z `agent/agent-profile.md`.
3. **Instructions**: wklej `agent/instructions-without-skills.md`.
4. **Knowledge** > wgraj te 12 plików z `skills/*/references/`:
   `platform.txt`, `recipes.txt`, `steps.txt`, `settings.txt`, `syntax.txt`,
   `functions-global.txt`, `functions-strings-text.txt`, `functions-structured-data.txt`,
   `functions-numbers-dates-collections.txt`, `errors-debugging.txt`, `review.txt`, `wdcli.txt`.
5. Włącz **Only use specified sources**.
6. Dodaj startery i przetestuj w **Try it**.

Microsoft traktuje wgraną wiedzę jako dane referencyjne, a nie instrukcje, dlatego w wariancie B
wszystkie zasady zachowania są w instrukcjach, a pliki zawierają fakty.

## Jak powstała treść

Skille napisano na podstawie dokumentacji deweloperskiej Workday (336 stron z sekcji Integration
Apps, Orchestrations, Expression Language i CLI, stan na 2026-10-02) i sprawdzono względem 163
prawdziwych plików orkiestracji z repozytorium
[WorkdayDeveloperProgram](https://github.com/Workday/WorkdayDeveloperProgram). Katalog funkcji
wygenerowano z tabel referencyjnych dokumentacji (926 funkcji); dwie funkcje pomocnicze używane w
przykładach Workdaya, a nieobecne w referencji (`chars.space()`, `chars.newline()`), są wypisane
osobno i oznaczone jako niezweryfikowane. Tam, gdzie dokumentacja Workdaya sama sobie przeczy (np. `wdcli auth login`
kontra `wdcli auth:login`), skille mówią to wprost, zamiast po cichu wybierać jedną wersję.

## Aktualizacja

Przy nowym wydaniu Workdaya sprawdź z dokumentacją: limity
(`workday-orchestration-design/references/platform.txt`), komponenty
(`workday-orchestration-steps/references/steps.txt`), funkcje
(`workday-orchestration-expressions/references/functions-*.txt`) i komendy
(`workday-wdcli/references/wdcli.txt`). Po zmianie skilla zbuduj ponownie jego `.zip`.

## Licencja

[Apache License 2.0](LICENSE). Źródła zewnętrzne i ich licencje: [NOTICE.md](NOTICE.md).
