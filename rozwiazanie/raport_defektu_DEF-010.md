# Raport o defekcie DEF-010 (BiletTO – przykład z symulowanego wykonania testów)

> Wyniki fikcyjne – aplikacja BiletTO nie istnieje. Przykład pokazuje defekt ponownie otwarty po niepełnej poprawce.

| Pole | Wartość |
|---|---|
| **ID** | DEF-010 |
| **Tytuł** | Kalkulator: dostawa płatna przy wartości biletów równej progowi 500,00 zł |
| **Data zgłoszenia** | 2026-10-13 (aktualizacja 2026-10-15) |
| **Zgłaszający** | B. Wiśniewska |
| **Obiekt testów / wersja** | BiletTO 1.0.0-rc1 (build 2026-10-12), retest na 1.0.0-rc2 (build 2026-10-15); `http://localhost/biletto/kalkulator.php` |
| **Środowisko** | Windows 11 Pro 24H2, Google Chrome 141 (64-bit), 1920×1080; XAMPP 8.2.12; dane po `install.php?reset=1` |
| **Powiązania** | TC-CEN-008, TC-CEN-009; REQ-CEN-05, REQ-CEN-07 |
| **Warunki wstępne** | Otwarta strona Kalkulator (logowanie niewymagane) |
| **Kroki do odtworzenia** | 1. Wybierz sektor „Płyta”, liczba biletów 2; pole „Mam kartę Klubu Fana” niezaznaczone.<br>2. Wpisz kod „FAN2026”, wybierz dostawę „Kurier”.<br>3. Kliknij „Oblicz”. |
| **Oczekiwany rezultat** | Wartość biletów 500.00 zł, rabat 10%, opłata serwisowa 4.00 zł, dostawa **0.00 zł**, do zapłaty **454.00 zł** – próg darmowej dostawy liczony od wartości biletów przed rabatem (REQ-CEN-05, słownik: „wartość biletów”). |
| **Rzeczywisty rezultat** | rc1 i rc2: dostawa **20.00 zł**, do zapłaty **474.00 zł**.<br>W rc1 błąd występował także bez kodu (Płyta × 2, Kurier: dostawa 20.00 zł, do zapłaty 524.00 zł zamiast 504.00 zł) – w rc2 ten wariant działa poprawnie. |
| **Powtarzalność** | zawsze (3/3 próby na rc1, 3/3 na rc2) |
| **Ważność (severity)** | wysoka – klient płaci 20,00 zł więcej, niż wynika z regulaminu promocji |
| **Priorytet** | wysoki – reguła widoczna w materiałach marketingowych („darmowa dostawa od 500 zł”) |
| **Status** | Ponownie otwarty |
| **Załączniki** | `DEF-010-rc1.png` (Płyta × 2 bez kodu, rc1), `DEF-010-rc2.png` (Płyta × 2 z kodem, rc2) |
| **Uwagi** | Historia: Nowy (13.10) → Otwarty → Naprawiony w rc2 („zmieniono > na >=”) → Do retestu → **Ponownie otwarty** (15.10). Hipoteza: próg porównywany z kwotą po rabacie (450,00 zł < 500,00 zł) – poprawka usunęła tylko jedną z dwóch przyczyn. Po kolejnej naprawie wykonać regresję wszystkich TC-CEN. |
