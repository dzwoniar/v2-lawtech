# Lawtech v2 — landing automatyzacji pism z kalkulatorem

Statyczny prototyp strony prezentującej koncepcję automatyzacji pism dla kancelarii. Rozwija [wariant v1](https://github.com/dzwoniar/v1-lawtech) o kalkulator kosztu pracy oraz sekcje procesu, oferty i gwarancji.

Repozytorium zawiera frontend demonstracyjny. Nie generuje pism, nie przetwarza dokumentów i nie łączy się z usługą AI.

## Funkcje

- Responsywna prezentacja oferty, procesu współpracy, opinii i FAQ.
- Kalkulator aktualizowany dwoma suwakami: godzin tygodniowo i stawki godzinowej.
- Formularz imienia, e-maila i zgody oraz uproszczony formularz popupu.
- Walidacja JavaScript i lokalna zmiana widoku na potwierdzenie.
- Popup przy opuszczaniu strony, ograniczony flagą w `sessionStorage`.
- Animacje pojawiania się sekcji przez `IntersectionObserver`, natywne FAQ i przewijanie do formularza.

## Uruchomienie lokalne

Wymagania: współczesna przeglądarka oraz Python 3 do serwowania plików.

```bash
git clone https://github.com/dzwoniar/v2-lawtech.git
cd v2-lawtech
python -m http.server 8000 --bind 127.0.0.1
```

Otwórz [http://localhost:8000](http://localhost:8000). Na Windows alternatywą dla `python` jest `py`. Zatrzymaj serwer przez `Ctrl+C`. Nie jest wymagana instalacja pakietów ani budowanie aplikacji.

## Architektura i obliczenia

```text
.
├── index.html   # treść, osadzony CSS i skrypty
└── README.md
```

Całość implementacji znajduje się w [index.html](index.html). Projekt korzysta z HTML5, CSS i JavaScript bez frameworka. Fonty Fraunces i Plus Jakarta Sans są pobierane z Google Fonts, a tekstura SVG jest osadzona w CSS.

`calcROI()` odczytuje 5–40 godzin tygodniowo i stawkę 150–800 PLN/h, po czym aktualizuje wyniki w DOM:

```text
koszt_roczny = godziny_tygodniowo × 4 × 12 × stawka
potencjalna_oszczędność = zaokrąglenie(koszt_roczny × 0,70)
```

Model zakłada cztery tygodnie w miesiącu i stałą oszczędność 70%. To ilustracja scenariusza, bez danych o rzeczywistej skuteczności wdrożenia.

`handleForm()` zatrzymuje wysyłkę, waliduje imię, e-mail oraz zgodę i zmienia widok na potwierdzenie. Nie wysyła danych do API. `sessionStorage` zapisuje flagę `exitPopupShown`, bez danych formularza.

## Ograniczenia

- Nie ma backendu, modelu AI, generowania dokumentów, anonimizacji ani integracji z systemem kancelarii.
- Formularze nie zapisują zgłoszeń i nie wysyłają e-maili. W repozytorium nie ma promowanej checklisty PDF.
- Linki polityki prywatności są odnośnikami `#`.
- Opinie, wyniki, gwarancje oraz deklaracje dotyczące DPA i lokalizacji serwerów są treścią prototypu. Nie stanowią dokumentacji działającej infrastruktury ani potwierdzonych rezultatów.
- Repozytorium nie zawiera konfiguracji środowiska, testów automatycznych ani procesu wdrożenia.
