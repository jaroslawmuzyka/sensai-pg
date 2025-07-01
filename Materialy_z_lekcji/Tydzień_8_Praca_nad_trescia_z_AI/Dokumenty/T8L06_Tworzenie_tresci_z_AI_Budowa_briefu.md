# T8L06: Tworzenie treści z AI - Budowa briefu

**Lekcja:** T8L06  
**Tydzień:** 8  
**Temat:** Tworzenie treści z AI: Budowa briefu  
**Platforma:** [SensAI Academy - Lekcja T8L06](https://learn.sensai.academy/next/public/lesson/351)

## Wprowadzenie

Ta lekcja pokazuje, jak przygotować szczegółowy "brief" dla sztucznej inteligencji. Celem jest precyzyjne sterowanie procesem generacji treści, aby uzyskać jak najwyższą jakość tekstu. Zamiast tworzyć cały artykuł za jednym razem, proces jest dzielony na mniejsze, zarządzalne etapy — generowanie treści nagłówków po nagłówku.

## 📂 Materiały do pobrania

- **[Pobierz plik workflow do Dify](https://learn.sensai.academy/download.php?lfid=71)**

## Dlaczego brief jest kluczowy?

Sztuczna inteligencja działa na zasadzie prawdopodobieństwa. Aby uzyskać spójny i merytoryczny tekst, musimy precyzyjnie określić, co ma zostać wygenerowane w każdym kroku. Dzielenie procesu na mniejsze części, takie jak generowanie osobnych akapitów dla każdego nagłówka, minimalizuje ryzyko błędów i "zapominania" o istotnych informacjach przez model językowy. Proces ten przypomina przygotowywanie wytycznych dla profesjonalnego copywritera.

## Elementy potrzebne do stworzenia briefu

Do wygenerowania kompletnego briefu konieczne jest zebranie i wykorzystanie następujących danych z Twojego pliku roboczego:

- **Wszystkie słowa kluczowe:** Pełna lista fraz kluczowych z Google, które mają zostać użyte w artykule.
- **Nagłówki (Headings):** Struktura artykułu w postaci nagłówków, dla których w poprzednim kroku przygotowano bazę wiedzy (RAG).
- **Knowledge Graph:** Graf wiedzy zapewniający szeroki obraz tematu i relacji między pojęciami.
- **Information Graph:** Graf informacji, który dostarcza dodatkowego kontekstu i szczegółów, uzupełniając wiedzę z bazy RAG.

**Wskazówka:** Celowo wykorzystuje się dane z różnych źródeł (RAG, Knowledge Graph, Information Graph), aby zapewnić modelowi AI jak najszerszą perspektywę i zminimalizować ryzyko pominięcia ważnych informacji.

## Struktura wygenerowanego briefu

Wynikiem procesu jest precyzyjny brief dla każdego nagłówka, który zawiera trzy kluczowe elementy:

- **Nagłówek:** Wskazuje konkretny fragment tekstu, który ma zostać w danym momencie wygenerowany (np. "Co to jest kortyzol?").
- **Wiedza do zawarcia:** Informacje pochodzące z `Information Graph` i `Knowledge Graph`, które muszą znaleźć się w danym segmencie tekstu.
- **Słowa kluczowe:** Konkretne frazy, które muszą zostać użyte w treści pod danym nagłówkiem.

## Automatyzacja procesu w Make

Proces tworzenia briefu jest dodawany jako kolejny krok do istniejącej automatyzacji, która budowała bazę wiedzy RAG. Poniżej przedstawiono, jak to skonfigurować.

### Krok 1: Dodanie modułu API do Dify

W istniejącym scenariuszu Make, po module generującym RAG, dodaj nowy moduł API. Nazwij go "Brief" i wklej swój klucz API do **Dify**.

### Krok 2: Konfiguracja danych wejściowych (JSON)

W module "Brief" należy przygotować strukturę danych w formacie JSON, która zostanie wysłana do Dify. Musi ona zawierać wszystkie wymagane elementy. Pamiętaj, aby zmapować odpowiednie zmienne z poprzednich modułów w Make.

Dane wejściowe powinny zawierać:

- `keyword`: Główne słowo kluczowe.
- `frazy`: Wszystkie słowa kluczowe pobrane z wyników wyszukiwania.
- `headings`: Lista wszystkich nagłówków artykułu.
- `knowledge_graph`: Dane z grafu wiedzy.
- `information_graph`: Dane z grafu informacji.

**Wskazówka:** Jeśli nowo dodane zmienne (np. `frazy`) nie są od razu widoczne w panelu mapowania, zapisz scenariusz i odśwież okno przeglądarki.

### Krok 3: Uruchomienie testowe i obsługa wyników

Uruchom scenariusz raz, aby Make "nauczył się" struktury danych wyjściowych z modułu Dify. Wynikiem działania modułu "Brief" będą dwie części: właściwy brief w formie tekstowej oraz jego wersja w formacie `.html`.

### Krok 4: Zapisywanie wyników w Google Sheets i Google Drive

Aby w pełni zautomatyzować proces i archiwizować wyniki, dodaj kolejne moduły w Make:

1. **Zapisz brief tekstowy:** Użyj modułu Google Sheets, aby zapisać wygenerowany brief tekstowy w odpowiedniej kolumnie arkusza (w przykładzie jest to kolumna **Q**).

2. **Stwórz plik HTML:** Dodaj moduł Google Docs z akcją "Create Document". Jako treść dokumentu przekaż dane HTML otrzymane z Dify. Nazwij plik, używając np. numeru wiersza i słowa kluczowego, aby łatwo go zidentyfikować.

3. **Zapisz link do pliku:** Na koniec, w module Google Sheets, zapisz link do nowo utworzonego dokumentu Google (`web view link`) w dedykowanej kolumnie (w przykładzie — **R**).

## Podsumowanie

Po wykonaniu tych kroków proces jest w pełni zautomatyzowany. Dla każdego tematu generowany jest nie tylko brief tekstowy zapisany w arkuszu, ale także gotowy do udostępnienia plik HTML na Dysku Google. Z tak przygotowanym materiałem można przejść do finalnego etapu, czyli generowania treści artykułu.

## Powiązane automatyzacje z repozytorium

### Automatyzacje Dify (.yml)
- **[SEO 3.0] Content brief.yml** - główna automatyzacja do generacji briefu treści
  - Lokalizacja: `../../Automatyzacje/[SEO 3.0] Content brief.yml`
  - Opis: Expert content brief generator, który mapuje wiedzę i słowa kluczowe do predefiniowanej listy nagłówków

### Automatyzacje Make.com (.blueprint.json)
- **SEO 3.0 [4] - Content generator.blueprint.json** - kompletna automatyzacja Make.com
  - Lokalizacja: `../../Automatyzacje/SEO 3.0 [4] - Content generator.blueprint.json`
  - Opis: Zawiera moduły "Brief" do tworzenia briefów tekstowych i HTML, integrację z Google Sheets i Google Drive

## Kluczowe koncepty

- **Brief Generator**: Narzędzie do precyzyjnego sterowania procesem generacji treści
- **Modular Approach**: Dzielenie procesu na mniejsze, zarządzalne etapy
- **Knowledge Integration**: Wykorzystanie danych z RAG, Knowledge Graph i Information Graph
- **Automated Workflow**: Pełna automatyzacja od briefu do archiwizacji wyników
- **Make.com Integration**: Rozszerzenie istniejącej automatyzacji o moduł Brief
- **Quality Control**: Precyzyjne określanie co ma zostać wygenerowane w każdym kroku

## Proces techniczny

1. **Przygotowanie danych**: Aggregacja słów kluczowych, nagłówków i grafów wiedzy
2. **Konfiguracja API**: Dodanie modułu Brief do istniejącej automatyzacji Make
3. **Mapowanie zmiennych**: Połączenie danych z poprzednich modułów z nowym modułem Brief
4. **Generacja briefu**: Tworzenie briefów tekstowych i HTML przez Dify
5. **Archiwizacja**: Zapisywanie wyników w Google Sheets i Google Drive
6. **Weryfikacja**: Testowanie i optymalizacja przepływu danych

## Zaawansowane funkcje

- **Dual Output Format**: Brief tekstowy i HTML dla różnych zastosowań
- **Automatic File Naming**: Inteligentne nazewnictwo plików z numerem wiersza i słowem kluczowym
- **Link Management**: Automatyczne zapisywanie linków do dokumentów Google
- **Variable Mapping**: Dynamiczne mapowanie zmiennych z poprzednich modułów
- **Error Handling**: Obsługa sytuacji gdy zmienne nie są od razu widoczne
- **Workflow Extension**: Bezproblemowe rozszerzenie istniejących automatyzacji 