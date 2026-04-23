# Diagramy przepływu danych (DFD)

## Założenia do dekompozycji

Dla systemu wspomagającego proces rekrutacji w firmie HR dobrane zostały trzy główne procesy o zbliżonej złożoności:

1. `Obsługa ofert i aplikacji`
2. `Selekcja kandydatów`
3. `Obsługa rozmów i decyzji klienta`

Taki podział jest zgodny z wcześniejszą specyfikacją wymagań i pozwala wykonać czytelną dekompozycję do poziomu 2 bez mieszania procesów bardzo prostych z bardzo złożonymi.

## Pliki z diagramami

- [DFD poziom 1](C:/Users/filip/Desktop/masi/dfd_poziom_1.puml)
- [DFD poziom 2 - proces 1](C:/Users/filip/Desktop/masi/dfd_poziom_2_proces_1.puml)
- [DFD poziom 2 - proces 2](C:/Users/filip/Desktop/masi/dfd_poziom_2_proces_2.puml)
- [DFD poziom 2 - proces 3](C:/Users/filip/Desktop/masi/dfd_poziom_2_proces_3.puml)

## Zgodność z zasadami z PDF

- każdy proces ma co najmniej jedno wejście i jedno wyjście,
- procesy są ponumerowane zgodnie z wymaganiami: `1, 2, 3` oraz `1.1-1.5`, `2.1-2.5`, `3.1-3.5`,
- nie ma bezpośrednich połączeń użytkownik-magazyn ani system zewnętrzny-magazyn,
- przepływy mają krótkie nazwy, a ich znaczenie jest opisane poniżej w słowniku danych,
- magazyny danych mają nazwy rzeczownikowe odpowiadające przechowywanym zbiorom danych.

## Magazyny danych

- `D1 Oferty`
- `D2 Aplikacje`
- `D3 Rankingi`
- `D4 Listy kandydatów`
- `D5 Rozmowy`
- `D6 Opinie klientów`
- `D7 Wyniki analiz`

## Słownik danych

### Obiekty podstawowe

`dane oferty = id klienta, nazwa stanowiska, opis stanowiska, wymagane kompetencje, lokalizacja, tryb pracy, widełki płacowe, termin publikacji`

`dane CRM = id klienta, nazwa klienta, dane kontaktowe klienta, status klienta, dane oferty`

`oferta robocza = dane oferty, dane CRM, status oferty`

`status oferty = [robocza|opublikowana|zamknięta]`

`oferta = @id oferty, id klienta, nazwa stanowiska, opis stanowiska, wymagane kompetencje, lokalizacja, tryb pracy, widełki płacowe, status oferty, data publikacji`

`oferty = {oferta}`

`CV = nazwa pliku, format pliku, rozmiar pliku, treść CV`

`zgoda = [tak|nie]`

`zgody = {zgoda}`

`dane aplikacji = imię, nazwisko, e-mail, telefon, id oferty, CV, (list motywacyjny), zgody`

`status aplikacji = [złożona|duplikat|do analizy|odrzucona|zakwalifikowana]`

`kandydat = @id kandydata, imię, nazwisko, e-mail, telefon`

`aplikacja = @id aplikacji, kandydat, id oferty, CV, status aplikacji, data złożenia`

`aplikacje = {aplikacja}`

`błędy = {nazwa pola, opis błędu}`

`wiadomość = adres e-mail, temat, treść, (załączniki)`

`status wysyłki = [wysłano|oczekuje|błąd]`

`potwierdzenie = [tak|nie]`

`kryteria selekcji = id oferty, minimalna ocena, wymagane kompetencje, preferowane kompetencje`

`kryteria = wymagane kompetencje, preferowane kompetencje, słowa kluczowe`

`profil = id aplikacji, umiejętności, doświadczenie, wykształcenie, słowa kluczowe`

`profile = {profil}`

`wynik analizy = @id wyniku, id aplikacji, ocena dopasowania, poziom pewności, brakujące kompetencje, rekomendacja`

`wyniki analiz = {wynik analizy}`

`ranking = {pozycja rankingu}`

`rankingi = {ranking}`

`pozycja rankingu = id aplikacji, kandydat, ocena dopasowania, poziom pewności, rekomendacja`

`kandydat wybrany = id aplikacji, kandydat, ocena dopasowania, status etapu`

`lista kandydatów = @id listy, id oferty, {kandydat wybrany}, data zatwierdzenia`

`listy kandydatów = {lista kandydatów}`

`decyzja = [zaprosić|odrzucić|do ponownej analizy]`

`decyzja kandydata = id aplikacji, decyzja, (uwagi)`

`decyzja klienta = id listy, {decyzja kandydata}, (uwagi ogólne)`

`opinia klienta = @id opinii, id listy, {decyzja kandydata}, (uwagi ogólne), data decyzji`

`opinie klientów = {opinia klienta}`

`dane rozmowy = id rekrutacji, forma rozmowy, czas trwania, uczestnicy, zakres terminów`

`propozycja terminu = data, godzina od, godzina do, forma rozmowy, uczestnicy`

`dane spotkania = id rozmowy, uczestnicy, data, godzina od, godzina do, forma rozmowy`

`termin = data, godzina od, godzina do, dostępność`

`terminy = {termin}`

`zaproszenie = adres e-mail, szczegóły rozmowy, link potwierdzenia`

`odpowiedź terminu = [akceptacja|odrzucenie|brak odpowiedzi]`

`status rozmowy = [proponowana|oczekuje na potwierdzenie|zatwierdzona|odrzucona|anulowana]`

`rozmowa = @id rozmowy, id listy, kandydat, klient, rekruter, termin, forma rozmowy, status rozmowy`

`rozmowy = {rozmowa}`

`id rekrutacji = @id rekrutacji`

`zapytanie oferty = id klienta, (id oferty CRM)`

## Przepływy z diagramów

### Poziom 1

- `dane oferty`
- `zapytanie oferty`
- `potwierdzenie`
- `dane aplikacji`
- `oferta`
- `oferty`
- `aplikacja`
- `kryteria selekcji`
- `aplikacje`
- `ranking`
- `lista kandydatów`
- `dane rozmowy`
- `decyzja klienta`
- `odpowiedź terminu`
- `status rozmowy`
- `zaproszenie`
- `dane spotkania`
- `terminy`
- `wiadomość`
- `status wysyłki`
- `rozmowa`
- `rozmowy`

### Dekompozycja procesu 1

- `dane CRM`
- `oferta robocza`
- `status oferty`
- `błędy`

### Dekompozycja procesu 2

- `kryteria`
- `CV`
- `profile`
- `wynik analizy`
- `wyniki analiz`

### Dekompozycja procesu 3

- `id rekrutacji`
- `opinia klienta`
- `propozycja terminu`

## Uwagi do oddania

Jeżeli prowadzący wymaga plików graficznych zamiast źródeł, te diagramy można bezpośrednio wyrenderować z plików `.puml` do SVG lub PNG. W obecnym repo źródła są gotowe, a nazewnictwo i struktura przepływów zostały dopasowane do zasad z instrukcji laboratoryjnej.
