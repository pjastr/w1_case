# Plan testów – szablon (skrócony, wg ISO/IEC/IEEE 29119-3)

> Wypełnij pola w nawiasach `<…>`. Plan skrócony – na ćwiczeniach wystarczy 1–2 zdania lub krótka lista w każdym punkcie.
> Usuń komentarze w cudzysłowie blokowym przed oddaniem.

| | |
|---|---|
| Identyfikator planu | `<PT-BiletTO-01>` |
| Wersja / data | `<1.0 / RRRR-MM-DD>` |
| Autor | `<imię i nazwisko, nr albumu>` |
| Status | `<szkic / do przeglądu / zatwierdzony>` |

## 1. Kontekst testowania

### 1.1 Przedmiot testów (elementy testowe)
`<nazwa aplikacji i wersja, adres, moduły objęte testami>`

### 1.2 Zakres testów
- **W zakresie:** `<np. rejestracja (REQ-REJ-…), kalkulator ceny biletów (REQ-CEN-…)>`
- **Poza zakresem:** `<np. wydajność (szczyt sprzedaży biletów), bezpieczeństwo płatności, moduł zamówień – z uzasadnieniem>`

### 1.3 Podstawa testów
`<dokumenty, z których wyprowadzamy testy, np. specyfikacja_BiletTO.md v1.0>`

### 1.4 Założenia i ograniczenia
`<np. czas: 1 zajęcia; aplikacja BiletTO niedostępna – testy tylko projektujemy; brak dostępu do kodu>`

### 1.5 Interesariusze
`<kto korzysta z wyników testów: prowadzący (klient – operator serwisu biletowego), zespół, właściciel produktu>`

## 2. Komunikacja
`<jak i komu raportujemy: raport z wykonania po sesji, raporty defektów w arkuszu, …>`

## 3. Rejestr ryzyk

| ID | Ryzyko (produktowe / projektowe) | Prawdopodobieństwo (1–3) | Wpływ (1–3) | Poziom (P×W) | Działanie ograniczające |
|---|---|---|---|---|---|
| R1 | `<…>` | | | | |
| R2 | `<…>` | | | | |

## 4. Strategia testów

### 4.1 Poziomy i typy testów
`<np. testy systemowe, funkcjonalne, czarnoskrzynkowe; manualne na tym etapie>`

### 4.2 Techniki projektowania testów
`<np. podział na klasy równoważności, analiza wartości brzegowych, lista kontrolna, testowanie eksploracyjne>`

### 4.3 Kryteria wejścia
`<kiedy możemy zacząć wykonywać testy, np. dostępne środowisko, zatwierdzona specyfikacja>`

### 4.4 Kryteria wyjścia (ukończenia)
`<np. 100% przypadków o priorytecie Wysoki wykonanych, każde wymaganie pokryte ≥1 przypadkiem, brak otwartych defektów krytycznych>`

### 4.5 Kryteria zawieszenia i wznowienia
`<np. zawieszenie, gdy strona nie działa / blokujący defekt; wznowienie po naprawie>`

### 4.6 Dane testowe i środowisko
`<przeglądarka, system, konta testowe (marek, ewa, zablokowany), reset danych>`

### 4.7 Retesty i testy regresji
`<kiedy i co powtarzamy po naprawie defektu>`

### 4.8 Metryki
`<np. liczba wykonanych / zaliczonych przypadków, liczba defektów wg ważności, pokrycie wymagań>`

### 4.9 Produkty testowania (testalia)
`<np. plan testów, arkusz przypadków, macierz śledzenia, raporty defektów, lista kontrolna, raport z wykonania>`

## 5. Działania testowe i harmonogram

| Działanie | Kto | Termin / czas | Produkt |
|---|---|---|---|
| `<analiza specyfikacji>` | | | |
| `<projektowanie przypadków>` | | | |
| `<wykonanie / sesja eksploracyjna>` | | | |
| `<raportowanie>` | | | |

## 6. Role i odpowiedzialności
`<kto planuje, projektuje, wykonuje, zatwierdza>`

## 7. Zatwierdzenie

| Rola | Imię i nazwisko | Data | Podpis |
|---|---|---|---|
| Autor | | | |
| Zatwierdzający | | | |
