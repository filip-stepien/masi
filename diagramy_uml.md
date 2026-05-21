# Diagram klas i diagram aktywnosci

## System wspomagajacy proces rekrutacji w firmie HR

Autor: Filip Stepien - 1ID21A

## Podstawa opracowania

Diagramy zostaly przygotowane na podstawie:

- instrukcji laboratoryjnej `Diagram klas, aktywnosci_unlocked.pdf`,
- specyfikacji wymagan `specyfikacja_wymagan.md`,
- zalozen systemu `zalozenia.md`,
- diagramow DFD i slownika danych `dfd.md`,
- modelu ERD `erd.md` oraz `erd_pelny.puml`.

## Pliki z diagramami

- `diagram_klas.puml` - diagram klas prezentujacy najwazniejsze klasy systemu, ich atrybuty, operacje, krotnosci i relacje.
- `diagram_aktywnosci_ai.puml` - diagram aktywnosci dla funkcjonalnosci "Analiza i ranking CV z uzyciem AI".
- `diagram_aktywnosci_ai.drawio` - edytowalna wersja diagramu aktywnosci przygotowana do otwarcia w app.diagrams.net.

## Zakres diagramu klas

Diagram klas obejmuje najwazniejsze obszary systemu:

- uczestnikow procesu: `Kandydat`, `Rekruter`, `Klient`,
- obsluge ofert i aplikacji: `Oferta`, `KryteriaSelekcji`, `CV`, `Aplikacja`,
- modul AI i ranking: `AnalizatorCV`, `ModelAI`, `ProfilKandydata`, `WynikAnalizy`, `Ranking`, `PozycjaRankingu`,
- dalszy proces rekrutacji: `ListaKandydatow`, `KandydatNaLiscie`, `DecyzjaKlienta`, `Rozmowa`, `Termin`, `Potwierdzenie`, `Wiadomosc`,
- integracje zewnetrzne: `CRMAdapter`, `CalendarAdapter`, `EmailAdapter`.

Relacje zostaly dobrane zgodnie z modelem ERD i wymaganiami z PDF: wystepuje generalizacja (`OsobaSystemu` -> `Kandydat`, `Rekruter`), kompozycje dla elementow nalezacych do calosci, asocjacje z krotnosciami oraz zaleznosci serwisow od klas dziedzinowych.

## Zakres diagramu aktywnosci

Diagram aktywnosci opisuje przypadek uzycia `Analiza i ranking CV z uzyciem AI`. Uwzglednia:

- uruchomienie analizy przez rekrutera,
- pobranie aplikacji i kryteriow selekcji,
- odczyt i normalizacje CV,
- budowe profilu kandydata,
- uruchomienie modulu AI,
- wyliczenie oceny dopasowania, rekomendacji i uzasadnienia,
- obsluge wyjatkow: brak aplikacji, nieczytelne CV, niedostepna usluga AI, niski poziom pewnosci,
- utworzenie i zatwierdzenie rankingu przez rekrutera.

## Zgodnosc z instrukcja

- wykonano diagram klas dla wybranego systemu informatycznego,
- diagram klas prezentuje atrybuty, operacje, widocznosc elementow oraz relacje miedzy klasami,
- wykonano diagram aktywnosci dla funkcjonalnosci zwiazanej z zastosowaniem narzedzia sztucznej inteligencji,
- diagram aktywnosci jest dostepny rowniez w formacie `.drawio`, zgodnym z narzedziem wskazanym w instrukcji.
