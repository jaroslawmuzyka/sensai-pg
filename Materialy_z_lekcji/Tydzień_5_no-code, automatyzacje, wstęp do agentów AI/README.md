# Tydzień 5: No-code, automatyzacje, wstęp do agentów AI

## Tematy

* Wprowadzenie do Make
* Wprowadzanie do Dify
* Instalacja narzędzi na serwerze, aktualizacja i utrzymanie narzędzi
* Wstęp do agentów AI
* Open AI Agent SDK
* Przykłady agentów

## Projekty

* Proste automatyzacje w Make z wykorzystaniem AI
* Proste procesy w Dify z wykorzystaniem AI

## Rezultaty

* Umiesz poruszać się w środowisku Make i budować proste automatyzacje z wykorzystaniem AI
* Umiesz łączyć zewnętrzne usługi i systemy z Make
* Umiesz poruszać się w środowisku Dify i budować proste procesy z wykorzystaniem AI
* Umiesz połączyć Make z Dify
* Rozumiesz koncepcję agentów AI

## Wprowadzenie do narzędzia Make.com

W tej lekcji poznasz podstawy narzędzia Make.com (dawniej Integromat) i nauczysz się tworzyć pierwsze automatyzacje z wykorzystaniem AI.

### Automatyzacja SensAI - Generowanie nagłówków SEO 3.0

**Plik Google Sheets do skopiowania**: [SensAI - proces generowania nagłówków - SEO 3.0](https://docs.google.com/spreadsheets/d/1aY6QQyK5GoWmMaafN-zIURrL52KC3ER70q0GwbwIarc/edit?usp=sharing)

**Plik automatyzacji**: [SensAI - automatyzacja do tworzenia nagłówków - SEO 3.0.blueprint.json](../../Automatyzacje/SensAI%20-%20automatyzacja%20do%20tworzenia%20nagłówków%20-%20SEO%203.0.blueprint.json)

#### Ogólny opis i cel automatyzacji

Ta automatyzacja to zaawansowane narzędzie do analizy konkurencji SEO, które wykorzystuje sztuczną inteligencję do tworzenia content briefs. System automatycznie analizuje najlepsze wyniki wyszukiwania Google dla danego słowa kluczowego, wyodrębnia z nich kluczowe informacje za pomocą AI, a następnie generuje zoptymalizowaną strukturę artykułu.

**Główne cele:**
- Automatyzacja procesu research konkurencji SEO
- Oszczędność czasu przy tworzeniu content briefs
- Wykorzystanie AI do analizy treści konkurentów
- Generowanie zoptymalizowanych struktur artykułów
- Skalowanie procesu content marketingu

**Korzyści:**
- Kompleksowa analiza TOP 5 wyników Google
- Automatyczne wyodrębnianie faktów z treści konkurentów
- Generowanie profesjonalnych outline'ów artykułów
- Integracja z Google Sheets dla łatwego zarządzania
- Wykorzystanie najnowszych modeli AI (GPT-4o, GPT-4o-mini)

#### Opis automatyzacji krok po kroku

##### 1. **Moduł Google Sheets: Watch Rows** (ID: 7)
- **Co robi**: Monitoruje arkusz Google Sheets i uruchamia automatyzację gdy pojawi się nowy wiersz
- **Konfiguracja**: Śledzi arkusz "SensAI - proces generowania nagłówków - SEO 3.0", Sheet1
- Pobiera słowo kluczowe z kolumny A (np. "Jak obrać ziemiaki?")

##### 2. **HTTP Request do SerpData API** (ID: 5)
- **Co robi**: Wykonuje zapytanie do API SerpData.io aby pobrać wyniki wyszukiwania Google
- **URL**: `https://api.serpdata.io/v1/search?keyword={{słowo_kluczowe}}&hl=pl&gl=pl`
- Pobiera organiczne wyniki wyszukiwania dla danego słowa kluczowego

##### 3. **Basic Feeder - TOP10** (ID: 64)
- **Co robi**: Iteruje przez wyniki organiczne z SerpData
- **Filtr**: "TOP10" - przetwarza wyniki wyszukiwania

##### 4. **HTTP Request do Jina.ai** (ID: 31)
- **Co robi**: Dla każdego wyniku (maksymalnie TOP 5) pobiera treść strony za pomocą Jina.ai
- **URL**: `https://r.jina.ai/{{url_strony}}`
- **Filtr**: "TOP5" - ogranicza do pierwszych 5 wyników
- Ma obsługę błędów (moduł Ignore ID: 66)

##### 5. **Basic Feeder** (ID: 84)
- **Co robi**: Iteruje przez pobrane treści stron

##### 6. **Basic Aggregator** (ID: 88)
- **Co robi**: Agreguje wszystkie pobrane treści w jedną strukturę danych

##### 7. **JSON Transform** (ID: 91)
- **Co robi**: Konwertuje zagregowane dane do formatu JSON

##### 8. **OpenAI GPT-4o-mini - Ekstrakcja faktów** (ID: 68)
- **Co robi**: Używa AI do wyodrębnienia faktów z treści konkurencyjnych stron
- **Prompt**: Zawiera szczegółowe instrukcje do ekstraktowania i organizowania faktów
- Wynik zapisywany w kolumnie C (Facts)

##### 9. **OpenAI GPT-4o - Tworzenie outline** (ID: 71)
- **Co robi**: Na podstawie wyodrębnionych faktów tworzy strukturę artykułu w HTML
- Generuje outline z tagami H1, H2, H3
- Wynik zapisywany w kolumnie D (Outline)

##### 10. **Google Sheets: Update Row** (ID: 72)
- **Co robi**: Zapisuje wyniki z powrotem do arkusza Google Sheets
- Kolumna B: Wyniki SERP
- Kolumna C: Wyodrębnione fakty  
- Kolumna D: Wygenerowany outline

#### Wymagane klucze API i konfiguracja

##### 1. **SerpData.io API Key**
- **Gdzie wstawić**: Moduł HTTP Request (ID: 5)
- **Lokalizacja**: Headers → Authorization → Bearer `[KLUCZ_API]`
- **Jak uzyskać**: Zarejestruj się na [serpdata.io](https://serpdata.io)
- **Uwagi**: Sprawdź limity API i cennik

##### 2. **Jina.ai API Key** 
- **Gdzie wstawić**: Moduł HTTP Request (ID: 31)
- **Lokalizacja**: Headers → Authorization → Bearer `[KLUCZ_API]`
- **Jak uzyskać**: Zarejestruj się na [jina.ai](https://jina.ai)
- **Uwagi**: Usługa do pobierania treści stron internetowych

##### 3. **OpenAI API Key**
- **Gdzie wstawić**: Moduły OpenAI (ID: 68 i 71)
- **Lokalizacja**: Connection → "Senuto" (nazwa połączenia)
- **Jak uzyskać**: 
  1. Załóż konto na [platform.openai.com](https://platform.openai.com)
  2. Przejdź do sekcji API Keys
  3. Wygeneruj nowy klucz API
- **Uwagi**: Wymaga aktywnego konta z dostępem do GPT-4o i GPT-4o-mini

##### 4. **Google Sheets Connection**
- **Gdzie skonfigurować**: Moduły Google Sheets (ID: 7 i 72)  
- **Lokalizacja**: Connection → "D Senuto" (nazwa połączenia)
- **Jak skonfigurować**: 
  1. W Make.com przejdź do Connections
  2. Dodaj nowe połączenie Google Sheets
  3. Autoryzuj dostęp do swojego konta Google
  4. Wybierz odpowiedni arkusz

#### Wymagania techniczne

**Struktura arkusza Google Sheets:**
- **Kolumna A**: Słowo kluczowe (trigger)
- **Kolumna B**: Wyniki SERP (automatycznie wypełniane)
- **Kolumna C**: Wyodrębnione fakty (automatycznie wypełniane)
- **Kolumna D**: Outline artykułu (automatycznie wypełniane)

**Ustawienia Make.com:**
- **Tryb**: Automatyczny (autoCommit: true)
- **Obsługa błędów**: Maksymalnie 3 błędy
- **Strefa**: eu1.make.com
- **Wersja**: 1

#### Podsumowanie działania

Ta automatyzacja tworzy kompleksowy system analizy konkurencji SEO, który:

1. **Pobiera słowa kluczowe** z arkusza Google Sheets
2. **Analizuje TOP 5 wyników Google** dla każdego słowa kluczowego
3. **Ekstraktuje fakty** z treści konkurentów za pomocą AI
4. **Generuje strukturę artykułu** optymalną pod SEO
5. **Zapisuje wyniki** z powrotem do arkusza

To profesjonalne narzędzie do research SEO wykorzystujące najnowsze technologie AI do tworzenia wysokiej jakości content briefs, które znacząco przyspieszają proces tworzenia treści zoptymalizowanych pod wyszukiwarki.

---

## Wstęp do Dify (Lekcja 01)

W tej lekcji poznasz podstawy narzędzia Dify, jego funkcje oraz możliwości wykorzystania w projektach AI.

- Notatka z lekcji: [./Dokumenty/T5L01_Wstep_do_Dify.md](./Dokumenty/T5L01_Wstep_do_Dify.md)
- Platforma kursu: [Wstęp do Dify](https://learn.sensai.academy/next/public/lesson/295)

## Instalacja i wstępna konfiguracja Dify na własnym serwerze (Lekcja 02)

W tej lekcji dowiesz się, jak zainstalować i skonfigurować Dify na własnym serwerze VPS, krok po kroku.

- Notatka z lekcji: [./Dokumenty/T5L02_Instalacja_i_konfiguracja_Dify.md](./Dokumenty/T5L02_Instalacja_i_konfiguracja_Dify.md)
- Platforma kursu: [Instalacja i wstępna konfiguracja Dify na własnym serwerze](https://learn.sensai.academy/next/public/lesson/295)
