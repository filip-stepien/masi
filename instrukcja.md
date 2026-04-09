Instrukcja laboratoryjna nr 2: Specyfikacja wymagań na
oprogramowanie

# Specyfikacja wymagań na oprogramowanie (SRS)

# I. Wprowadzenie

```
Materiały przygotowane w oparciu o wykłady profesora Kazimierza Worwy „Modelowanie
i analiza SI”.
```
# Struktura SRS

## 1 Wprowadzenie

```
1.1 Zakres systemu informatycznego
Krótki opis funkcjonalności modelowanego systemu informatycznego oraz problemów, które
ma rozwiązywać. Należy odpowiedzieć na pytania: na czym polega problem (z punktu
widzenia użytkownika), kogo dotyczy, których działów, jakie straty ponosi użytkownik/firma
w związku z tym problemem, pomysł rozwiązania (podsumowanie funkcjonalności systemu).
Np.: Problem dotyczy kontroli stanu produktów na magazynie. Rozwiązaniem będzie system
automatyzujący obsługę zamówień towaru...
```
```
1.2 Definicje, akronimy, skróty
Definicje terminów specjalistycznych, opis niezrozumiałych terminów. Terminy powinny być
uporządkowane według kolejności alfabetycznej.
```
```
1.3 Odwołania do literatury
Rozdział zawierający wszystkie pozycje literackie, ustawy wykorzystywane w tworzeniu
systemu, np. Ustawa o systemach sztucznej inteligencji, Prawo o szkolnictwie wyższym
i nauce.
```

## 2 Ogólny opis produktu

2.1 Kontekst funkcjonowania

Umiejscowienie systemu pomiędzy użytkownikami oraz systemami zewnętrznymi. Diagram
przedstawiający współpracę modelowanego systemu, użytkowników oraz systemów
zewnętrznych.
Np.: Administrator Ceneo API
Sprzedawca PayU
Księgowa

2.2 **Charakterystyka użytkowników**

Opis przyszłych użytkowników systemu z uwzględnieniem wieku użytkownika,
zaawansowania obsługi komputera, dostępu do internetu, wymagane umiejętności.
Np.: Administrator – wiek 20-40 lat, zaawansowana znajomość obsługi komputera, stały
dostęp do internetu.

2.3 **Główne funkcje produktu**

Diagram przypadków użycia prezentujący funkcje systemu dla poszczególnych
użytkowników.

2.4 **Założenia i zależności**

Wszelkie założenia systemu. Wymagane dane na potrzeby nauczenia wybranego modelu
sztucznej inteligencji.
Np.:
Systemu musi spełniać wymagania stawiane przez ustawę ............Zakłada się używanie
specjalnej klasy sprzętu dla użytkowników różnych działów, nie jest więc potrzebne
rozwiązanie uniwersalne dla całej firmy. W celu nauczenia klasyfikatorów danych tekstowych
potrzebny będzie zbiór zawierający co najmniej 10 tys. rekordów....

[Kontekst funkcjonowania](kontekst_funkcjonowania.png)


## 3 Wymagania funkcjonalne

3.1 I **nterfejsy zewnętrzne**
Opis interfejsów zewnętrznych poprzez które modelowany system będzie współpracował z
systemami zewnętrznymi: nazwa, opis, specyfikacja wyjścia, wejścia, ograniczenia czasowe
itd.
Np.: System → Ceneo API
Każde żądanie do API musi zawierać token autoryzacyjny ważny przez określony czas i
pobierany na podstawie klucza API. Dostęp do usługi odbywa się po protokole https.
Format danych: domyślnie XML, możliwość zastosowania JSON.

3.2 Funkcje
Główny podrozdział, funkcjonalność systemu. Do opisu funkcji należy wykorzystać
przypadki użycia, czyli interakcje pomiędzy użytkownikiem a systemem. Dla
najważniejszych przypadków użycia na diagramie należy opisać scenariusz przypadków
użycia, czyli określić specyfikację przepływu zdarzeń między aktorami, a systemem, np.
System pyta o ilość produktów. Klient wprowadza ilość. W każdym scenariuszu należy
przeanalizować możliwe rozszerzenia. Rozszerzenia w scenariuszu opisują możliwe
alternatywne przepływy zdarzeń (przebieg), np. w zależności od danych uzyskanych od
aktora (np. Klient anuluje operację). Pojedynczy alternatywny przepływ zdarzeń nie powinien
być traktowany jako oddzielny przypadek użycia na diagramie przypadków użycia
(grupujemy wszystko w jeden przypadek i opisujemy w jednym scenariuszu w postaci
scenariuszu głównego i rozszerzeń, na diagramie nie umieszczamy wtedy dodatkowych
przypadków). W przypadku gdy możliwe rozszerzenie jest rozbudowane (zawiera kilka
przepływów) lub np. te same przepływy zdarzeń mogą powtarzać się w różnych przypadkach
użycia, można wyodrębnić je na diagramie w postaci oddzielnych przypadków za pomocą
include lub extend, natomiast wszystko dokładnie opisujemy w scenariuszu przypadku
głównego jako kontynuacja przypadku do którego się odnosi.
Np.:
3.2.1 Księgowa
3.2.1.1 Generowanie faktur
Główny scenariusz:

- księgowa wprowadza dane,
- system wyszukuje konkretne zamówienie,
- księgowa generuje fakturę
- wydruk faktury
Rozszerzenia:
- w przypadku gdy dane na fakturze nie zgadzają się z danymi w systemie, system informuje
księgową o błędzie

## 4 Wymagania niefunkcjonalne

4.1 **Użyteczność**

Wymagana łatwość użytkowania systemu.
Np.: Maksymalny czas szkolenia użytkowników, liczba kontaktów ze wsparciem, łatwy i
prosty interfejs.

4.2 **Niezawodność**

Wymagana niezawodność, czyli np.: średnia liczba godzin pracy systemu bez awarii,
maksymalny czas przerwy w działaniu.

4.3 **Wydajność**

Wymagana wydajność systemu, np.: liczba transakcji które system obsłuży w czasie godziny,
liczba użytkowników zalogowanych w jednym czasie, rozmiar danych treningowych, czas
uczenia modelu sztucznej inteligencji, itp.

4.4 **Bezpieczeństwo**

Wymagane zabezpieczenia systemu, polityka bezpieczeństwa, szyfrowanie.
Np.: System musi zapewniać ciągłą autoryzację użytkowników. Dostęp do systemu jedynie z
sieci wewnętrznej.

# II. Zadania do samodzielnego rozwiązania

1. Dla systemu informatycznego wybranego przedsiębiorstwa należy wykonać
specyfikację wymagań na oprogramowanie - zgodnie z podpunktami zamieszczonymi we
wprowadzeniu.


