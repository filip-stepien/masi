# Diagramy związków encji (ERD)

## System wspomagający proces rekrutacji w firmie HR

Autor: Filip Stępień - 1ID21A

## Źródła modelu

Diagramy ERD zostały przygotowane na podstawie:

- instrukcji laboratoryjnej `ERD_unlocked.pdf`,
- końcowego sprawozdania DFD `C:/Users/filip/Downloads/1ID21A_Stępień_Filip_3.pdf`,
- specyfikacji wymagań systemu `specyfikacja_wymagan.md`.

Zgodnie z instrukcją ERD model wynika z DFD i przedstawia obiekty, ich atrybuty oraz związki z krotnościami. Związki wiele-do-wielu zostały rozbite przez encje pośrednie.

## Pliki z diagramami

- [Pełny diagram ERD](C:/Users/filip/Desktop/masi/erd_pelny.puml)
- [ERD - obsługa ofert i aplikacji](C:/Users/filip/Desktop/masi/erd_oferty_i_aplikacje.puml)
- [ERD - selekcja kandydatów](C:/Users/filip/Desktop/masi/erd_selekcja_kandydatow.puml)
- [ERD - rozmowy i decyzje klienta](C:/Users/filip/Desktop/masi/erd_rozmowy_i_decyzje.puml)

## Przyjęte decyzje modelowe

- `Klient` i `Rekruter` są pełnymi encjami systemu. Wynika to z końcowego DFD, w którym występują jako uczestnicy procesów, oraz z decyzji projektowej potwierdzonej po analizie dokumentacji.
- Nie utworzono osobnej encji `Rekrutacja`. W końcowym DFD wszystkie główne obiekty procesu są wiązane przez `@id oferty`, dlatego `Oferta` pełni rolę kontekstu rekrutacji.
- Relacja kandydat-oferta jest związkiem wiele-do-wielu rozbitym przez encję `Aplikacja`.
- Relacja ranking-wynik analizy jest rozbita przez encję `Pozycja rankingu`, ponieważ ranking zawiera wiele pozycji, a wynik analizy może pojawić się w kolejnych wersjach rankingu.
- Relacja lista kandydatów-aplikacja jest rozbita przez encję `Kandydat na liście`, ponieważ lista zawiera wielu kandydatów, a kandydat może znaleźć się na listach tworzonych w różnych etapach procesu.
- `Profil kandydata` z DFD potraktowano jako dane wynikające z encji `Kandydat` i `CV`, a nie jako osobny magazyn danych. W DFD profil jest przepływem wykorzystywanym podczas analizy.
- Wartości takie jak `status oferty`, `status aplikacji`, `status rankingu`, `status listy`, `status rozmowy`, `decyzja`, `rekomendacja` i `ocena kandydata` są atrybutami słownikowymi, a nie osobnymi encjami.
- Encje `Wiadomość`, `Status wysyłki`, `Zaproszenie`, `Potwierdzenie`, `Termin`, `Propozycja terminu` i `Spotkanie kalendarza` uwzględniono, ponieważ występują w końcowym słowniku przepływów DFD i są potrzebne do obsługi powiadomień, potwierdzeń oraz synchronizacji z kalendarzem.

## Główne encje

### Uczestnicy procesu

`Kandydat` przechowuje dane osoby aplikującej, dane kontaktowe oraz podstawowy profil zawodowy. Kandydat może posiadać wiele dokumentów `CV` i może złożyć wiele aplikacji, ale tylko jedną aplikację na tę samą ofertę.

`Klient` reprezentuje firmę lub osobę zlecającą rekrutację. Klient zleca oferty, otrzymuje listy kandydatów, wystawia opinie, podejmuje decyzje oraz uczestniczy w rozmowach.

`Rekruter` odpowiada za ofertę, zatwierdza listy kandydatów i planuje rozmowy.

### Oferty i aplikacje

`Oferta` przechowuje dane stanowiska pobierane lub aktualizowane z CRM: tytuł, opis, wymagania, obowiązki, lokalizację, tryb pracy, formę zatrudnienia, wynagrodzenie, status, datę utworzenia i termin ważności.

`Kryteria selekcji` zawierają wymagania wykorzystywane do oceny dopasowania kandydatów do oferty.

`CV` przechowuje przesłany dokument kandydata oraz dane odczytane z dokumentu.

`Aplikacja` łączy kandydata, ofertę i wybrane CV. Zawiera datę zgłoszenia, status aplikacji, wynik wstępnej oceny, komentarz rekrutera oraz opcjonalny list motywacyjny.

### Selekcja kandydatów

`Wynik analizy` zapisuje rezultat oceny aplikacji: wynik punktowy, poziom dopasowania, spełnione i niespełnione kryteria, rekomendację, uzasadnienie oraz datę analizy.

`Ranking` jest tworzony dla konkretnej oferty i ma status, np. roboczy, do zatwierdzenia albo zatwierdzony.

`Pozycja rankingu` opisuje miejsce konkretnego wyniku analizy w rankingu.

`Lista kandydatów` jest przygotowywana dla oferty, klienta i rekrutera.

`Kandydat na liście` opisuje konkretną aplikację umieszczoną na liście kandydatów.

### Decyzje, opinie i rozmowy

`Decyzja klienta` zapisuje decyzję klienta dotyczącą kandydata z listy, np. zaakceptowany, odrzucony, do rozmowy.

`Opinia klienta` zapisuje ocenę, komentarz, mocne i słabe strony oraz rekomendację klienta.

`Rozmowa` dotyczy wybranego kandydata z listy, oferty, klienta i rekrutera. Zawiera formę rozmowy, lokalizację lub link, status, wynik i notatki.

`Propozycja terminu` przechowuje proponowany termin rozmowy oraz jego status.

`Termin` przechowuje potwierdzony lub aktualny termin rozmowy.

`Spotkanie kalendarza` odwzorowuje dane spotkania synchronizowane z Google Calendar.

`Zaproszenie`, `Wiadomość`, `Status wysyłki` i `Potwierdzenie` obsługują wysyłkę informacji do uczestników i zbieranie odpowiedzi. `Wiadomość` może dotyczyć potwierdzenia aplikacji albo zaproszenia na rozmowę, a `Potwierdzenie` może dotyczyć aplikacji albo rozmowy, zgodnie z typem potwierdzenia z DFD.

## Najważniejsze związki

- Jeden `Klient` może zlecić wiele `Ofert`.
- Jeden `Rekruter` może odpowiadać za wiele `Ofert`.
- Jedna `Oferta` ma jedne `Kryteria selekcji`.
- Jeden `Kandydat` może posiadać wiele dokumentów `CV`.
- Jeden `Kandydat` może złożyć wiele `Aplikacji`.
- Jedna `Oferta` może mieć wiele `Aplikacji`.
- Jedna `Aplikacja` może mieć wiele `Wyników analizy`, np. po ponownym uruchomieniu analizy.
- Jedna `Oferta` może mieć wiele `Rankingów`.
- Jeden `Ranking` zawiera wiele `Pozycji rankingu`.
- Jedna `Lista kandydatów` zawiera wiele pozycji `Kandydat na liście`.
- Jeden `Kandydat na liście` może mieć wiele `Decyzji klienta` i `Opinii klienta`.
- Jeden `Kandydat na liście` może prowadzić do wielu `Rozmów`, np. po przełożeniu lub kolejnym etapie.
- Jedna `Rozmowa` może mieć wiele `Propozycji terminu`.
- Jedna `Rozmowa` ma maksymalnie jeden aktualny `Termin` potwierdzony.
- Jedna `Aplikacja` może wygenerować wiadomość i potwierdzenie zgłoszenia.
- Jedna `Rozmowa` może wygenerować wiele `Zaproszeń`, `Wiadomości` i `Potwierdzeń`.

## Mapowanie magazynów DFD na ERD

| Magazyn DFD | Encje ERD |
| --- | --- |
| Oferty | `Oferta`, `Kryteria selekcji`, `Klient`, `Rekruter` |
| Aplikacje | `Kandydat`, `CV`, `Aplikacja` |
| Wyniki analiz | `Wynik analizy` |
| Rankingi | `Ranking`, `Pozycja rankingu` |
| Listy kandydatów | `Lista kandydatów`, `Kandydat na liście` |
| Opinie klientów | `Decyzja klienta`, `Opinia klienta` |
| Rozmowy | `Rozmowa`, `Propozycja terminu`, `Termin`, `Spotkanie kalendarza`, `Zaproszenie`, `Wiadomość`, `Status wysyłki`, `Potwierdzenie` |
