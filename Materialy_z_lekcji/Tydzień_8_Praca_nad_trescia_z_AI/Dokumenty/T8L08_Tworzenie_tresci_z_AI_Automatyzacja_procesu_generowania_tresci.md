# T8L08: Tworzenie treści z AI - Automatyzacja procesu generowania treści

**Lekcja:** T8L08  
**Tydzień:** 8  
**Temat:** Tworzenie treści z AI: Automatyzacja procesu generowania treści  
**Platforma:** [SensAI Academy - Lekcja T8L08](https://learn.sensai.academy/next/public/lesson/348)

## Wprowadzenie

Ta lekcja przedstawia ostatni, najbardziej zaawansowany element całego procesu: w pełni zautomatyzowane generowanie kompletnego artykułu na podstawie przygotowanego wcześniej planu nagłówków. Krok po kroku omówimy logikę stojącą za scenariuszem w platformie Make.com, który tworzy treść, paragraf po paragrafie, i zapisuje ją w pliku Google Docs.

Kompletny, gotowy do importu scenariusz automatyzacji jest dostępny w materiałach do pobrania oraz na GitHubie.

## 📂 Materiały do pobrania

- **[Pobierz plik workflow do Dify](https://learn.sensai.academy/download.php?lfid=72)**
- **[Pobierz plik automatyzacji do Make.com](https://learn.sensai.academy/download.php?lfid=73)**

## Logika automatyzacji w Make.com

Scenariusz jest złożony, ale jego działanie opiera się na kilku kluczowych modułach i koncepcjach. Oto jego budowa krok po kroku:

### 1. Wyzwalacz i przygotowanie danych

- **Start procesu:** Automatyzacja uruchamia się, gdy w kolumnie `T` arkusza Google Sheets dla danego wiersza zostanie ustawiony status **"generuj"**.
- **Przetwarzanie danych wejściowych (JSON):** Scenariusz pobiera dane z arkusza (w tym listę nagłówków w formacie JSON). Ponieważ Make.com wymaga specyficznej struktury danych do iteracji, dane te są konwertowane dwukrotnie: najpierw z formatu JSON na obiekt (*bundle*), a następnie na tablicę (*array*), która może być użyta w kolejnych modułach.

### 2. Utworzenie pliku docelowego

Jeszcze przed rozpoczęciem generowania treści, scenariusz tworzy pusty plik w Google Drive. Nazwa pliku jest generowana dynamicznie i zawiera słowo kluczowe, co ułatwia identyfikację. To w tym pliku będą zapisywane kolejne akapity artykułu.

### 3. Zarządzanie kontekstem za pomocą Data Store

To najważniejszy mechanizm w całej automatyzacji, który pozwala na zachowanie kontekstu między generowaniem kolejnych paragrafów.

- **Czym jest Data Store:** Jest to mała, wewnętrzna baza danych w Make.com, która służy do tymczasowego przechowywania informacji.
- **Czyszczenie bazy:** Na początku każdego uruchomienia scenariusza, Data Store jest całkowicie czyszczony. Zapobiega to przenoszeniu kontekstu z poprzednio generowanych artykułów (np. informacji o kortyzolu do artykułu o progesteronie).
- **Pobieranie poprzedniej treści:** W trakcie generowania każdego nowego akapitu, scenariusz odczytuje z Data Store całą treść wygenerowaną do tej pory.
- **Aktualizacja bazy:** Po wygenerowaniu nowego akapitu, Data Store jest ponownie czyszczony, a następnie zapisywana jest w nim zaktualizowana, pełna treść artykułu (stara treść + nowo dodany akapit).

**Ważna instrukcja:** Aby ten proces zadziałał, musisz w swoim koncie Make.com **stworzyć własny Data Store** i dodać w nim jedno pole tekstowe o nazwie `content`. Bez tego automatyzacja napotka błąd.

### 4. Iteracja, generowanie i zapisywanie

Sercem procesu jest iterator, który wykonuje pętlę dla każdego nagłówka z przygotowanej listy.

1. **Pętla po nagłówkach (Iterator):** Moduł pobiera listę nagłówków i dla każdego z nich po kolei wykonuje serię działań.
2. **Wywołanie API Deefai:** Dla każdego nagłówka wysyłane jest zapytanie do workflow w Deefai. Co kluczowe, oprócz samego nagłówka, przekazywana jest również pełna treść wygenerowana do tej pory (pobrana z Data Store), aby AI miało kontekst i mogło napisać spójny akapit.
3. **Dopisywanie paragrafu do pliku:** Zamiast tworzyć plik na końcu, scenariusz używa modułu **Insert a paragraph to a document**. Dzięki temu po każdej iteracji nowy akapit jest natychmiast dopisywany do istniejącego pliku Google Doc.

### 5. Zakończenie procesu

Po zakończeniu wszystkich iteracji, scenariusz wkleja link do gotowego pliku w odpowiedniej kolumnie arkusza i zmienia status na **"gotowe"**.

### Ograniczenia procesu – ważna uwaga

Należy pamiętać, że scenariusz zmienia status w arkuszu na "gotowe" i wkleja link do pliku niemal natychmiast po uruchomieniu. Jednak faktyczne generowanie treści trwa znacznie dłużej, ponieważ każdy akapit wymaga osobnego wywołania API. Obserwuj tworzony plik w Google Docs, aby śledzić postępy w generowaniu artykułu na żywo.

Dzięki tej automatyzacji otrzymujesz kompletny, gotowy do publikacji artykuł, stworzony w sposób ustrukturyzowany i kontekstowy. Zachęcamy do eksperymentowania i rozbudowy tego workflow!

## Powiązane automatyzacje z repozytorium

### Automatyzacje Dify (.yml)
- **[SEO 3.0] Generowanie contentu.yml** - kompletny workflow do generowania treści z procesem humanizacji
  - Lokalizacja: `../../Automatyzacje/[SEO 3.0] Generowanie contentu.yml`
  - Opis: Główny workflow zawierający logikę generowania treści stosowaną w automatyzacji
  - Wykorzystuje wieloetapowy proces z kontrolą kontekstu i jakości

### Automatyzacje Make.com (.blueprint.json)
- **SEO 3.0 [4] - Content generator.blueprint.json** - kompletna automatyzacja Make.com do generowania artykułów
  - Lokalizacja: `../../Automatyzacje/SEO 3.0 [4] - Content generator.blueprint.json`
  - Opis: Scenariusz implementujący pełną automatyzację procesu generowania treści z wykorzystaniem Data Store, iteratorów i integracji z Google Docs

## Kluczowe koncepty

- **End-to-End Automation**: Kompletna automatyzacja od planu nagłówków do gotowego artykułu
- **Data Store Management**: Zarządzanie kontekstem między iteracjami za pomocą wewnętrznej bazy danych Make.com
- **Iterator Pattern**: Przetwarzanie listy nagłówków jeden po drugim z zachowaniem kontekstu
- **Real-time Document Building**: Dopisywanie paragrafów do Google Docs w czasie rzeczywistym
- **Context Preservation**: Przekazywanie pełnej treści wygenerowanej do tej pory do kolejnych iteracji
- **Status Management**: Automatyczne zarządzanie statusami w arkuszu Google Sheets
- **Error Prevention**: Czyszczenie Data Store przed każdym uruchomieniem dla eliminacji cross-contamination
- **Dynamic File Naming**: Automatyczne tworzenie nazw plików z wykorzystaniem słów kluczowych

## Proces techniczny

### Etap 1: Inicjalizacja i przygotowanie
1. **Trigger Activation**: Status "generuj" w kolumnie T arkusza Google Sheets
2. **Data Retrieval**: Pobranie danych z arkusza (słowo kluczowe, nagłówki JSON, brief, RAG)
3. **JSON Processing**: Konwersja JSON → Bundle → Array dla kompatybilności z Make.com
4. **File Creation**: Tworzenie pustego pliku Google Docs z dynamiczną nazwą

### Etap 2: Context Management Setup
- **Data Store Initialization**: Tworzenie/czyszczenie pola `content` w Data Store
- **Context Reset**: Eliminacja pozostałości z poprzednich generacji
- **Memory Allocation**: Przygotowanie przestrzeni na akumulację treści

### Etap 3: Iterative Content Generation
- **Iterator Launch**: Uruchomienie pętli po liście nagłówków
- **Context Retrieval**: Pobranie dotychczasowej treści z Data Store
- **API Call**: Wywołanie Dify API z aktualnym nagłówkiem + kontekstem
- **Content Accumulation**: Dopisanie nowego akapitu do istniejącej treści
- **Data Store Update**: Aktualizacja bazy z nową, pełną treścią

### Etap 4: Document Assembly
- **Paragraph Insertion**: Wykorzystanie "Insert a paragraph to a document" Google Docs
- **Real-time Updates**: Natychmiastowe dodawanie treści do pliku
- **Format Preservation**: Zachowanie formatowania HTML z Dify workflow

### Etap 5: Process Finalization
- **Link Generation**: Utworzenie linku do gotowego dokumentu Google Docs
- **Status Update**: Zmiana statusu na "gotowe" w arkuszu
- **Cleanup**: Finalne czyszczenie Data Store

## Zaawansowane funkcje

- **Asynchronous Processing**: Niezależne przetwarzanie każdego akapitu z zachowaniem kolejności
- **Memory Management**: Efektywne zarządzanie pamięcią przez cykliczne czyszczenie Data Store
- **Error Handling**: Obsługa błędów API i problemów z formatowaniem JSON
- **Scalability**: Możliwość przetwarzania artykułów o dowolnej liczbie nagłówków
- **Integration Layer**: Seamless połączenie między Dify, Make.com i Google Workspace
- **Progress Monitoring**: Możliwość śledzenia postępu generacji w czasie rzeczywistym
- **Quality Control**: Zachowanie kontekstu zapewniające spójność całego artykułu
- **Automated Workflow**: Bezobsługowy proces od triggera do gotowego dokumentu

## Wymagania techniczne

### Make.com Configuration
- **Data Store**: Utworzenie własnego Data Store z polem tekstowym `content`
- **Google Docs Integration**: Konfiguracja połączenia z Google Workspace
- **API Credentials**: Ustawienie autoryzacji dla Dify API
- **Iterator Module**: Konfiguracja do przetwarzania tablic JSON

### Dify Workflow Requirements
- **Content Generation Pipeline**: Workflow z wieloetapową generacją i humanizacją
- **API Endpoint**: Skonfigurowany endpoint do wywołań z Make.com
- **Context Handling**: Obsługa dużych kontekstów (cała dotychczasowa treść)
- **Output Formatting**: Generacja treści w formacie HTML/Markdown

### Google Sheets Structure
- **Column T**: Status control ("generuj", "gotowe")
- **Headers Column**: Lista nagłówków w formacie JSON
- **Output Columns**: Miejsce na link do gotowego dokumentu
- **Input Data**: Słowo kluczowe, brief, dane RAG w odpowiednich kolumnach

## Monitoring i optymalizacja

- **Real-time Tracking**: Obserwowanie procesu generacji w Google Docs
- **Performance Metrics**: Czas generacji na akapit, całkowity czas procesu
- **Error Logging**: Monitorowanie błędów API i problemów z formatowaniem
- **Quality Assessment**: Sprawdzanie spójności między paragrafami
- **Resource Usage**: Monitoring wykorzystania Data Store i limitu API calls
- **Scalability Testing**: Testowanie z artykułami o różnej liczbie nagłówków
- **Context Validation**: Weryfikacja poprawności przekazywania kontekstu
- **Output Quality**: Kontrola formatowania i struktury gotowych dokumentów 