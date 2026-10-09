# Plan testów – BiletTO, moduły Rejestracja i Kalkulator ceny biletów (rozwiązanie wzorcowe)

| | |
|---|---|
| Identyfikator planu | PT-BiletTO-01 |
| Wersja / data | 1.0 / 2026-10-09 |
| Autor | Zespół TO (rozwiązanie wzorcowe dla prowadzącego) |
| Status | do przeglądu |

## 1. Kontekst testowania

### 1.1 Przedmiot testów
BiletTO 1.0 – serwis sprzedaży biletów na koncerty (PHP 8.2 + MariaDB, XAMPP), `http://localhost/biletto/` –
strony `rejestracja.php` i `kalkulator.php`. Dodatkowo (ćw. 1): strony ćwiczeniowe the-internet – `/login`
(lista kontrolna) oraz strony do sesji eksploracyjnej.

### 1.2 Zakres testów
- **W zakresie:** rejestracja konta (REQ-REJ-01 – 11), kalkulator ceny biletów (REQ-CEN-01 – 08);
  testy funkcjonalne czarnoskrzynkowe.
- **Poza zakresem (w tym planie):** logowanie i blokada (LOG), repertuar i zamówienia biletów (ZAM),
  kontakt (KON) – kolejne iteracje; testy wydajnościowe (np. szczyt sprzedaży po otwarciu przedsprzedaży)
  i bezpieczeństwa (brak wymagań i czasu); płatności online (serwis ich nie obsługuje – akcja „Opłać”
  jest symulowana); zgodność z wieloma przeglądarkami (tylko Chrome).

### 1.3 Podstawa testów
`specyfikacja_BiletTO.md` v1.0 (identyfikatory REQ-…); dane początkowe i cennik sektorów – Załącznik A
specyfikacji.

### 1.4 Założenia i ograniczenia
- Ćw. 1: 180 min, praca w parach; aplikacja BiletTO nie jest uruchomiona – przypadki testowe są tylko
  projektowane, wykonanie po udostępnieniu środowiska.
- Brak dostępu do kodu źródłowego – testowanie czarnoskrzynkowe.
- Wykonanie ręczne (automatyzacja na późniejszych zajęciach).
- Ceny sektorów są stałe (Załącznik A) – oczekiwane kwoty liczone są dla tego cennika; zmiana cennika
  wymaga przeliczenia oczekiwanych rezultatów.

### 1.5 Interesariusze
Prowadzący (w roli operatora serwisu biletowego i właściciela produktu), zespół testowy (para studentów).

## 2. Komunikacja
Po sesji: raport z wykonania (arkusz „Raport z wykonania”). Defekty – arkusz „Raporty defektów”
(jeden wiersz = jeden raport, zrzuty ekranu `DEF-nr.png`). Niejasności w wymaganiach – lista
pytań do właściciela produktu (sekcja w raporcie z wykonania).

## 3. Rejestr ryzyk

| ID | Ryzyko | P (1–3) | W (1–3) | P×W | Działanie ograniczające |
|---|---|---|---|---|---|
| R1 | (produktowe) Błędne obliczenie kwoty do zapłaty (rabat, opłata serwisowa, dostawa) – strata finansowa klienta lub organizatora, reklamacje | 2 | 3 | 6 | Tablica decyzyjna dla rabatu (karta × kod), AWB progu 500,00 zł i liczby biletów 1/6, przypadki zaokrągleń |
| R2 | (produktowe) Zakup biletów ponad limit 6 sztuk – wykup puli przez pośredników („koniki”) | 2 | 3 | 6 | AWB liczby biletów 0/1/6/7, EP dla wartości niecałkowitych i nieliczbowych |
| R3 | (produktowe) Rejestracja konta z niepoprawnymi danymi (np. osoba poniżej 16 lat, błędny telefon – bilet SMS nie dotrze) | 2 | 2 | 4 | AWB wieku 15/16/99/100 i długości telefonu 8/9/10, EP dla formatu loginu i hasła |
| R4 | (produktowe) Użytkownik nie może założyć konta mimo poprawnych danych – utrata sprzedaży | 1 | 3 | 3 | Przypadki dla poprawnych wartości brzegowych (login 4 i 16 znaków, hasło 8 i 24, wiek 16 i 99, telefon pusty) |
| R5 | (projektowe) Środowisko BiletTO niedostępne na ćw. 1 | 3 | 2 | 6 | Na ćw. 1 tylko projektowanie; wykonanie po udostępnieniu środowiska |
| R6 | (projektowe) Niejednoznaczne wymagania (np. metoda zaokrąglania) | 2 | 2 | 4 | Przegląd specyfikacji (test statyczny) na początku zajęć, pytania do właściciela produktu |

## 4. Strategia testów

### 4.1 Poziomy i typy testów
Testy systemowe; funkcjonalne; czarnoskrzynkowe; ręczne. Dodatkowo test statyczny
(przegląd specyfikacji) i testowanie oparte na doświadczeniu (lista kontrolna, sesja eksploracyjna).

### 4.2 Techniki projektowania testów
Podział na klasy równoważności (EP), analiza wartości brzegowych (AWB), tablica decyzyjna (rabat:
karta Klubu Fana × kod promocyjny), zgadywanie błędów (zaokrąglenia, wiele błędów naraz), lista
kontrolna (strona `/login`), testowanie eksploracyjne (sesja 30 min, karta sesji).

### 4.3 Kryteria wejścia
Specyfikacja v1.0 dostępna i przejrzana; do wykonania: BiletTO uruchomiona w XAMPP,
`install.php?reset=1` zwraca „OK”.

### 4.4 Kryteria wyjścia (ukończenia)
- Każde wymaganie REQ-REJ i REQ-CEN pokryte ≥ 1 przypadkiem testowym (macierz śledzenia),
- 100% przypadków o priorytecie Wysoki wykonanych, ≥ 90% wszystkich,
- brak otwartych defektów o ważności Krytyczna i Wysoka (lub decyzja właściciela produktu).

### 4.5 Kryteria zawieszenia i wznowienia
Zawieszenie: aplikacja niedostępna, błąd bazy danych, defekt blokujący > 30% przypadków.
Wznowienie: po naprawie i pozytywnym teście dymnym (strona główna, rejestracja poprawnymi danymi,
obliczenie w kalkulatorze dla wartości domyślnych).

### 4.6 Dane testowe i środowisko
Windows 11, Chrome (aktualna wersja), XAMPP portable; dane początkowe po `install.php?reset=1`
(konta marek, ewa, zablokowany; cennik sektorów Płyta 250,00 / Trybuna 199,99 / Balkon 99,99 zł).
Przed każdym przypadkiem rejestracji – reset danych lub unikalny login.

### 4.7 Retesty i testy regresji
Po naprawie defektu: retest przypadku, który go wykrył, oraz przypadków dla tego samego wymagania;
po każdej zmianie reguł cenowych – ponowne wykonanie wszystkich TC-CEN.

### 4.8 Metryki
Liczba przypadków zaprojektowanych / wykonanych / zaliczonych; defekty wg ważności i statusu;
procent wymagań pokrytych przypadkami.

### 4.9 Produkty testowania
Plan testów (ten dokument), arkusz `Dokumentacja_testowa_rozwiazanie.xlsx` (przypadki testowe,
macierz śledzenia, raporty defektów, lista kontrolna, raport z wykonania), zrzuty ekranu.

## 5. Działania testowe i harmonogram (ćw. 1)

| Działanie | Kto | Czas | Produkt |
|---|---|---|---|
| Przegląd specyfikacji, lista niejasności | para | 25 min | lista pytań |
| Warunki testowe, plan testów | para | 25 min | plan testów |
| Projektowanie przypadków + macierz | para | 45 min | arkusz: przypadki, macierz |
| Sesja eksploracyjna + raporty defektów | każdy osobno | 35 min | raporty defektów |
| Lista kontrolna /login – przygotowanie i wykonanie | para | 20 min | lista kontrolna |
| Raport z wykonania | para | 10 min | raport |

## 6. Role i odpowiedzialności
Student A – rejestracja (przypadki, macierz), student B – kalkulator ceny biletów; obaj – sesja
eksploracyjna (osobne strony), wspólnie – lista kontrolna i raport. Zatwierdza: prowadzący.

## 7. Zatwierdzenie

| Rola | Imię i nazwisko | Data | Podpis |
|---|---|---|---|
| Autor | Zespół TO | 2026-10-09 | |
| Zatwierdzający | prowadzący | | |
