# Specyfikacja wymagań na oprogramowanie (SRS)

## System wspomagający proces rekrutacji w firmie HR

Autor: Filip Stępień - 1ID21A

## 1 Wprowadzenie

### 1.1 Zakres systemu informatycznego

System ma na celu wspomaganie procesu rekrutacji w firmie HR. Dzięki temu wyeliminowany zostanie problem ręcznej obsługi aplikacji kandydatów i CV oraz trudności związanych z uzgadnianiem terminów rozmów kwalifikacyjnych między rekruterem, kandydatem i klientem.

Problem dotyczy działu rekrutacji. Ręczna obsługa aplikacji kandydatów i CV oraz trudności związane z uzgadnianiem terminów rozmów rekrutacyjnych powodują długi czas odpowiedzi na aplikację. Przez ten fakt rośnie ryzyko pominięcia wartościowych kandydatów oraz opóźnień w realizacji procesu rekrutacyjego. Powoduje to wzrost kosztów operacyjnych firm zlecającyh rekrutację oraz przedłużanie czasu zatudnienia pracowników.

W związku z tymi problemami, rozwiązanie ma zapewnić łatwy sposób na obsługę aplikacji kandydatów, przechowywanie dokumentów aplikacyjnych i danych kontaktowych, analizę i wstępną selekcję CV, jak i również planowanie rozmów kwalifikacyjnych oraz udostępnianie wyników rekrutacji klientowi.

### 1.2 Definicje, akronimy, skróty

- AI - sztuczna inteligencja
- API - interfejs programistyczny
- BERT - model sztucznej inteligencji do przetwarzania języka naturalnego
- CRM - system zarządzania relacjami z klientami, przechowujący dane klientów i ofert rekrutacyjnych
- CV - Curriculum Vitae, dokument kandydata zawierający informacje o doświadczeniu, edukacji i umiejętnościach
- HR - dział firmy związany z rekrutacją i zarządzaniem zasobami ludzkimi
- RODO - rozporządzenie o ochronie danych osobowych

### 1.3 Odwołania do literatury

1. Jacob Devlin, Ming-Wei Chang, Kenton Lee, Kristina Toutanova, "BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding", NAACL 2019, https://aclanthology.org/N19-1423/
2. Django Documentation, wersja 5.2, https://docs.djangoproject.com/en/5.2/
3. React Documentation, https://react.dev/
4. Google Calendar API overview, https://developers.google.com/workspace/calendar/api/guides/overview
5. Rozporządzenie (UE) 2016/679 Parlamentu Europejskiego i Rady z dnia 27 kwietnia 2016 r. (RODO), https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32016R0679
6. Rozporządzenie (UE) 2024/1689 Parlamentu Europejskiego i Rady z dnia 13 czerwca 2024 r. (Artificial Intelligence Act), https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32024R1689

## 2 Ogólny opis produktu

### 2.1 Kontekst funkcjonowania

System będzie zarówno obsługiwał użytkowników końcowych jak i integrował się z systemami zewnętrznymi wspierającymi realizację procesu - z systemem CRM firmy HR, usługą Google Calendar oraz systemem poczty elektronicznej.

![Diagram kontekstu funkcjonowania](context.puml)

### 2.2 Charakterystyka użytkowników

- Kandydat - wiek 20-55 lat, podstawowy, średni lub zaawansowany poziom obsługi komputera, stały dostęp do internetu, wymagane umiejętności: wypełnienie formularza, przesłanie CV, odczyt powiadomień i potwierdzenie terminu rozmowy.
- Rekruter - wiek 25-50 lat, średni lub zaawansowany poziom obsługi komputera, stały dostęp do internetu, wymagane umiejętności: obsługa systemu webowego, ocena kandydatów, interpretacja wyników AI i planowanie spotkań.
- Klient - wiek 30-60 lat, podstawowy lub średni poziom obsługi komputera, stały dostęp do internetu, wymagane umiejętności: przegląd listy kandydatów, udzielanie informacji zwrotnej i akceptacja udziału w rozmowie.

### 2.3 Główne funkcje produktu

![Diagram przypadków użycia](usecase.puml)

### 2.4 Założenia i zależności

System będzie działał jako aplikacja webowa dostępna przez przeglądarkę internetową. Warstwa frontendowa zostanie zbudowana w React, a backend w Pythonie z użyciem frameworka Django. System będzie zintegrowany z CRM firmy HR, z którego będą pobierane informacje o ofertach i klientach, a także z usługą poczty elektronicznej oraz Google Calendar. Model AI będzie jedynie wspierał rekrutera - ostateczne decyzje w procesie rekrutacji zawsze będzie podejmował człowiek. Do procesu nauki modelu sztucznej inteligencji wykorzystany zostanie zbiór historycznych danych rekrutacyjnych, zawierający CV, opisy ofert oraz wcześniejsze oceny kandydatów (co najmniej 10 tyś. rekordów). Dane wykorzystywane do uczenia modelu powinny być odpowiednio zanonimizowane, a cały system musi działać zgodnie z przepisami o ochronie danych osobowych.

## 3 Wymagania funkcjonalne

### 3.1 Interfejsy zewnętrzne

#### 3.1.1 System -> Google Calendar API

Interfejs służy do obsługi rozmów kwalifikacyjnych w kalendarzu. Komunikacja odbywa się przez protokół HTTPS (REST API) z użyciem formatu JSON oraz autoryzacji OAuth 2.0.

Żądanie zawiera identyfikator spotkania, a w przypadku próby utworzenia - również szczegóły takie jak termin, czas trwania. Zwracana list spotkań lub informacja o ewentualnych konfliktach terminów.

Odpowiedź interfejsu może zawierać zarówno żądane dane, jak i informacje o błędzie, np. konflikt terminów.

#### 3.1.2 System -> CRM firmy HR

Interfejs służy do pobierania danych klientów i ofert pracy. Komunikacja odbywa się przez protokół HTTPS (REST API) z użyciem formatu JSON. Dostęp do interfejsu jest zabezpieczony tokenem API.

Żądanie może zawierać identyfikator klienta lub identyfikator oferty - zwracane są wówczas szczegóły rekordów - dane osobowe w przypadku klienta oraz opis stanowsika i wymagane kompetencje w przypadku ofert pracy. Możliwe jest również wykonanie żądania w celu pobrania wszystkich ofert.

W przypadku błędu odpowiedź zawiera odpowiedni komunikat, np. brak autoryzacji.

#### 3.1.3 System -> System poczty elektronicznej

Interfejs służy do wysyłania powiadomień, m.in. potwierdzeń aplikacji i zaproszeń na rozmowy.

Interfejs otrzymuje adres e-mail odbiorcy, temat wiadomości, jej treść oraz ewentalne załączniki. Zwracany jest status wysyłki oraz komunikat błędu, jeśli operacja się nie powiedzie. Wiadomość powinna zostać wysłana w czasie do 1 minuty od zatwierdzenia operacji w systemie.

### 3.2 Funkcje

#### 3.2.1 Kandydat

##### 3.2.1.1 Złożenie aplikacji na ofertę

Główny scenariusz:

- kandydat otwiera wybraną ofertę pracy,
- system prezentuje formularz aplikacyjny,
- kandydat uzupełnia wymagane dane i dołącza CV,
- system sprawdza kompletność formularza oraz poprawność załącznika,
- system zapisuje aplikację i przypisuje ją do odpowiedniej oferty,
- system wysyła kandydatowi potwierdzenie złożenia aplikacji.

Rozszerzenia:

- jeśli kandydat nie uzupełni wszystkich wymaganych pól, system wskazuje brakujące dane i nie zapisuje aplikacji,
- jeśli plik CV ma nieprawidłowy format lub zbyt duży rozmiar, system odrzuca załącznik i prosi o ponowne przesłanie,
- jeśli kandydat złożył już aplikację na tę samą ofertę, system informuje o duplikacie i umożliwia aktualizację zgłoszenia,
- jeśli wysłanie potwierdzenia się nie powiedzie, aplikacja pozostaje zapisana, a powiadomienie zostaje oznaczone do ponownej wysyłki.

#### 3.2.2 Rekruter

##### 3.2.2.1 Rejestracja / aktualizacja oferty rekrutacyjnej

Główny scenariusz:

- rekruter wybiera klienta lub rozpoczyna tworzenie nowej oferty,
- system pobiera dane z CRM albo udostępnia formularz ręcznej edycji,
- rekruter uzupełnia lub weryfikuje nazwę stanowiska, opis i wymagane kompetencje,
- system zapisuje ofertę w systemie rekrutacyjnym,
- system publikuje ofertę i udostępnia ją kandydatom.

Rozszerzenia:

- jeśli CRM jest chwilowo niedostępny, system pozwala zapisać ofertę jako wersję roboczą i zsynchronizować ją później,
- jeśli dane oferty są niekompletne, system wskazuje brakujące pola i blokuje publikację,
- jeśli oferta została wycofana lub zamknięta, system blokuje przyjmowanie nowych aplikacji.

##### 3.2.2.2 Analiza i ranking CV z użyciem AI

Główny scenariusz:

- rekruter otwiera listę aplikacji przypisaną do wybranej oferty,
- system odczytuje dane z CV i przygotowuje je do analizy,
- system uruchamia model AI i porównuje profile kandydatów z wymaganiami oferty,
- system wylicza ocenę dopasowania i tworzy ranking kandydatów,
- rekruter przegląda wyniki i weryfikuje rekomendacje systemu.

Rozszerzenia:

- jeśli treść CV nie może zostać poprawnie odczytana, system oznacza aplikację do ręcznej analizy,
- jeśli model zwraca niski poziom pewności oceny, system oznacza wynik do dodatkowej weryfikacji,
- jeśli usługa AI jest niedostępna, system umożliwia ręczne przeglądanie kandydatów i ponowienie analizy później.

##### 3.2.2.3 Utworzenie listy kandydatów

Główny scenariusz:

- rekruter otwiera ranking kandydatów dla wybranej oferty,
- system prezentuje kandydatów uporządkowanych według oceny dopasowania,
- rekruter zaznacza osoby przeznaczone do dalszego etapu,
- system tworzy listę kandydatów i zapisuje ją w ramach danej rekrutacji,
- rekruter zatwierdza listę do dalszego wykorzystania w procesie.

Rozszerzenia:

- jeśli ranking kandydatów nie został jeszcze wygenerowany, system wymaga wcześniejszego wykonania analizy CV,
- jeśli rekruter usunie kandydata z listy, system aktualizuje listę i zapisuje historię zmian,
- jeśli żaden kandydat nie spełnia wymagań, system pozwala pozostawić pustą listę albo wrócić do analizy.

##### 3.2.2.4 Zaplanowanie rozmowy kwalifikacyjnej

Główny scenariusz:

- rekruter wybiera kandydata z listy kandydatów,
- rekruter określa formę rozmowy, przewidywany czas trwania i uczestników spotkania,
- system sprawdza dostępne terminy w kalendarzu,
- system proponuje możliwe terminy rozmowy,
- rekruter wybiera i zatwierdza termin,
- system zapisuje spotkanie, synchronizuje je z kalendarzem i wysyła powiadomienia do kandydata oraz klienta.

Rozszerzenia:

- jeśli wystąpi konflikt terminów, system proponuje inne dostępne terminy,
- jeśli synchronizacja z kalendarzem nie powiedzie się, system zapisuje próbę i umożliwia jej ponowienie,
- jeśli wysłanie powiadomień nie powiedzie się, spotkanie pozostaje zapisane, a system oznacza konieczność ponownej wysyłki.

#### 3.2.3 Klient

##### 3.2.3.1 Przegląd listy kandydatów

Główny scenariusz:

- klient loguje się do systemu lub otwiera bezpieczny link,
- system prezentuje listę kandydatów przypisaną do jego rekrutacji,
- klient przegląda profile kandydatów oraz podstawowe informacje o ich dopasowaniu,
- system udostępnia szczegóły wybranego kandydata,
- klient kończy przegląd listy.

Rozszerzenia:

- jeśli lista kandydatów nie została jeszcze przygotowana, system informuje klienta o braku danych do przeglądu,
- jeśli klient utraci sesję, system wymaga ponownego uwierzytelnienia,
- jeśli klient nie ma uprawnień do danej rekrutacji, system blokuje dostęp do listy.

##### 3.2.3.2 Przekazanie informacji zwrotnej

Główny scenariusz:

- klient otwiera listę kandydatów przypisaną do rekrutacji,
- system prezentuje kandydatów oraz formularz decyzji i uwag,
- klient wskazuje kandydatów zaakceptowanych do dalszego etapu albo wpisuje komentarze,
- system zapisuje informację zwrotną i udostępnia ją rekruterowi,
- system aktualizuje status rekrutacji.

Rozszerzenia:

- jeśli klient nie wybierze żadnego kandydata, system zapisuje informację o konieczności ponownej selekcji,
- jeśli klient przerwie operację przed zatwierdzeniem, system może zapisać wersję roboczą odpowiedzi,
- jeśli zapis informacji zwrotnej się nie powiedzie, system informuje klienta o błędzie i pozwala ponowić operację.

#### 3.2.4 Czynności wspólne dla kandydata i klienta

##### 3.2.4.1 Potwierdzenie terminu rozmowy

Główny scenariusz:

- kandydat albo klient otrzymuje powiadomienie z propozycją terminu rozmowy,
- system udostępnia szczegóły spotkania po otwarciu linku lub zalogowaniu do systemu,
- użytkownik potwierdza proponowany termin,
- system zapisuje odpowiedź,
- jeśli wszystkie wymagane osoby potwierdziły spotkanie, system oznacza termin rozmowy jako zatwierdzony i informuje rekrutera.

Rozszerzenia:

- jeśli kandydat albo klient odrzuci termin, system zapisuje brak akceptacji i przekazuje informację rekruterowi,
- jeśli link do potwierdzenia jest nieważny lub wygasł, system wymaga ponownego wygenerowania zaproszenia,
- jeśli użytkownik nie odpowie w wyznaczonym czasie, system może wysłać przypomnienie.

## 4 Wymagania niefunkcjonalne

### 4.1 Użyteczność

- rekruter po szkoleniu nie dłuższym niż 4 godziny powinien być w stanie samodzielnie obsługiwać podstawowe procesy systemu,
- najważniejsze operacje rekrutera powinny być dostępne z poziomu głównego panelu bez konieczności przechodzenia przez więcej niż 3 ekrany,
- komunikaty błędów powinny być jednoznaczne i wskazywać sposób poprawy danych,
- system powinien być dostosowany co najmniej do pracy na komputerach i urządzeniach mobilnych.

### 4.2 Niezawodność

- dostępność systemu powinna wynosić co najmniej 99,9% w skali roku (maksymalnie ~8h przerwy),
- system powinien wykonywać regularne kopie zapasowe danych nie rzadziej niż raz na 24 godziny,
- po awarii odtworzenie systemu i danych powinno być możliwe w czasie do 4 godzin.

### 4.3 Wydajność

- system powinien obsłużyć co najmniej 1000 jednocześnie zalogowanych użytkowników,
- proces ponownego uczenia modelu AI na zbiorze do 10 000 rekordów powinien zakończyć się w czasie do 8 godzin,
- system powinien przechowywać dane rekrutacyjne bez zauważalnego spadku wydajności przy wzroście liczby rekordów do co najmniej 100 000 rocznie.

### 4.4 Bezpieczeństwo

- każdy użytkownik musi być uwierzytelniony przed uzyskaniem dostępu do danych innych niż publiczne oferty pracy,
- transmisja danych wymagających autoryzacji musi być szyfrowana protokołem TLS,
- hasła użytkowników muszą być przechowywane w postaci bezpiecznych skrótów kryptograficznych,
- dane osobowe kandydatów i klientów muszą być chronione zgodnie z RODO,
- dane wykorzystywane do trenowania modelu AI powinny być odpowiednio zanonimizowane.
