## Wprowadzenie: Kluczowa rola danych w pracy z modelami językowymi
W tej lekcji zajmiemy się fundamentalnym aspektem pracy z modelami językowymi: przygotowaniem i pozyskiwaniem danych. Jest to proces o kluczowym znaczeniu, ponieważ korzystając z modeli poprzez API czy w ramach automatyzacji, często będziemy musieli dostarczyć im specyficzne dane lub przetworzyć istniejące przed ich użyciem.

Celem tej lekcji jest pokazanie, dlaczego dane są tak ważne, skąd je czerpać i w jakiej formie najlepiej dostarczać je modelom.

### Dlaczego modele językowe potrzebują od nas danych?
Modele językowe, mimo swojej zaawansowanej wiedzy nabytej podczas treningu, posiadają pewne ograniczenia:

1.  **Ograniczona wiedza (Knowledge Cutoff):**
    *   Modele są trenowane na danych dostępnych tylko do określonego momentu w czasie. Na przykład, w panelu Gemini AI Studio od Google można znaleźć informację "knowledge cut off: October 2024", co oznacza, że model nie posiada wiedzy o wydarzeniach po tej dacie.
    *   Bez dostarczenia aktualnych danych lub bez użycia przez model narzędzi (np. wyszukiwarki Google/Bing), nie będzie on w stanie odpowiadać na pytania dotyczące najnowszych zdarzeń.
    *   Modele nie aktualizują swojej wewnętrznej "wiedzy" na podstawie interakcji z użytkownikiem. Nowe, bardziej aktualne wersje modeli powstają w wyniku kolejnych procesów treningowych na nowszych danych.
2.  **"Kontekst jest królem" (Context is King):**
    *   Aby model mógł dostarczyć trafne i satysfakcjonujące odpowiedzi, wymaga odpowiednich danych kontekstowych.
    *   Wiele osób napotyka problemy, próbując np. generować nagłówki za pomocą ChatGPT bez dostarczania specyficznych danych. Modele nie były trenowane do każdego możliwego zadania z użyciem wszystkich możliwych danych, dlatego nasza pomoc w postaci kontekstu jest niezbędna.
    *   Dostarczenie aktualnych danych pozwala modelom odpowiadać na pytania dotyczące bieżących informacji.
3.  **Model jako procesor informacji, a nie tylko źródło:**
    *   Kluczowa zasada: nie polegaj wyłącznie na tym, co model "wie" z treningu. Skup się na tym, co mu dostarczysz.
    *   Każdy proces i automatyzacja powinna dzielić problem na jak najmniejsze części. Każda z tych części prawdopodobnie będzie wymagać dostarczenia specyficznych danych, na których model ma operować.

### Skąd pozyskiwać dane dla modeli językowych?
Istnieje kilka głównych źródeł danych:
*   **Web Scraping:** Proces automatycznego pobierania danych ze stron internetowych. Temu zagadnieniu poświęcona będzie oddzielna lekcja.
*   **Zewnętrzne serwisy API:** Możliwość skorzystania z interfejsów programistycznych udostępniających potrzebne dane, np. API z wynikami meczów sportowych. Dzięki temu model, mimo braku wiedzy o danym meczu, może napisać jego relację na podstawie dostarczonych przez API informacji.
*   **Pliki lokalne:** Dane, które możemy bezpośrednio przesłać do modelu.

### W jakiej formie dostarczać dane do modelu?
Format danych ma znaczenie dla efektywności i kosztów:
*   **Zwykły tekst (Plain Text):** Model sobie z nim poradzi, ale nie zawsze jest to najbardziej optymalna metoda.
*   **JSON (JavaScript Object Notation):** Modele dobrze radzą sobie z tym formatem, zwłaszcza jeśli dane pochodzą z innego API. Należy jednak pamiętać, że znaczniki struktury JSON (nazwy pól, nawiasy klamrowe) również zużywają tokeny, co przy dużych plikach JSON może wpływać na koszt.
*   **CSV (Comma-Separated Values):** Inny format tekstowy, z którym modele dobrze sobie radzą.
*   **XML (eXtensible Markup Language):** Czytelny dla modeli, ale podobnie jak JSON, jego znaczniki zużywają tokeny, co czyni go potencjalnie kosztownym.
*   **Markdown:** Jest to **zalecany format**. Oczyszczony tekst, który modele bardzo dobrze przyswajają. Producenci modeli językowych często rekomendują właśnie ten format.

W ramach tego kursu najczęściej będziemy korzystać ze zwykłego tekstu, JSON i Markdown.

### Część praktyczna: Demonstracja w Google Colab
Przejdziemy teraz do praktycznego przykładu w Google Colab. Pamiętaj, aby przed rozpoczęciem pracy skopiować notatnik na swój dysk, aby móc go edytować.

**Krok 1: Konfiguracja kluczy API**

W notatniku konfigurujemy klucze API dla: OpenAI, Jina, OpenRouter oraz Serpdata (usługa Senuto do pobierania wyników wyszukiwania Google, do której otrzymasz rabat w ramach kursu).

**Krok 2: Ilustracja ograniczeń modelu (Knowledge Cutoff)**

Zadajemy modelowi GPT-4o pytanie: "Jaka jest stopa bezrobocia w Polsce?". Model, mając odcięcie wiedzy np. na poziomie 2024 roku, odpowie informacją aktualną na czas swojego treningu (np. "Na koniec września 2023 roku stopa bezrobocia w Polsce wyniosła 5%"). Dla użytkownika szukającego aktualnych danych, taka odpowiedź jest nieprzydatna.

**Krok 3: Pozyskiwanie aktualnych danych**
*   **Wykorzystanie API Serpdata.io:** Pobieramy 10 najlepszych wyników wyszukiwania Google dla zapytania "Ile wynosi bezrobocie w Polsce" (język polski). Otrzymujemy listę adresów URL.
*   **Wykorzystanie Jina Reader:** Z pierwszych trzech adresów URL pobieramy treść stron w formacie Markdown. Zakładamy, że te treści zawierają aktualne informacje o stopie bezrobocia. (Alternatywnie, można by spróbować wyekstrahować dane bezpośrednio ze snippetów FAQ zwracanych przez API Serpdata, bez konieczności pobierania pełnych treści stron).

**Krok 4: Przetwarzanie wstępne danych – ekstrakcja faktów**

Zanim prześlemy całe trzy artykuły do modelu, warto je przetworzyć. W tym przypadku, wyekstrahujemy z nich kluczowe fakty dotyczące bezrobocia w Polsce.
*   Wysyłamy pobrane teksty (w Markdown) do modelu (np. GPT-4o mini, który jest tani i wystarczający do takich zadań) z prośbą o ekstrakcję samych faktów (liczby, konkretne stwierdzenia).
*   Wynikiem jest lista faktów, którą można zapisać np. w pandas DataFrame.
*   Ten krok ilustruje ogólną zasadę dzielenia problemów LLM na mniejsze etapy. Innym przykładem przetwarzania wstępnego mogłoby być przekształcenie wewnętrznej bazy wiedzy firmy na format pytań i odpowiedzi (Q&A), aby model lepiej sobie z nią radził.

**Krok 5: Zadawanie pytań z dostarczonym kontekstem**

Ponownie zadajemy pytanie: "Jaka jest stopa bezrobocia w Polsce?", ale tym razem w prompcie dołączamy wyekstrahowane wcześniej fakty jako kontekst: `Kontekst: Fakty wyekstraktowane z różnych źródeł: [lista faktów]`.
*   Model, korzystając z dostarczonych faktów, powinien teraz udzielić aktualnej odpowiedzi, np. "Bezrobocie w Polsce na koniec stycznia 2025 wynosi 5,4%".
*   Możemy dalej zawężać pytanie, np. "Jakie jest bezrobocie w Polsce w kwietniu 2025?". Model nadal będzie korzystał z tego samego zestawu faktów.
*   Porównując odpowiedź modelu z aktualnymi danymi (np. z szybkiego wyszukiwania w Google), możemy zweryfikować poprawność.

W ten sposób, dostarczając kontekst, umożliwiliśmy modelowi odpowiedź na pytanie dotyczące aktualnych wydarzeń, podobnie jak moglibyśmy to zrobić np. z wynikami wczorajszego meczu.

**Krok 6: Znaczenie formatu danych – Markdown vs. HTML**

Porównamy koszt i efektywność przesyłania danych w formacie HTML i Markdown.
*   Pobieramy treść tej samej strony (np. sensei.academy) raz jako surowy HTML, a raz jako Markdown (przy użyciu Jina Reader).
*   **Liczba tokenów:** Surowy HTML może zająć znacznie więcej tokenów (np. 53 000) niż czysty Markdown (np. 20 000).
*   **Koszt:** Przy założeniu, że 1000 tokenów kosztuje 0,20 USD, przetworzenie HTML kosztowałoby 10 USD, a Markdown 4 USD. W tym przykładzie Markdown jest o 60% tańszy. Różnica zależy od ilości znaczników HTML na stronie.
*   **"Szum" w prompcie:** Nadmiarowe znaczniki HTML mogą wprowadzać szum informacyjny, co potencjalnie może prowadzić do błędnego zrozumienia zapytania przez model.

Dlatego we wszystkich automatyzacjach i pracach z modelami będziemy preferować format Markdown.

### Dodatkowe źródła danych typu API
Polecam dwa serwisy ułatwiające dostęp do różnorodnych API:
*   **RapidAPI:** Jest to hub agregujący tysiące różnych API (np. do danych z LinkedIn, wyników sportowych). Standaryzuje sposób odpytywania API, więc po nauczeniu się obsługi jednego, łatwo korzystać z kolejnych.
*   **Apify:** Podobny do RapidAPI agregator API, oferujący dostęp do wielu źródeł danych.

### Podsumowanie i dalsze kroki
Zachęcam do samodzielnego przejścia przez przygotowany notatnik Google Colab, eksperymentowania z komórkami i wykorzystania zdobytej wiedzy we własnych projektach. Zrozumienie, jak pozyskiwać i przygotowywać dane, jest kluczowe dla efektywnej pracy z modelami językowymi. 