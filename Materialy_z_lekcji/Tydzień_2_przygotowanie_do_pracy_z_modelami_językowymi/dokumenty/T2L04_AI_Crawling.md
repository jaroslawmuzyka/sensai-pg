# Wprowadzenie: Narzędzia do przygotowywania danych dla modeli językowych
W tej lekcji poznasz trzy kluczowe narzędzia, które znacząco ułatwiają dostosowywanie danych ze stron internetowych, tak aby były one łatwo przetwarzane przez modele językowe. Zrozumienie ich działania jest istotne, ponieważ będą one często wykorzystywane w kolejnych częściach kursu.

### Narzędzie 1: Jina Reader
**Jina Reader** to narzędzie stworzone przez firmę Jina, specjalizującą się w rozwiązaniach AI. Jest to jedno z moich ulubionych narzędzi, często wykorzystywane w automatyzacjach.

**Jak działa Jina Reader?**
*   Podstawowa funkcja: Po podaniu adresu URL (np. poprzez interfejs webowy lub API wpisując `r.jina.ai/adres-strony.pl`), narzędzie zwraca treść danej strony internetowej w formacie **Markdown**.
*   Format Markdown jest znacznie bardziej przyjazny dla modeli językowych niż surowy HTML, który często zawiera wiele zbędnych tagów, zwiększających koszt przetwarzania przez modele.
*   Proces: Wysyłasz URL -> Jina Reader przetwarza stronę -> Otrzymujesz czysty tekst w Markdown (zawierający tytuł, URL źródłowy i treść).

**Dodatkowe funkcje Jina Reader:**
*   **Wyszukiwarka:** Wpisując `s.jina.ai/słowo-kluczowe`, Jina Reader może zwrócić listę adresów URL powiązanych z danym tematem.
*   **Czytanie obrazków (OCR):** Jeśli na stronie znajdują się obrazy, Jina Reader potrafi dostarczyć ich tekstowy opis, co pomaga w pełniejszym zrozumieniu kontekstu strony.
*   **Czytanie plików PDF:** Narzędzie potrafi przetwarzać treść z plików PDF dostępnych pod podanym adresem URL.
*   **API i parametry:**
    *   Możliwość wyboru formatu wyjściowego (Markdown, HTML, screenshot całej strony, "page shot").
    *   Ustawienie limitu czasu (timeout) na przetworzenie strony.
    *   Crawlowanie treści z określonych selektorów CSS.
    *   Oczekiwanie na załadowanie się dynamicznych elementów strony.
    *   Możliwość wykorzystania serwerów proxy.

**Koszt:** Jina Reader jest narzędziem płatnym, ale jego koszt jest relatywnie niski. Przykładowo, za 200 dolarów można uzyskać możliwość przetworzenia 11 miliardów tokenów, co odpowiada wielokrotnemu przetworzeniu treści całej Wikipedii.

Osobiście cenię to narzędzie za jego szybkość, sprawność i niezawodność.

### Narzędzie 2: Firecrawl
**Firecrawl** to popularne narzędzie do web scrapingu, które zdobywa coraz większe uznanie.

**Główne cechy i różnice względem Jina Reader:**
*   W przeciwieństwie do Jina Reader, gdzie podajemy pojedynczy URL, Firecrawl potrafi **scrawlować całą domenę**.
*   Podobnie jak Jina, konwertuje treść stron do formatu Markdown.

**Kluczowa funkcja: LLM Extract**
*   Firecrawl integruje modele językowe bezpośrednio w procesie scrapingu, umożliwiając ekstrakcję konkretnych informacji bez potrzeby manualnego definiowania selektorów CSS czy XPath.
*   Jak to działa:
    1.  Pobierasz dane do formatu Markdown.
    2.  Definiujesz schemat danych, które chcesz wyekstrahować (np. zmienna `isPolishCompany` typu string).
    3.  Firecrawl używa swojego wewnętrznego modelu językowego, aby przeanalizować treść strony i na jej podstawie wypełnić zdefiniowany schemat.
*   **Przykład:** Chcesz sprawdzić, czy firma stojąca za domeną `senuto.com` pochodzi z Polski. Firecrawl pobierze treść, a jego LLM przeanalizuje ją pod kątem danych adresowych, numeru NIP itp., a następnie zwróci np. `true` lub `false` dla zmiennej `isPolishCompany`. Dla `disney.com` prawdopodobnie zwróciłby `false`.
*   **Zastosowanie w SEO:** Możliwość masowego wyciągania informacji takich jak autorzy artykułów blogowych czy tagi, nawet jeśli nie są one umieszczone w jednolity sposób na różnych stronach.

**Firecrawl vs. Jina Reader + zewnętrzne API LLM:** Firecrawl ma funkcję ekstrakcji LLM wbudowaną natywnie. Korzystając z Jina Reader, musielibyśmy pobrać treść, a następnie osobno wysłać ją do API np. OpenAI z odpowiednim promptem, aby uzyskać podobny efekt.

**Dostępność:**
*   **Open Source:** Repozytorium Firecrawl jest dostępne na GitHubie, co pozwala na samodzielną instalację i hosting.
*   **Wersja komercyjna:** Dostępna jest również wersja przeglądarkowa z planami cenowymi, działająca podobnie do innych popularnych crawlerów na rynku.

### Narzędzie 3: Crawl4AI
**Crawl4AI** to stosunkowo nowe narzędzie, będące konkurentem dla Firecrawl, oferujące zbliżone funkcjonalności.

**Główne cechy:**
*   Podobnie jak Firecrawl, jest to narzędzie **open source**. W momencie nagrywania tej lekcji nie posiadało jeszcze wersji komercyjnej (stan na maj 2025).
*   Twórcy chwalą się, że Crawl4AI jest **znacznie szybszy** od Firecrawl (według ich benchmarków nawet dwukrotnie).
*   Można go uruchomić na własnym serwerze (np. przez Docker) lub korzystać z niego jako biblioteki Python w środowiskach takich jak Google Colab.

**Przykładowe funkcje (demonstracja w Google Colab):**
*   **Pobieranie treści do Markdown:** Analogicznie do Jina Reader i Firecrawl, można pobrać treść strony (np. `senuto.com.pl`) w formacie Markdown. Korzystając z Google Colab, jest to darmowe.
    ```python
    # Przykładowy kod w Pythonie (Google Colab)
    # Instalacja biblioteki
    # !pip install crawl4ai
    # from crawl4ai import WebCrawler
    # crawler = WebCrawler()
    # crawled_data = crawler.crawl(url='https://senuto.com.pl')
    # print(crawled_data.markdown)
    ```
*   **Obsługa proxy:** Przydatne przy intensywnym crawlowaniu lub analizie wyników wyszukiwania.
*   **Ekstrakcja danych strukturyzowanych (JSON) z wykorzystaniem LLM:**
    1.  Konfigurujesz model językowy, który ma być użyty do ekstrakcji (np. GPT-4.0, używając własnego klucza API).
    2.  Definiujesz prompt, który precyzuje, jakie informacje mają zostać wyekstrahowane i w jakim formacie.
    3.  Crawl4AI pobiera treść strony do Markdown, a następnie wysyła ją wraz z Twoim promptem do skonfigurowanego modelu LLM.
    4.  Model analizuje treść i zwraca dane w ustrukturyzowanym formacie JSON.
*   **Przykład ekstrakcji cenników:** Masz listę 100 stron z cennikami konkurencji. Każda strona ma inną strukturę. Możesz użyć Crawl4AI, aby dla każdej strony:
    *   Pobrać treść.
    *   Wysłać do GPT-4.0 z promptem: "Wyekstrahuj nazwy pakietów, ich ceny, cykl płatności (miesięczny/roczny) oraz czy jest to pakiet podstawowy czy dodatek (add-on)".
    *   Otrzymać dane w formacie JSON, np.:
        ```json
        [
            { "packageName": "Lite", "price": 39, "currency": "EUR", "paymentCycle": "miesięcznie", "type": "pakiet", "billing": "miesięczna" },
            { "packageName": "Lite", "price": 32, "currency": "EUR", "paymentCycle": "rocznie", "type": "pakiet", "billing": "roczna" },
            { "packageName": "SERP Analysis", "price": 12, "currency": "EUR", "paymentCycle": "miesięcznie", "type": "add-on", "billing": "miesięczna" }
        ]
        ```
    To ilustruje "nową erę crawlowania", gdzie modele językowe pomagają w łatwy sposób strukturyzować nieustrukturyzowane dane.

Link do notatnika Google Colab z przykładami użycia Crawl4AI będzie dostępny w materiałach do lekcji.

### Automatyzacja w Make.com (podejście No-Code)
Pokażę teraz, jak osiągnąć podobne rezultaty (pobieranie treści, analiza LLM, zapis danych) bez pisania kodu, używając platformy automatyzacyjnej **Make.com**.

**Cel automatyzacji:** Stworzyć crawler, który dla listy URLi:
1.  Pobierze treść strony.
2.  Określi, w jakim mieście zlokalizowana jest firma.
3.  Przygotuje krótki opis działalności firmy.

**Kroki scenariusza w Make.com:**
1.  **Google Sheets - Wczytaj dane:** Moduł pobiera listę adresów URL ze wskazanego arkusza Google Sheets.
2.  **HTTP - Pobierz treść z Jina Reader API:**
    *   Dla każdego URL z arkusza, wykonaj zapytanie GET do API Jina Reader (`r.jina.ai/{URL_z_Google_Sheets}`).
    *   Skonfiguruj autoryzację, używając swojego klucza API Jina Reader (dostępny na `r.jina.ai/reader` w zakładce API po opłaceniu usługi).
    *   Moduł zwraca treść strony w formacie Markdown.
3.  **OpenAI - Analiza treści:**
    *   Użyj modelu GPT-4O mini (tani, z dużym oknem kontekstowym 128k tokenów).
    *   **Rola System:** Zdefiniuj zadanie dla modelu, np.: "Jesteś analitykiem biznesowym. Przeanalizuj dostarczoną treść strony internetowej. Zidentyfikuj miasto, w którym firma ma siedzibę, określ typ działalności firmy i przygotuj zwięzły opis jej działalności. Zwróć dane w formacie JSON: `{\"description\": \"opis firmy\", \"location\": {\"city_name\": \"nazwa miasta\"}}`". (Prompt do wykorzystania będzie w materiałach).
    *   **Rola User:** Przekaż treść strony (Markdown) uzyskaną z Jina Reader w poprzednim kroku.
    *   W Make.com skonfiguruj moduł OpenAI, aby automatycznie parsował odpowiedź JSON (np. opcje `response_format: map`, `JSON object`, `Parse JSON response: true`).
4.  **Google Sheets - Zapisz wyniki:**
    *   Zaktualizuj odpowiedni wiersz w arkuszu Google Sheets.
    *   Zapisz wygenerowany opis firmy (`Description`) i zidentyfikowaną nazwę miasta (`City Name`) w odpowiednich kolumnach.

**Rezultat:** Automatyzacja przechodzi przez listę URLi, analizuje treść stron i uzupełnia arkusz Google Sheets o opisy firm i ich lokalizacje. Przykładowo, dla Senuto może wygenerować opis "Senuto to platforma oferująca zaawansowane narzędzia SEO i analizy treści" oraz zidentyfikować Warszawę jako miasto. Dla whitepress.com może wskazać Bielsko-Białą.

Taki proces nazywa się **data enrichment** (wzbogacanie danych) i jest bardzo przydatny np. do kategoryzacji domen, identyfikacji branż, lokalizacji itp. Plik z gotową automatyzacją Make.com będzie dostępny w materiałach do lekcji, abyś mógł/mogła go zaimportować i od razu używać.

### Podsumowanie
W tej lekcji omówiliśmy trzy potężne narzędzia do przygotowywania danych dla modeli językowych: **Jina Reader**, **Firecrawl** oraz **Crawl4AI**. Dodatkowo, zobaczyłeś/aś, jak podobne zadania można realizować w podejściu no-code przy użyciu platformy **Make.com**. Te narzędzia i techniki będą fundamentem dla wielu działań omawianych w kolejnych lekcjach. 