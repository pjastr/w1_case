# Specyfikacja wymagań – serwis BiletTO (bilety na koncerty)

| | |
|---|---|
| Dokument | Specyfikacja wymagań funkcjonalnych i ogólnych (podstawa testów) |
| Przedmiot testów | BiletTO 1.0 – serwis internetowy sprzedaży biletów na koncerty, PHP 8.2 + MySQL/MariaDB (XAMPP) |
| Adres | `http://localhost/biletto/` (strona główna `index.php`) |
| Wersja dokumentu | 1.0 (ćwiczenia 1 – case „serwis biletowy”) |

Każde wymaganie ma unikalny identyfikator (`REQ-<obszar>-<nr>`), do którego odwołujemy się
w przypadkach testowych, macierzy śledzenia i raportach defektów.
Obszary: **UI** – wymagania ogólne, **REJ** – rejestracja, **LOG** – logowanie i blokada konta,
**CEN** – kalkulator ceny biletów, **ZAM** – repertuar i zamówienia biletów, **KON** – formularz kontaktowy.

Słowo „musi” oznacza wymaganie obowiązkowe. Teksty komunikatów podane w cudzysłowie
„…” są wymagane dosłownie (łącznie z kropką na końcu).

---

## 1. Wymagania ogólne (UI)

Wymagania REQ-UI-01 – REQ-UI-07 dotyczą stron serwisu dostępnych z menu (Start, Repertuar,
Rejestracja, Logowanie, Kalkulator, Moje bilety, Kontakt, Administracja); nie dotyczą technicznej
strony instalacji `install.php`.

| ID | Wymaganie |
|---|---|
| REQ-UI-01 | Każda strona zawiera menu z odnośnikami: Start, Repertuar, Rejestracja, Kalkulator, Moje bilety, Kontakt, Administracja oraz – dla użytkownika niezalogowanego – Logowanie. Dla zalogowanego zamiast „Logowanie” wyświetlany jest napis „Zalogowano: &lt;login&gt;” i odnośnik „Wyloguj”. |
| REQ-UI-02 | Każda strona ma niepusty, opisowy tytuł (element `<title>`) w postaci „BiletTO – &lt;nazwa strony&gt;”, np. „BiletTO – repertuar”. |
| REQ-UI-03 | Każdy obrazek (w tym plakaty koncertów) ma niepusty tekst alternatywny (atrybut `alt`). |
| REQ-UI-04 | Każde widoczne pole formularza ma etykietę powiązaną z polem (`<label for="…">`). |
| REQ-UI-05 | Pole adresu e-mail w każdym formularzu ma typ `email`. |
| REQ-UI-06 | Komunikaty o wyniku operacji zakończonej przekierowaniem (logowanie, wylogowanie, operacje na zamówieniach, odblokowanie konta) są wyświetlane w wyróżnionym bloku komunikatu: zielonym (powodzenie) lub czerwonym (błąd). Komunikat znika po odświeżeniu strony. |
| REQ-UI-07 | Serwis działa w języku polskim; polskie znaki są wyświetlane poprawnie (UTF-8). Stopka każdej strony zawiera numer wersji serwisu. |
| REQ-UI-08 | Wszystkie dane wejściowe są sprawdzane po stronie serwera (niezależnie od walidacji w przeglądarce). |
| REQ-UI-09 | Otwarcie adresu `install.php?reset=1` (lub odnośnika „Przywróć dane początkowe” w panelu administracyjnym) przywraca dane początkowe (Załącznik A) i wylogowuje użytkownika. Strona instalacji wyświetla status „OK”. |

## 2. Rejestracja konta (REJ) – strona „Rejestracja”

| ID | Wymaganie |
|---|---|
| REQ-REJ-01 | Formularz rejestracji zawiera pola: Login, E-mail, Telefon (opcjonalnie), Wiek, Hasło, Powtórz hasło, pole wyboru „Akceptuję regulamin” oraz przycisk „Załóż konto”. |
| REQ-REJ-02 | Login musi mieć od 4 do 16 znaków, zaczynać się od małej litery łacińskiej i składać się wyłącznie z małych liter łacińskich a–z, cyfr 0–9 i znaku podkreślenia `_`. W przeciwnym razie komunikat: „Login musi mieć od 4 do 16 znaków, zaczynać się od litery i zawierać tylko małe litery, cyfry lub _.” |
| REQ-REJ-03 | Login musi być unikalny. Jeśli konto o takim loginie istnieje, komunikat: „Login jest już zajęty.” |
| REQ-REJ-04 | E-mail musi być poprawnym adresem e-mail. W przeciwnym razie komunikat: „Niepoprawny adres e-mail.” |
| REQ-REJ-05 | Telefon jest opcjonalny (na ten numer wysyłane są SMS-y z biletami). Jeśli pole nie jest puste, musi zawierać dokładnie 9 cyfr (bez spacji i innych znaków). W przeciwnym razie komunikat: „Numer telefonu musi składać się z 9 cyfr.” |
| REQ-REJ-06 | Wiek musi być liczbą całkowitą z zakresu 16–99 (włącznie). W przeciwnym razie komunikat: „Wiek musi być liczbą całkowitą z zakresu 16–99.” |
| REQ-REJ-07 | Hasło musi mieć od 8 do 24 znaków (włącznie) i zawierać co najmniej jedną literę oraz co najmniej jedną cyfrę. W przeciwnym razie komunikat: „Hasło musi mieć od 8 do 24 znaków i zawierać literę oraz cyfrę.” |
| REQ-REJ-08 | Pole „Powtórz hasło” musi być identyczne z polem „Hasło”. W przeciwnym razie komunikat: „Hasła nie są identyczne.” |
| REQ-REJ-09 | Regulamin musi zostać zaakceptowany. W przeciwnym razie komunikat: „Musisz zaakceptować regulamin.” |
| REQ-REJ-10 | Po wysłaniu formularza z błędami wyświetlana jest lista **wszystkich** błędów (po jednym komunikacie dla każdego błędnego pola), konto nie jest tworzone, a pola Login, E-mail, Telefon i Wiek zachowują wpisane wartości. |
| REQ-REJ-11 | Po wysłaniu poprawnego formularza tworzone jest aktywne konto (status ACTIVE, 0 nieudanych prób logowania), wyświetlany jest komunikat „Konto zostało utworzone. Możesz się zalogować.”, a formularz jest czyszczony. Nowy użytkownik może się od razu zalogować. |

## 3. Logowanie i blokada konta (LOG) – strony „Logowanie” i „Administracja”

| ID | Wymaganie |
|---|---|
| REQ-LOG-01 | Formularz logowania zawiera pola Login i Hasło oraz przycisk „Zaloguj”. |
| REQ-LOG-02 | Poprawny login i hasło dla konta aktywnego (ACTIVE) powodują zalogowanie, przejście na stronę główną i komunikat „Zalogowano jako &lt;login&gt;.” Licznik nieudanych prób logowania tego konta jest zerowany. |
| REQ-LOG-03 | Błędne hasło dla konta aktywnego zwiększa licznik nieudanych prób o 1 i wyświetla komunikat „Błędny login lub hasło. Pozostało prób: N.”, gdzie N = 3 − liczba kolejnych nieudanych prób. |
| REQ-LOG-04 | Trzecia kolejna nieudana próba (bez poprawnego logowania pomiędzy nimi) blokuje konto (status LOCKED) i wyświetla komunikat „Konto zostało zablokowane po 3 nieudanych próbach.” |
| REQ-LOG-05 | Na konto zablokowane nie można się zalogować, także poprawnym hasłem. Wyświetlany jest komunikat „Konto jest zablokowane. Skontaktuj się z obsługą BiletTO.” |
| REQ-LOG-06 | Próba logowania na nieistniejący login wyświetla komunikat „Błędny login lub hasło.” (bez informacji o liczbie prób). |
| REQ-LOG-07 | Odnośnik „Wyloguj” kończy sesję, przenosi na stronę główną i wyświetla komunikat „Wylogowano.” |
| REQ-LOG-08 | Panel „Administracja” wyświetla tabelę użytkowników z kolumnami: Login, E-mail, Telefon, Wiek, Nieudane próby, Status (ACTIVE lub LOCKED). (Uproszczenie aplikacji szkoleniowej: panel nie wymaga logowania.) |
| REQ-LOG-09 | Dla konta zablokowanego (i tylko dla niego) panel wyświetla przycisk „Odblokuj”. Jego użycie zmienia status na ACTIVE, zeruje licznik nieudanych prób i wyświetla komunikat „Odblokowano konto &lt;login&gt;.” |

## 4. Kalkulator ceny biletów (CEN) – strona „Kalkulator”

Kalkulator wylicza cenę biletów na koncerty halowe ze sprzedażą sektorową (cennik sektorów –
Załącznik A). Kalkulator nie tworzy zamówienia i nie wymaga logowania.

| ID | Wymaganie |
|---|---|
| REQ-CEN-01 | Formularz zawiera: wybór sektora (Płyta – domyślnie, Trybuna, Balkon), pole „Liczba biletów” (domyślnie 1), pole wyboru „Mam kartę Klubu Fana”, pole „Kod promocyjny”, wybór sposobu dostawy biletów (E-bilet – domyślnie, Odbiór w kasie, Kurier) oraz przycisk „Oblicz”. Po obliczeniu wprowadzone dane pozostają w formularzu. |
| REQ-CEN-02 | Liczba biletów to liczba całkowita z zakresu 1–6 (limit biletów w jednym zamówieniu). Dla innej wartości wyświetlany jest komunikat „Liczba biletów musi być liczbą całkowitą z zakresu 1–6.” i wynik nie jest obliczany. |
| REQ-CEN-03 | Rabat: 15%, gdy klient ma kartę Klubu Fana **i** podał poprawny kod promocyjny; 10%, gdy spełniony jest tylko jeden z tych warunków; 0%, gdy żaden. Rabaty nie sumują się. |
| REQ-CEN-04 | Poprawny kod promocyjny to „FAN2026”; wielkość liter nie ma znaczenia, a spacje na początku i końcu są pomijane. Gdy podano niepusty, niepoprawny kod, wyświetlany jest komunikat „Nieprawidłowy kod promocyjny – został pominięty.”, a rabat liczony jest tak, jakby kodu nie podano. |
| REQ-CEN-05 | Dostawa jest bezpłatna, gdy klient ma kartę Klubu Fana **lub** wartość biletów (przed rabatem) wynosi co najmniej 500,00 zł. |
| REQ-CEN-06 | Koszt płatnej dostawy: E-bilet 0,00 zł, Odbiór w kasie 5,00 zł, Kurier 20,00 zł. |
| REQ-CEN-07 | Kwota do zapłaty = wartość biletów × (100 − rabat) / 100 (zaokrąglona do pełnego grosza) + opłata serwisowa + koszt dostawy. Opłata serwisowa wynosi 2,00 zł za każdy bilet i nie podlega rabatowi. |
| REQ-CEN-08 | Wynik zawiera: wartość biletów, rabat w procentach (np. „15%”), opłatę serwisową, koszt dostawy i kwotę do zapłaty w formacie „429.00 zł” (dwa miejsca po kropce). Przykład: Płyta, 2 bilety, karta Klubu Fana, kod „fan2026”, Kurier → wartość biletów 500.00 zł, rabat 15%, opłata serwisowa 4.00 zł, dostawa 0.00 zł, do zapłaty 429.00 zł. |

## 5. Repertuar i zamówienia biletów (ZAM) – strony „Repertuar” i „Moje bilety”

| ID | Wymaganie |
|---|---|
| REQ-ZAM-01 | Strona „Repertuar” jest dostępna bez logowania i wyświetla tabelę koncertów z kolumnami: Koncert, Data, Miejsce, Cena biletu (np. „189.00 zł”), Wolne miejsca, Status sprzedaży. Status sprzedaży: „Sprzedaż zakończona”, gdy data koncertu jest wcześniejsza niż bieżąca data; w przeciwnym razie „Wyprzedane”, gdy liczba wolnych miejsc wynosi 0; w pozostałych przypadkach „W sprzedaży”. |
| REQ-ZAM-02 | Strona „Moje bilety” jest dostępna tylko dla zalogowanych. Niezalogowany użytkownik jest przenoszony na stronę logowania z komunikatem „Zaloguj się, aby zobaczyć swoje bilety.” |
| REQ-ZAM-03 | Strona „Moje bilety” wyświetla tabelę **własnych** zamówień użytkownika z kolumnami: Nr, Koncert, Liczba biletów, Kwota (np. „378.00 zł”), Status (Zarezerwowane, Opłacone, Wydane, Wykorzystane, Anulowane, Zwrócone), Akcje. |
| REQ-ZAM-04 | Zalogowany użytkownik może zarezerwować bilety, wybierając koncert z listy i podając liczbę biletów (liczba całkowita 1–6). Zamówienie otrzymuje status „Zarezerwowane”, kwotę = cena biletu × liczba biletów, liczba wolnych miejsc koncertu zmniejsza się o liczbę biletów, a wyświetlany jest komunikat „Utworzono zamówienie #&lt;nr&gt;.” Komunikaty błędów: dla liczby spoza zakresu – „Liczba biletów musi być liczbą całkowitą z zakresu 1–6.”; gdy liczba biletów przekracza liczbę wolnych miejsc – „Brak wystarczającej liczby wolnych miejsc (dostępne: N).”; dla koncertu o statusie innym niż „W sprzedaży” – „Sprzedaż biletów na ten koncert jest niedostępna.” |
| REQ-ZAM-05 | Dozwolone są wyłącznie przejścia: Zarezerwowane –opłać→ Opłacone; Zarezerwowane –anuluj→ Anulowane; Opłacone –wydaj bilety→ Wydane; Opłacone –zwróć→ Zwrócone; Wydane –zwróć→ Zwrócone; Wydane –wykorzystaj→ Wykorzystane. Stany Wykorzystane, Anulowane i Zwrócone są końcowe. Anulowanie i zwrot zwiększają liczbę wolnych miejsc koncertu o liczbę biletów z zamówienia. |
| REQ-ZAM-06 | Przy każdym zamówieniu wyświetlane są przyciski wyłącznie tych akcji, które są dozwolone w jego bieżącym stanie („Opłać”, „Wydaj bilety”, „Wykorzystaj”, „Zwróć”, „Anuluj”). Zamówienia w stanie końcowym nie mają przycisków. |
| REQ-ZAM-07 | Po wykonaniu dozwolonej akcji status zmienia się zgodnie z REQ-ZAM-05 i wyświetlany jest komunikat „Zamówienie #&lt;nr&gt;: &lt;stary status&gt; → &lt;nowy status&gt;.”, np. „Zamówienie #1: Zarezerwowane → Opłacone.” Każda zmiana jest zapisywana w historii zamówienia. |
| REQ-ZAM-08 | Próba wykonania niedozwolonej akcji (np. przez bezpośrednie wywołanie adresu `akcja.php?id=4&akcja=zwroc`) nie zmienia statusu i wyświetla komunikat „Niedozwolone przejście: &lt;status&gt; → &lt;akcja&gt;.”, np. „Niedozwolone przejście: Wykorzystane → zwroc.” |
| REQ-ZAM-09 | Próba wykonania akcji na zamówieniu nieistniejącym lub należącym do innego użytkownika wyświetla komunikat „Nie znaleziono zamówienia.” i niczego nie zmienia. |

## 6. Formularz kontaktowy (KON) – strona „Kontakt”

| ID | Wymaganie |
|---|---|
| REQ-KON-01 | Formularz zawiera pola: Imię (maks. 60 znaków), E-mail (maks. 120 znaków), Nr zamówienia (opcjonalnie), Wiadomość oraz przycisk „Wyślij”. Strona spełnia wymagania REQ-UI-02 – REQ-UI-05. |
| REQ-KON-02 | Imię nie może być puste – w przeciwnym razie komunikat „Podaj imię.” |
| REQ-KON-03 | E-mail musi być poprawnym adresem – w przeciwnym razie komunikat „Niepoprawny adres e-mail.” |
| REQ-KON-04 | Nr zamówienia, jeśli podany, musi być dodatnią liczbą całkowitą – w przeciwnym razie komunikat „Numer zamówienia musi być dodatnią liczbą całkowitą.” |
| REQ-KON-05 | Wiadomość nie może być pusta – w przeciwnym razie komunikat „Wpisz treść wiadomości.” |
| REQ-KON-06 | Po wysłaniu poprawnego formularza wiadomość jest zapisywana i wyświetlany jest komunikat „Dziękujemy za wiadomość. Odpowiemy w ciągu 2 dni roboczych.” |

---

## Załącznik A. Dane początkowe (po `install.php?reset=1`)

**Konta użytkowników**

| Login | Hasło | E-mail | Telefon | Wiek | Status | Nieudane próby |
|---|---|---|---|---|---|---|
| marek | Koncert123 | marek@example.com | 600100200 | 30 | ACTIVE | 0 |
| ewa | Bilety456 | ewa@example.com | (brak) | 22 | ACTIVE | 0 |
| zablokowany | Koncert123 | zb@example.com | (brak) | 41 | LOCKED | 3 |

**Repertuar** (koncerty i wykonawcy są fikcyjni)

| Id | Koncert | Data | Miejsce | Cena biletu | Wolne miejsca |
|---|---|---|---|---|---|
| K1 | Rockowa Noc – Echo Północy | 2026-11-21 | Hala Nova, Wrocław | 189.00 zł | 120 |
| K2 | Jazz pod Gwiazdami – Trio Lumen | 2026-12-05 | Klub Akustyk, Kraków | 120.00 zł | 2 |
| K3 | Elektroniczny Świt | 2026-11-07 | Arena Port, Gdańsk | 150.00 zł | 0 |
| K4 | Symfonicznie o zmierzchu | 2026-09-20 | Filharmonia Nadmorska, Gdynia | 95.00 zł | 40 |

**Zamówienia**

| Nr | Właściciel | Koncert | Liczba biletów | Kwota | Status |
|---|---|---|---|---|---|
| 1 | marek | K1 | 2 | 378.00 zł | Zarezerwowane |
| 2 | marek | K1 | 1 | 189.00 zł | Opłacone |
| 3 | marek | K2 | 2 | 240.00 zł | Wydane |
| 4 | marek | K4 | 2 | 190.00 zł | Wykorzystane |
| 5 | marek | K1 | 4 | 756.00 zł | Anulowane |
| 6 | marek | K3 | 1 | 150.00 zł | Zwrócone |
| 7 | ewa | K1 | 2 | 378.00 zł | Zarezerwowane |

**Cennik sektorów (kalkulator ceny biletów)**

| Sektor | Cena biletu |
|---|---|
| Płyta | 250,00 zł |
| Trybuna | 199,99 zł |
| Balkon | 99,99 zł |

## Załącznik B. Słownik

- **Konto aktywne / zablokowane** – status konta ACTIVE / LOCKED widoczny w panelu administracyjnym.
- **Kolejne nieudane próby** – nieudane próby logowania na to samo konto, między którymi nie było poprawnego logowania ani odblokowania konta.
- **Wartość biletów** – cena biletu w wybranym sektorze × liczba biletów, przed naliczeniem rabatu, opłaty serwisowej i kosztu dostawy.
- **Klub Fana** – program lojalnościowy BiletTO; posiadanie karty klient deklaruje w kalkulatorze polem wyboru.
- **Opłata serwisowa** – stała opłata doliczana do każdego biletu (2,00 zł), niezależna od rabatu.
