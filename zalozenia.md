# System wspomagający proces rekrutacji w firmie HR

# Filip Stępień - 1ID21A

**1. Cele przedsięwzięcia**

Celem przedsięwzięcia jest zaprojektowanie systemu informatycznego wspomagającego procesy
rekrutacyjne w firmie HR z wykorzystaniem narzędzi sztucznej inteligencji. System będzie wspierał
proces przyjmowania i rejestracji aplikacji kandydatów, analizę i selekcję CV z użyciem AI oraz
planowanie i obsługę rozmów kwalifikacyjnych z klientem zlecającym rekrutację.

**2. Zakres przedsięwzięcia**

- Przyjmowanie i rejestracja aplikacji kandydatów.
    Użytkownicy: rekruter, kandydat
- Analiza i selekcja CV z wykorzystaniem sztucznej inteligencji.
    Użytkownicy: rekruter
- Planowanie i obsługa rozmów kwalifikacyjnych z klientem.
    Użytkownicy: rekruter, kandydat, klient

**3. Opis użytkowników i systemów zewnętrznych projektowanego systemu informatycznego**

System będzie obsługiwany przez trzy grupy użytkowników:

- kandydatów – przesyłających aplikacje i umawiających się na rozmowy rekrutacyjne,
- rekruterów – odpowiedzialnych za analizę CV, selekcję kandydatów i planowanie rozmów,
- klientów – firm zlecających rekrutację, przeglądających wyniki selekcji.

System będzie współpracował z zewnętrznymi systemami i usługami:

- API kalendarza Google Calendar – do planowania terminów rozmów kwalifikacyjnych,
- system CRM funkcjonujący w firmie – zarządzający danymi klientów i ofert pracy,
- system poczty elektronicznej – automatycznie wysyłający powiadomienia i zaproszenia dla
    kandydatów i klientów.

**4. Ogólny opis wymagań**

System musi spełniać następujące wymagania niefunkcjonalne:

- Dostęp do systemu powinien być całodobowy przez 7 dni w tygodniu, z możliwością
    odzyskiwania danych z kopii zapasowych w przypadku awarii.
- Wszystkie dane klientów, kandydatów i rekruterów muszą być przechowywane w sposób
    bezpieczny.
- System powinien być wydajny, umożliwiając przetwarzanie aplikacji i CV, oraz
    generowanie raportów i powiadomień bez długich czasów oczekiwania.
- Interfejs powinien być intuicyjny i przyjazdy dla użytkownika końcowego.
- Architektura systemu musi umożliwiać łatwą rozbudowę o nowe funkcje i integracje z
    nowymi systemami.


**5. Ogólna koncepcja systemu**

System zostanie zbudowany w architekturze web service: frontend w frameworku React, natomiast
backend w języku Python i frameworku Django. System będzie przechowywał dane kandydatów
(CV, dane kontaktowe, wyniki przetwarzania), dane klientów (oferty pracy) oraz harmonogramy
rozmów. Dostęp do systemu będzie odbywał się przez przeglądarkę internetową. Do analizy CV
wykorzystanie zostanie model NLP BERT klasyfikujący kandydatów według dopasowania do ofert
pracy. Model będzie trenowany na danych historycznych rekrutacji, oznaczonych stanowiskami
i odpowiadającymi CV.

**6. Wstępne oszacowanie kosztów**

Wstępne oszacowanie kosztów:

- narzędzia programistyczne (hosting, środowisko programistyczne) – 20 000 zł
- projekt oprogramowania (architektura, integracje) – 50 000 zł
- implementacja i wynagrodzenie programistów i specjalistów – 500 000 zł
- trenowanie modelu – 30 000 zł
- testowanie systemu – 30 000 zł
- wdrożenie – 20 000 zł

**7. Wstępny harmonogram prac**

- analiza wymagań – 4 tygodnie
- implementacja backendu i integracji z systemami zewnętrznymi – 12 tygodnie
- implementacja frontendu – 8 tygodni
- przygotowanie danych i trenowanie modelu – 3 tygodnie
- testowanie systemu – 3 tygodnie
- wdrożenie i szkolenie użytkowników – 2 tygodnie

**8. Opis rozważanych rozwiązań, ich ocena i uzasadnienie wyboru jednego z nich**

```
Rozwiązanie Django Flask
Cena (PLN) 0 (open source) 0 (open source)
Czas wdrożenia (tyg.) 10 12
Skalowalność (%) 90 80
Wydajność (RPS) 150 100
Niezawodność (błędy / tydz.) 1 1
```
```
Rozwiązanie Django Flask
Cena (PLN) 0 0
Czas wdrożenia (tyg.) 1 0.
Skalowalność (%) 1 0.
Wydajność renderowania (RPS) 1 0.
Niezawodność (błędy / tydz.) 1 1
```

```
Rozwiązanie React Vue
Cena (PLN) 0 (open source) 0 (open source)
Czas wdrożenia (tyg.) 10 12
Skalowalność (%) 90 80
Wydajność renderowania (RPS) 150 100
Niezawodność (błędy / tydz.) 2 1
```
```
Rozwiązanie React Vue
Cena (PLN) 0 0
Czas wdrożenia (tyg.) 1 0.
Skalowalność (%) 1 0.
Wydajność renderowania (RPS) 0.75 0.
Niezawodność (błędy / tydz.) 0.9 1
```

**9. Opis wymaganych zasobów**

Zasoby wymagane do realizacji systemu:

- komputery stacjonarne / laptopy
- serwery z GPU, serwery NAS
- drukarki kolorowe
- sieć Wi-Fi / LAN
- zasilacze UPS


