# Materiały do Tygodnia 8: Praca nad treścią z AI

Ten katalog zawiera materiały dodatkowe do lekcji z ósmego tygodnia kursu SEO 3.0, poświęconego praktycznej pracy nad tworzeniem treści z wykorzystaniem narzędzi sztucznej inteligencji.

## Opis tygodnia

W tym tygodniu skupiamy się na praktycznych aspektach tworzenia wysokiej jakości treści z wykorzystaniem AI. Poznasz zaawansowane techniki promptowania, automatyzację procesów contentowych, optymalizację treści pod kątem semantycznego SEO oraz integrację różnych narzędzi AI w codziennej pracy nad treścią.

## Spis treści

- [Wstęp do tworzenia treści z AI](#lekcja-wstęp-do-tworzenia-treści-z-ai)
- [Tworzenie treści z AI - Budowa wiedzy](#lekcja-tworzenie-treści-z-ai---budowa-wiedzy)
- [Tworzenie treści z AI - Automatyzacja do budowy wiedzy](#lekcja-tworzenie-treści-z-ai---automatyzacja-do-budowy-wiedzy)
- [Tworzenie treści z AI - Budowa struktury nagłówków](#lekcja-tworzenie-treści-z-ai---budowa-struktury-nagłówków)
- [Tworzenie treści z AI - Budowa bazy wiedzy (RAG)](#lekcja-tworzenie-treści-z-ai---budowa-bazy-wiedzy-rag)
- [Tworzenie treści z AI - Budowa briefu](#lekcja-tworzenie-treści-z-ai---budowa-briefu)

---

## Lekcja: Wstęp do tworzenia treści z AI

Ta lekcja rozpoczyna bardzo praktyczny tydzień kursu, w którym skupimy się na automatyzacjach, workflowach i zaawansowanej pracy z jednostką treści. Poznasz procesy i narzędzia, które pozwolą nie tylko generować, ale także skutecznie optymalizować content pod kątem nowoczesnych wyszukiwarek i AI Overview. W lekcji zostanie odtworzony proces bardzo zbliżony do tego, jakiego używa Google do generowania odpowiedzi w AI Overview (RAG - Retrieval-Augmented Generation). Poznasz kluczowe techniki optymalizacji, w tym modele rerankingowe i wykorzystanie "Reasoning Gap" - luk w rozumowaniu treści konkurencji.

**Materiały:**
- Notatka z lekcji: [T8L01_Wstep_do_tworzenia_tresci_z_AI.md](./Dokumenty/T8L01_Wstep_do_tworzenia_tresci_z_AI.md)
- Link do lekcji na platformie: [SensAI Academy](https://learn.sensai.academy/next/public/lesson/349)

**Narzędzia i zasoby:**
- Google Colab: [Praktyczne narzędzie do pracy z treścią](https://colab.research.google.com/drive/1jaCTMhvxX4t3oHJMjQZFIsrc8IVUUryU?usp=sharing)
- Omówienie notatnika w Loom: [Przewodnik wideo](https://www.loom.com/share/b36891b9d36c42a58397b35d1ef41387)
- Wytyczne redakcyjne: [Dokument Google z wytycznymi](https://docs.google.com/document/d/1TglwJ80mAU7tfNjybTgRyXX9sklKanV_uDqvqDcDUCI/edit?usp=sharing)

**Automatyzacje:**
- [SEO 3.0] Generowanie contentu.yml - [link do automatyzacji](../../Automatyzacje/[SEO%203.0]%20Generowanie%20contentu.yml)
- [SEO 3.0] Content brief.yml - [link do automatyzacji](../../Automatyzacje/[SEO%203.0]%20Content%20brief.yml)
- [SEO 3.0] Budowa RAG.yml - [link do automatyzacji](../../Automatyzacje/[SEO%203.0]%20Budowa%20RAG.yml)

---

## Lekcja: Tworzenie treści z AI - Budowa wiedzy

Fundamentalny etap procesu generowania treści z AI - budowa solidnej bazy wiedzy. Lekcja przedstawia kompletny workflow w narzędziu Deefai do zbierania i przetwarzania informacji z różnych źródeł. Obejmuje proces od pobierania danych z wyników wyszukiwania (SerpData), przez crawling stron konkurencji, po analizę treści przez AI i ekstrakcję wiedzy w formie trójników semantycznych, słów kluczowych i grafów wiedzy.

**Materiały:**
- Notatka z lekcji: [T8L02_Tworzenie_tresci_z_AI_Budowa_wiedzy.md](./Dokumenty/T8L02_Tworzenie_tresci_z_AI_Budowa_wiedzy.md)
- Link do lekcji na platformie: [SensAI Academy](https://learn.sensai.academy/next/public/lesson/346)
- Plik workflow Dify: [Pobierz workflow](https://learn.sensai.academy/download.php?lfid=65)

**Kluczowe tematy:**
- 5-etapowy proces generacji treści (budowa wiedzy, struktura nagłówków, generacja treści, brief generacyjny, finalizacja)
- Workflow w narzędziu Deefai i równoległe przetwarzanie danych
- Pobieranie danych z SerpData (AI Overview + Top 10 wyników organicznych)
- Crawling i analiza treści ze stron konkurencji z obsługą błędów
- 4 gałęzie analizy AI: ekstrakcja słów kluczowych, trójniki semantyczne, nagłówki konkurencji, graf wiedzy
- Przygotowanie ustrukturyzowanych danych do kolejnych etapów procesu

**Automatyzacje:**
- [SEO3.0] Budowa bazy wiedzy.yml - [główny workflow](../../Automatyzacje/[SEO3.0]%20Budowa%20bazy%20wiedzy.yml)
- SEO 3.0 - [1] Budowa wiedzy.blueprint.json - [szablon Blueprint](../../Automatyzacje/SEO%203.0%20-%20[1]%20Budowa%20wiedzy.blueprint.json)

---

## Lekcja: Tworzenie treści z AI - Automatyzacja do budowy wiedzy

Praktyczna implementacja automatyzacji procesu budowy wiedzy poprzez integrację Google Sheets jako panelu sterowania z Make.com i Dify. Lekcja pokazuje krok po kroku budowę kompletnego workflow do zarządzania projektami contentowymi, od konfiguracji triggera w arkuszu kalkulacyjnym, przez transformację danych i komunikację z API Dify, po automatyczne zapisywanie wyników z aktualizacją statusu zadań.

**Materiały:**
- Notatka z lekcji: [T8L03_Tworzenie_tresci_z_AI_Automatyzacja_do_budowy_wiedzy.md](./Dokumenty/T8L03_Tworzenie_tresci_z_AI_Automatyzacja_do_budowy_wiedzy.md)
- Link do lekcji na platformie: [SensAI Academy](https://learn.sensai.academy/next/public/lesson/353)
- Plik automatyzacji Make.com: [Pobierz workflow](https://learn.sensai.academy/download.php?lfid=66)

**Kluczowe elementy:**
- Panel sterowania w Google Sheets z dropdown statusów ("Wybierz status", "generuj", "gotowe")
- Kolumny wejściowe: słowo kluczowe, język, AI Overview, status kontrolny
- Kolumny wynikowe: frazy z SERP, graf informacji, nagłówki konkurencji, knowledge graph
- Scenariusz Make.com: trigger Google Sheets Search Rows → JSON Transform → HTTP Request do Dify → Update Row
- Automatyzacja z harmonogramem (co 15 minut) dla bezobsługowego działania

**Materiały zewnętrzne:**
- [Główny arkusz Google Sheets](https://docs.google.com/spreadsheets/d/1SdeOwR3uw0N3MQa3YFX-l66wZ6SO56AlKorQK600a14/edit?usp=sharing) - panel sterowania
- [Katalog z wynikami Google Drive](https://drive.google.com/drive/folders/11_ee_P405ThkaDgQj63QRiWRMRlQzH97?usp=sharing) - brief, content, audyt

**Automatyzacje:**
- [SEO3.0] Budowa bazy wiedzy.yml - [główny workflow YAML](../../Automatyzacje/[SEO3.0]%20Budowa%20bazy%20wiedzy.yml)
- SEO 3.0 - [1] Budowa wiedzy.blueprint.json - [szablon Blueprint Make.com](../../Automatyzacje/SEO%203.0%20-%20[1]%20Budowa%20wiedzy.blueprint.json)

---

## Lekcja: Tworzenie treści z AI - Budowa struktury nagłówków

Drugi kluczowy etap procesu generacji treści - tworzenie struktury nagłówków przy wykorzystaniu nowoczesnych modeli reasoningowych. Lekcja prezentuje metodę generowania trzech typów nagłówków (rozbudowane H2+H3, płaskie H2, pytania) dostosowanych do różnych strategii SEO oraz pełną automatyzację procesu przez Google Sheets i Make.com z etapem manualnej weryfikacji.

**Materiały:**
- Notatka z lekcji: [T8L04_Tworzenie_tresci_z_AI_Budowa_struktury_naglowkow.md](./Dokumenty/T8L04_Tworzenie_tresci_z_AI_Budowa_struktury_naglowkow.md)
- Link do lekcji na platformie: [SensAI Academy](https://learn.sensai.academy/next/public/lesson/347)
- Workflow Dify: [Pobierz workflow](https://learn.sensai.academy/download.php?lfid=67)
- Automatyzacja Make.com: [Pobierz scenariusz](https://learn.sensai.academy/download.php?lfid=68)

**Kluczowe koncepty:**
- **Trzy typy nagłówków:** rozbudowane (H2+H3) dla core section, płaskie H2 jako standard, pytania dla SEO i blog content
- **Reasoning models:** wykorzystanie zaawansowanych promptów z eliminacją redundancji i logicznym przepływem
- **Strategiczne zastosowanie:** dopasowanie typu nagłówków do pozycji artykułu w topical map (rdzeń vs outer section)
- **Punkt kontrolny:** manualna weryfikacja przed przejściem do generacji treści
- **Automatyzacja Make.com:** trigger na status "generuj" → filtr bezpieczeństwa → API Dify → zapis trzech wariantów

**Zaawansowane funkcje:**
- Eliminacja generycznych fraz AI ("Wprowadzenie", "Podsumowanie", "Ultimate Guide")
- Logiczny przepływ użytkownika od definicji głównego pojęcia do tematów pomocniczych
- System statusów z manualną kontrolą jakości przed finalną generacją

**Automatyzacje:**
- [SEO 3.0] Budowa nagłówków - blog.yml - [główny workflow YAML](../../Automatyzacje/[SEO%203.0]%20Budowa%20nagłówków%20-%20blog.yml)
- SEO 3.0 [2] - Nagłówki.blueprint.json - [szablon Blueprint Make.com](../../Automatyzacje/SEO%203.0%20[2]%20-%20Nagłówki.blueprint.json)

---

## Lekcja: Tworzenie treści z AI - Budowa bazy wiedzy (RAG)

Proces budowy bazy wiedzy w modelu RAG (Retrieval-Augmented Generation) z precyzyjnym fragmentowaniem danych (chunking) w celu eliminacji halucynacji w generowanych tekstach. Lekcja obejmuje dwustrategy approach (wiedza dokładna vs. ogólna), ręczny proces w Dify oraz pełną automatyzację Make.com z konfiguracją wyszukiwania hybrydowego i rerankingu.

**Materiały:**
- Notatka z lekcji: [T8L05_Tworzenie_tresci_z_AI_Budowa_bazy_wiedzy_RAG.md](./Dokumenty/T8L05_Tworzenie_tresci_z_AI_Budowa_bazy_wiedzy_RAG.md)
- Link do lekcji na platformie: [SensAI Academy](https://learn.sensai.academy/next/public/lesson/352)
- Workflow Dify: [Pobierz workflow](https://learn.sensai.academy/download.php?lfid=69)
- Automatyzacja Make.com: [Pobierz scenariusz](https://learn.sensai.academy/download.php?lfid=70)

**Kluczowe koncepty:**
- **RAG Architecture:** Retrieval-Augmented Generation dla faktualnych treści bez halucynacji
- **Chunking strategy:** Separator `###`, 450-500 tokenów, zachowanie kontekstu między fragmentami
- **Dwutorowa wiedza:** dokładna (direct answers) vs ogólna (AI-generated additional context)
- **Wyszukiwanie hybrydowe:** połączenie wyszukiwania wektorowego z rerankingiem
- **Quality control:** Testowanie fragmentów, monitoring trafności, optymalizacja parametrów

**Proces techniczny:**
- Generacja danych przez Dify workflow z internet search
- Import do bazy wiedzy z custom separatorem `###`
- Konfiguracja: wysoka jakość wektoryzacji + `base-multimodal-reranker-generic`
- API integration: Dataset ID, authorization headers, JSON body format
- Status management przez Google Sheets (kolumny N, P)

**Zaawansowane funkcje:**
- **Reranking:** Dodatkowa analiza trafności wyników wyszukiwania wektorowego  
- **Hybrid search:** Kombinacja semantic similarity i keyword matching
- **Batch processing:** Skalowalne przetwarzanie wielu słów kluczowych
- **Monitoring:** Analiza pokrycia, threshold similarity, performance tracking

**Automatyzacje:**
- [SEO 3.0] Budowa RAG.yml - [główny workflow YAML](../../Automatyzacje/[SEO%203.0]%20Budowa%20RAG.yml)
- SEO 3.0 [3] - RAG.blueprint.json - [szablon Blueprint Make.com](../../Automatyzacje/SEO%203.0%20[3]%20-%20RAG.blueprint.json)

---

## Lekcja: Tworzenie treści z AI - Budowa briefu

Ostatni etap przed finalną generacją treści - przygotowanie szczegółowych briefów dla AI. Lekcja przedstawia metodę dzielenia procesu generacji na mniejsze, precyzyjnie sterowane kroki, gdzie każdy nagłówek otrzymuje dedykowany brief zawierający konkretne wytyczne, wiedzę do zawarcia i słowa kluczowe. Proces wykorzystuje dane z poprzednich etapów (RAG, Knowledge Graph, Information Graph) i jest w pełni zautomatyzowany przez Make.com z archiwizacją wyników w Google Sheets i Google Drive.

**Materiały:**
- Notatka z lekcji: [T8L06_Tworzenie_tresci_z_AI_Budowa_briefu.md](./Dokumenty/T8L06_Tworzenie_tresci_z_AI_Budowa_briefu.md)
- Link do lekcji na platformie: [SensAI Academy](https://learn.sensai.academy/next/public/lesson/351)
- Workflow Dify: [Pobierz workflow](https://learn.sensai.academy/download.php?lfid=71)

**Kluczowe koncepty:**
- **Brief Generator:** Precyzyjne sterowanie procesem generacji treści przez dzielenie na zarządzalne etapy
- **Knowledge Integration:** Wykorzystanie danych z RAG, Knowledge Graph i Information Graph w jednym briefie
- **Modular Approach:** Generowanie briefów nagłówek po nagłówku dla eliminacji błędów AI
- **Dual Output Format:** Brief tekstowy i HTML dla różnych zastosowań
- **Quality Control:** Precyzyjne określanie co ma zostać wygenerowane w każdym kroku

**Proces techniczny:**
- Agregacja danych: słowa kluczowe, nagłówki, Knowledge Graph, Information Graph
- Rozszerzenie automatyzacji Make.com o moduł "Brief" z API Dify
- Mapowanie zmiennych z poprzednich modułów (frazy, headings, grafy wiedzy)
- Generacja dual output: brief tekstowy + HTML przez Dify
- Automatyzacja archiwizacji: Google Sheets (kolumna Q) + Google Drive z linkami (kolumna R)

**Zaawansowane funkcje:**
- **Variable Mapping:** Dynamiczne mapowanie danych z poprzednich etapów automatyzacji
- **Automatic File Naming:** Inteligentne nazewnictwo plików z numerem wiersza i słowem kluczowym
- **Link Management:** Automatyczne zapisywanie linków do dokumentów Google (`web view link`)
- **Error Handling:** Obsługa sytuacji gdy zmienne nie są od razu widoczne w panelu mapowania
- **Workflow Extension:** Bezproblemowe rozszerzenie istniejących automatyzacji bez konfliktów

**Automatyzacje:**
- [SEO 3.0] Content brief.yml - [główny workflow YAML](../../Automatyzacje/[SEO%203.0]%20Content%20brief.yml)
- SEO 3.0 [4] - Content generator.blueprint.json - [szablon Blueprint Make.com](../../Automatyzacje/SEO%203.0%20[4]%20-%20Content%20generator.blueprint.json)

---

## Dodatkowe zasoby

### Notatniki Google Colab
- [Praktyczne narzędzie do pracy z treścią](https://colab.research.google.com/drive/1jaCTMhvxX4t3oHJMjQZFIsrc8IVUUryU?usp=sharing) - główny notatnik do tej lekcji

### Datasety
*Linki do datasetów wykorzystywanych w tym tygodniu będą dodane w miarę potrzeb.*

### Prompty
*Linki do dedykowanych promptów dla tego tygodnia będą dodane w katalogu [Prompty](../../Prompty/).*

### Automatyzacje
Kompletny zestaw automatyzacji do pracy z treścią dostępny w folderze [Automatyzacje](../../Automatyzacje/) zawiera:
- Narzędzia do generowania treści
- Systemy do budowy bazy wiedzy RAG
- Automatyzacje tworzenia nagłówków i briefów contentowych
- Narzędzia do audytu treści 