# Raport o defekcie – szablon

> Na podstawie ISO/IEC/IEEE 29119-3 (raport o incydencie) i sylabusa ISTQB CTFL 4.0 (rozdz. 5.5).
> Zasada: inna osoba, korzystając wyłącznie z raportu, musi odtworzyć awarię.
> Jeden raport = jeden problem. Pisz rzeczowo, bez ocen („programista zepsuł…”).

| Pole | Wartość |
|---|---|
| **ID** | `DEF-<nr>` |
| **Tytuł** | `<gdzie + co się dzieje; krótko, np. „Kalkulator: opłata serwisowa objęta rabatem”>` |
| **Data zgłoszenia** | `<RRRR-MM-DD>` |
| **Zgłaszający** | `<imię i nazwisko>` |
| **Obiekt testów / wersja** | `<aplikacja, wersja/build, adres URL strony>` |
| **Środowisko** | `<system, przeglądarka i wersja, rozdzielczość, dane (konto)>` |
| **Powiązania** | `<ID przypadku testowego / pozycji listy kontrolnej / wymagania REQ-…>` |
| **Warunki wstępne** | `<stan systemu przed krokami, np. zalogowany jako marek, dane po resecie>` |
| **Kroki do odtworzenia** | 1. `<…>`<br>2. `<…>`<br>3. `<…>` |
| **Oczekiwany rezultat** | `<co powinno się stać – z odwołaniem do wymagania>` |
| **Rzeczywisty rezultat** | `<co się stało – dokładne komunikaty, wartości>` |
| **Powtarzalność** | `<zawsze / czasami (np. 3 na 10 prób) / jednorazowo>` |
| **Ważność (severity)** | `<krytyczna / wysoka / średnia / niska>` – wpływ na system i użytkownika |
| **Priorytet** | `<wysoki / średni / niski>` – pilność naprawy |
| **Status** | `Nowy` |
| **Załączniki** | `<DEF-nr.png – zrzut ekranu (Win+Shift+S), log z konsoli DevTools>` |
| **Uwagi** | `<obejście, obserwacje, hipotezy – oznaczone jako hipotezy>` |

## Lista kontrolna przed wysłaniem raportu

- [ ] Tytuł mówi *gdzie* i *co* – bez czytania reszty wiadomo, czego dotyczy.
- [ ] Awaria odtworzona co najmniej dwa razy (lub podana częstość).
- [ ] Kroki zaczynają się od stanu początkowego i są ponumerowane.
- [ ] Oczekiwany rezultat wynika z wymagania (podano jego ID) lub jasno opisanej wyroczni.
- [ ] Rzeczywisty rezultat zawiera dokładny tekst komunikatu / wartość.
- [ ] Dołączony zrzut ekranu z zaznaczonym problemem.
- [ ] Jeden problem w jednym raporcie; sprawdzono, czy nie jest duplikatem.
