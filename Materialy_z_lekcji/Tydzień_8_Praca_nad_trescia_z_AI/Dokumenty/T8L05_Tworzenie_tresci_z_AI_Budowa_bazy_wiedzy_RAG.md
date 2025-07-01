# T8L05: Tworzenie treści z AI - Budowa bazy wiedzy (RAG)

## Opis lekcji

Ta lekcja przeprowadzi Cię przez proces tworzenia bazy wiedzy w modelu RAG (Retrieval-Augmented Generation). Celem jest przygotowanie precyzyjnych, podzielonych na fragmenty danych (tzw. "chunking"), które posłużą sztucznej inteligencji do generowania merytorycznych i zgodnych z faktami treści. Takie podejście znacząco minimalizuje ryzyko wystąpienia halucynacji w generowanych tekstach.

---

## 📂 Materiały do pobrania

**Plik workflow do Dify:**  
[Pobierz plik workflow do Dify](https://learn.sensai.academy/download.php?lfid=69)

**Plik automatyzacji do Make.com:**  
[Pobierz plik automatyzacji do Make.com](https://learn.sensai.academy/download.php?lfid=70)

**Automatyzacje z repozytorium:**
- **[SEO 3.0] Budowa RAG.yml** - [główny workflow YAML](../../../Automatyzacje/[SEO%203.0]%20Budowa%20RAG.yml)
- **SEO 3.0 [3] - RAG.blueprint.json** - [szablon Blueprint Make.com](../../../Automatyzacje/SEO%203.0%20[3]%20-%20RAG.blueprint.json)

---

## Strategia budowy wiedzy: precyzja i kontekst

Proces opiera się na dwóch rodzajach wiedzy pozyskiwanej z internetu na podstawie wcześniej przygotowanych nagłówków:

### 1. Wiedza dokładna
Polega na bezpośrednim znalezieniu odpowiedzi na pytania zawarte w Twoich nagłówkach. AI otrzymuje zadanie, aby dla każdego nagłówka (np. "Jakie funkcje pełni kortyzol?") znaleźć i sformułować konkretną, dopasowaną odpowiedź.

### 2. Wiedza ogólna
W tym podejściu dajemy AI więcej swobody. Na podstawie całego zebranego materiału, model sam decyduje, jakie dodatkowe pytania warto zadać i na nie odpowiada. To pozwala wzbogacić treść o istotne konteksty i informacje, których mogliśmy nie przewidzieć w strukturze nagłówków.

---

## Jak ręcznie zbudować bazę wiedzy RAG w Dify

Zanim przejdziemy do automatyzacji, warto zrozumieć proces, wykonując go ręcznie. Pozwoli to lepiej poznać mechanizmy działania platformy Dify.

### Krok 1: Wygenerowanie pliku z wiedzą

Pierwszym krokiem jest uruchomienie w Dify przepływu pracy (workflow), który przeszukuje internet, zbiera treści z najlepszych wyników, a następnie na ich podstawie generuje dwa zestawy pytań i odpowiedzi (dokładne i ogólne). Wynikiem tego procesu jest plik tekstowy (np. `kortyzol_rag.txt`), w którym każda para pytanie-odpowiedź jest oddzielona specjalnym separatorem (w tym przypadku znakiem `###`).

### Krok 2: Tworzenie nowej bazy wiedzy

W panelu Dify przejdź do sekcji **Wiedza**. Kliknij przycisk "Utwórz wiedzę", a następnie wybierz opcję importu danych z pliku tekstowego.

### Krok 3: Konfiguracja importu danych

Po wybraniu pliku `.txt` należy skonfigurować sposób jego przetwarzania:

#### Ustawienia podstawowe:
- **Separator bloków:** Ustaw separator, który został zdefiniowany w prompcie, czyli `###`. Dzięki temu Dify prawidłowo podzieli tekst na osobne fragmenty (chunki).
- **Maksymalna długość bloku:** 450-500 tokenów (ok. 2000 znaków)
- **Pozostałe opcje:** Pozostaw domyślne ustawienia

### Krok 4: Ustawienia zaawansowane bazy wiedzy

Po załadowaniu fragmentów, Dify rozpocznie ich indeksowanie. W tym momencie należy skonfigurować kluczowe parametry bazy wiedzy:

#### Parametry kluczowe:
- **Jakość wektoryzacji:** Zawsze wybieraj opcję **wysokiej jakości**, aby zapewnić najlepsze wyniki.
- **Tryb wyszukiwania:** Wybierz **wyszukiwanie hybrydowe**. Ten tryb, oprócz standardowego wyszukiwania wektorowego, wykorzystuje model typu "reranker", który dodatkowo analizuje i szereguje wyniki, aby znaleźć najbardziej trafne fragmenty.
- **Model rerankera:** Z listy wybierz model `base-multimodal-reranker-generic`.

### Krok 5: Testowanie bazy wiedzy

Skorzystaj z wbudowanego przycisku **Testowanie**. Wpisz dowolny nagłówek ze swojego planu (nawet jeśli jego forma jest nieco inna niż w bazie), a system pokaże, które fragmenty wiedzy zostały uznane za najbardziej pasujące. To doskonały sposób, aby zobaczyć reranking w akcji.

---

## Automatyzacja budowy RAG za pomocą Make.com

Ręczne tworzenie bazy jest pouczające, ale celem jest pełna automatyzacja. Poniższe kroki pokazują, jak skonfigurować scenariusz w Make, który wykona cały proces za Ciebie.

### Krok 1: Przygotowanie scenariusza w Make

Stwórz nowy scenariusz w Make, który będzie uruchamiany, gdy w arkuszu Google w kolumnie statusu (np. kolumna **N**) pojawi się wartość **"generuj"**. Scenariusz powinien pobierać z danego wiersza:

- Słowo kluczowe
- Język 
- Listę nagłówków do generacji

### Krok 2: Wywołanie przepływu pracy w Dify

Dodaj moduł API Dify, aby wywołać workflow generujący wiedzę. 

#### Konfiguracja modułu API:
- **Endpoint:** API workflow Dify
- **Metoda:** POST
- **Body (JSON):** 
  ```json
  {
    "keyword": "[pobrane_słowo_kluczowe]",
    "language": "[język]",
    "headings": "[lista_nagłówków]"
  }
  ```
- **Autoryzacja:** Klucz API z odpowiedniej aplikacji w Dify

### Krok 3: Wywołanie API bazy wiedzy Dify

Po otrzymaniu odpowiedzi z pierwszego modułu (zawierającej wiedzę dokładną i ogólną), dodaj nowy moduł **HTTP > Make a request**. Będzie on odpowiedzialny za dodanie wygenerowanej treści do Twojej bazy wiedzy w Dify.

#### Konfiguracja API bazy wiedzy:
- **URL:** Adres API wiedzy z **Dataset ID** Twojej bazy (znajdziesz w URL panelu Dify)
- **Metoda:** `POST`
- **Headers:** 
  - `Authorization: Bearer [KLUCZ_API_WIEDZY]`
  - `Content-Type: application/json`
- **Body (JSON):**
  ```json
  {
    "name": "[słowo_kluczowe]",
    "text": "[połączona_wiedza_ogólna_i_dokładna]"
  }
  ```

> **Ważne:** W udostępnionym szablonie automatyzacji znajdują się gotowe reguły przetwarzania, które zapewniają m.in. użycie trybu hybrydowego i wysokiej jakości wektoryzacji, tak jak w procesie ręcznym.

### Krok 4: Aktualizacja statusu w Google Sheets

Na końcu scenariusza dodaj moduł, który zaktualizuje status w arkuszu Google:
- Kolumna **P:** "OK" 
- Kolumna **N:** "gotowe"

To zasygnalizuje zakończenie procesu dla danego słowa kluczowego.

---

## Kluczowe komponenty systemu RAG

### 1. Chunking (Fragmentowanie)
- **Separator:** `###` dla prawidłowego podziału
- **Rozmiar fragmentu:** 450-500 tokenów (~2000 znaków)
- **Overlapping:** Zachowanie kontekstu między fragmentami

### 2. Wektoryzacja
- **Jakość:** Zawsze wysoka jakość dla najlepszych wyników
- **Model:** Embedding model zoptymalizowany pod język polski
- **Indeksowanie:** Automatyczne po dodaniu fragmentów

### 3. Wyszukiwanie hybrydowe
- **Wyszukiwanie wektorowe:** Semantyczne podobieństwo
- **Reranking:** Dodatkowa analiza trafności przez model `base-multimodal-reranker-generic`
- **Kombinacja:** Najlepsze z obu metod

### 4. Retrieval (Odzyskiwanie)
- **Top-K:** Liczba najlepszych fragmentów
- **Threshold:** Próg podobieństwa
- **Context window:** Rozmiar kontekstu dla generacji

---

## Typy wiedzy w systemie

### Wiedza dokładna
```
Pytanie: "Jakie funkcje pełni kortyzol?"
Odpowiedź: "Kortyzol pełni następujące funkcje:
1. Regulacja metabolizmu węglowodanów
2. Kontrola reakcji zapalnych
3. Odpowiedź na stres..."
```

### Wiedza ogólna
```
Pytanie: "Jak kortyzol wpływa na sen?"
Odpowiedź: "Wysoki poziom kortyzolu może zakłócać rytm snu przez:
- Blokowanie produkcji melatoniny
- Zwiększenie czujności w godzinach nocnych..."
```

---

## Przepływ procesu automatyzacji

```
Dane z nagłówków (etap 2)
    ↓
Status "generuj" w kolumnie N
    ↓
Trigger Make.com
    ↓
API call do Dify workflow
    ↓
Generacja wiedzy (dokładna + ogólna)
    ↓
API call do bazy wiedzy Dify
    ↓
Chunking + wektoryzacja + indeksowanie
    ↓
Status "gotowe" w arkuszu → Gotowość do brief generation
```

---

## Monitoring i optymalizacja

### Kontrola jakości
- **Testowanie fragmentów:** Regularne sprawdzanie odpowiedzi na typowe zapytania
- **Analiza pokrycia:** Czy wszystkie nagłówki mają odpowiednią wiedzę
- **Reranking performance:** Monitorowanie trafności wyszukiwania

### Optymalizacja parametrów
- **Rozmiar chunków:** Dostosowanie do długości typowych pytań
- **Threshold similarity:** Balans między precyzją a recall
- **Model rerankera:** Wybór najlepszego dla domeny

### Skalowanie
- **Batch processing:** Przetwarzanie wielu słów kluczowych
- **Deduplikacja:** Unikanie duplikatów w bazie
- **Archiwizacja:** Zarządzanie starymi fragmentami

---

## Podsumowanie

Po poprawnym skonfigurowaniu automatyzacji, cały proces budowy bazy wiedzy RAG będzie odbywał się bez Twojej ingerencji. Wystarczy, że dodasz nowe słowo kluczowe i nagłówki do arkusza oraz ustawisz odpowiedni status. Z tak przygotowaną bazą jesteśmy gotowi na kolejny etap: przygotowanie briefu do generacji treści.

**Korzyści systemu RAG:**
- **Eliminacja halucynacji:** Fakty oparte na zweryfikowanych źródłach
- **Kontekstowa wiedza:** Odpowiedzi dopasowane do konkretnych nagłówków
- **Skalowalność:** Automatyczne przetwarzanie dużej liczby tematów
- **Jakość:** Hybrydowe wyszukiwanie z rerankingiem
- **Kontrola:** Pełna transparentność źródeł i fragmentów

---

**Link do lekcji na platformie:** [SensAI Academy - Lekcja T8L05](https://learn.sensai.academy/next/public/lesson/352) 