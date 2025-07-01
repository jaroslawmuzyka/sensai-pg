# T8L02: Tworzenie treści z AI - Budowa wiedzy

Ta lekcja rozpoczyna serię poświęconą budowie profesjonalnego procesu generowania treści z użyciem sztucznej inteligencji. Zaczynamy od fundamentalnego etapu: tworzenia solidnej bazy wiedzy. Dowiesz się, jak zbierać i przetwarzać informacje z różnych źródeł, aby przygotować fundament pod wysokiej jakości artykuł.

## 📂 Materiały do pobrania

[📂 Pobierz plik workflow Dify do lekcji](https://learn.sensai.academy/download.php?lfid=65)

## Powiązane automatyzacje

Lekcja wykorzystuje automatyzacje z folderu `Automatyzacje/`:
- **[SEO3.0] Budowa bazy wiedzy.yml** - główny workflow do budowy bazy wiedzy
- **SEO 3.0 - [1] Budowa wiedzy.blueprint.json** - szablon Blueprint dla procesu budowy wiedzy

## Cel i etapy procesu generacji treści

Celem jest stworzenie kompletnego, zautomatyzowanego procesu do generowania treści. Każdy proces, niezależnie od tematu, składa się z kilku kluczowych etapów:

1. **Budowa wiedzy:** Zbieranie informacji z zewnętrznych źródeł, ponieważ modele językowe są procesorami języka, a nie źródłami wiedzy.
2. **Tworzenie struktury nagłówków:** Kluczowy etap decydujący o jakości, kontekście i semantyce finalnego tekstu. Zła struktura może sprawić, że cały artykuł będzie bezwartościowy.
3. **Generacja treści:** Wykorzystanie zebranej wiedzy do tworzenia tekstu dla poszczególnych nagłówków (proces RAG – Retrieval-Augmented Generation).
4. **Tworzenie briefu generacyjnego:** Wzbogacenie struktury o konkretne frazy kluczowe, pytania i informacje, które muszą znaleźć się w każdej sekcji. To tak, jakby dać copywriterowi szczegółowe wytyczne zamiast samych nagłówków.
5. **Finalna generacja, humanizacja i formatowanie:** Ostatni szlif nadający treści ostateczny kształt.

## Narzędzia i założenia wstępne

Wszystkie prezentowane w lekcji kroki opierają się na narzędziu **Deefai**. Gotowe przepływy pracy (workflowy) są dostępne do importu pod lekcją.

### Wymagane dane wejściowe:

- **Fraza kluczowa lub temat:** Na przykład `co to jest kortyzol?`.
- **Język:** Definiuje język, w którym pozyskiwana jest wiedza i frazy (np. `polski`).
- **(Opcjonalnie, ale zalecane) Treść AI Overview:** Ręcznie skopiowana treść z panelu AI Overview w wynikach wyszukiwania Google. Jest to ważne, ponieważ narzędzia nie są w stanie automatycznie pobrać pełnej, rozwiniętej treści.

## Krok po kroku: Budowa bazy wiedzy w Deefai

Proces pozyskiwania wiedzy jest pierwszym i najważniejszym elementem całego workflow. Poniżej omówiono jego logiczną strukturę i działanie poszczególnych bloków.

### 1. Pobieranie danych z wyników wyszukiwania (SerpData)

Proces rozpoczyna się od zapytania do narzędzia **SerpData**, które pobiera dane bezpośrednio z wyników wyszukiwania Google dla podanej frazy kluczowej.

- **Co jest pobierane:** Lista 10 najlepszych wyników organicznych (Top 10) oraz, jeśli istnieje, zawartość panelu **AI Overview**.
- **Kluczowe informacje:** Narzędzie wyciąga nie tylko adresy URL z wyników organicznych, ale także adresy stron, które posłużyły Google do syntezy odpowiedzi w AI Overview. To cenne źródła, ponieważ są już "zaakceptowane" przez AI.
- **Konfiguracja:** W tym bloku można zdefiniować geolokalizację i język wyszukiwania (np. `hl=pl` dla języka polskiego, `gl=pl` dla Polski).

### 2. Przetwarzanie i czyszczenie listy URL

Surowe dane z SerpData są następnie przetwarzane przez specjalny skrypt. Jego celem jest stworzenie jednej, unikalnej listy adresów URL do dalszej analizy. Skrypt usuwa duplikaty i ogranicza listę do 25 adresów (standardowy limit w Deefai).

### 3. Pobieranie treści ze stron (Crawling)

Następnie proces iteruje po każdym adresie URL z listy, aby pobrać treść strony internetowej. Wykorzystywany jest do tego blok **Gina**.

- **Równoległość:** Aby przyspieszyć proces, Deefai pozwala na równoległe przetwarzanie kilku stron jednocześnie (w tym przypadku 4 wątki).
- **Obsługa błędów:** To kluczowy element. Jeśli pobranie którejś ze stron się nie powiedzie (np. z powodu zabezpieczeń), proces nie jest przerywany. Zamiast tego zwracana jest pusta wartość (spacja), co pozwala kontynuować pracę z pozostałymi źródłami.

**Wskazówka:** Gina pobiera całą zawartość strony, włączając w to nawigację i inne "szumy". Dla uzyskania czystszych danych i lepszych wyników, zaawansowani użytkownicy mogą zastąpić ten blok własnym, bardziej zaawansowanym crawlerem.

### 4. Analiza treści i ekstrakcja wiedzy (praca AI)

Po zebraniu treści ze wszystkich źródeł, workflow rozdziela się na cztery równoległe gałęzie, w których AI wykonuje różne zadania analityczne.

**Usuwanie brandów:** Na początku procesu AI identyfikuje i ekstrahuje nazwy marek (np. Medicover, Apteka Melisa) z domen, aby uniknąć umieszczania ich w generowanej, neutralnej treści.

- **Gałąź 1: Ekstrakcja słów kluczowych i encji.** AI analizuje wszystkie teksty w poszukiwaniu najważniejszych słów kluczowych i encji silnie powiązanych z głównym tematem (np. "kortyzol"). Proces jest dwuetapowy: najpierw ekstrakcja, a potem filtrowanie i usuwanie duplikatów dla zapewnienia wysokiej jakości.

- **Gałąź 2: Ekstrakcja bazy wiedzy (trójniki semantyczne).** To najważniejsza część. AI przekształca tekst w ustrukturyzowane dane w formie trójników semantycznych (`podmiot-orzeczenie-dopełnienie`, np. `kortyzol-jest-hormonem stresu`). Zapewnia to głęboką, szczegółową wiedzę, która będzie podstawą do tworzenia nagłówków i treści. Ten proces jest wykonywany zarówno na treściach z pobranych stron, jak i na wklejonej ręcznie treści AI Overview.

- **Gałąź 3: Ekstrakcja nagłówków konkurencji.** AI wyciąga nagłówki H2 i H3 ze stron konkurencji. Będą one przydatne w późniejszym etapie planowania struktury artykułu.

- **Gałąź 4: Tworzenie grafu wiedzy (Knowledge Graph).** Używając promptu od Senuto, AI tworzy graf wiedzy, który daje szerszy, "big picture" obraz tematu. Uzupełnia on szczegółowe trójniki semantyczne o relacje i szerszy kontekst.

### 5. Łączenie i finalizowanie wyników

Na końcu wszystkie dane z równoległych gałęzi są łączone. Otrzymujemy kompletny zestaw informacji gotowy do wykorzystania w kolejnym kroku.

## Wyniki etapu budowy wiedzy

Po zakończeniu tego workflow otrzymujemy cztery kluczowe zestawy danych:

1. **Zestaw słów kluczowych:** Lista fraz i encji, które muszą znaleźć się w tekście.
2. **Graf informacji (trójniki semantyczne):** Czysta, ustrukturyzowana wiedza na dany temat. To fundament merytoryczny artykułu.
3. **Nagłówki konkurencji:** Inspiracja do budowy własnej, kompleksowej struktury.
4. **Graf wiedzy (Senuto):** Ogólny obraz tematu, pomocny w zrozumieniu relacji między pojęciami.

Z tak przygotowaną bazą wiedzy jesteśmy gotowi, aby przejść do kolejnej lekcji, w której zajmiemy się budową optymalnej struktury nagłówków dla naszego artykułu.

## Linki i zasoby

- **Platforma lekcji:** [https://learn.sensai.academy/next/public/lesson/346](https://learn.sensai.academy/next/public/lesson/346)
- **Powiązane automatyzacje:** 
  - [SEO3.0] Budowa bazy wiedzy.yml
  - SEO 3.0 - [1] Budowa wiedzy.blueprint.json
- **Graf wiedzy Senuto:** Wykorzystuje prompt [Topical_Map_Generator.md](../../../Prompty/Topical_Map_Generator.md) 