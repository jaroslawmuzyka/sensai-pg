# Wprowadzenie do generowania skryptów Python przy użyciu modeli językowych
W tej lekcji skupimy się na wykorzystaniu modeli językowych do generowania skryptów w Pythonie. Chociaż narzędzia no-code mogą zastępować potrzebę pisania skryptów, Python często okazuje się bardziej elastyczny, wydajny i szybszy, szczególnie przy przetwarzaniu danych lub zadaniach jednorazowych.

### Najlepsze modele językowe do programowania (Maj 2025)
Według społeczności programistycznej, następujące modele językowe wyróżniają się w zadaniach związanych z kodowaniem:
*   **Modele Claude:**
    *   Claude 3.7 Sonnet
    *   Claude 3.5 Sonnet
    (Dostępne np. bezpośrednio w Claude lub przez narzędzia takie jak Cursor).
*   **Modele Gemini:**
    *   Gemini 2.5 Flash Preview
    *   Gemini 2.5 Pro Preview

Modele OpenAI, jak np. GPT-4.1, choć ulepszone, generalnie rzadziej są pierwszym wyborem do złożonych zadań programistycznych, ale mogą sobie poradzić z prostszymi skryptami.

### Krok 1: Definiowanie zasad (instrukcji systemowych) dla modelu językowego
Aby efektywnie generować kod, musimy najpierw przekazać modelowi językowemu odpowiednie zasady i kontekst działania. Pomocna może być strona **Cursor Directory**, która agreguje gotowe prompty systemowe dla różnych technologii, w tym Pythona.

**Jak wykorzystać instrukcje systemowe:**
*   **Custom GPTs (OpenAI):** Wklej wybrane lub zmodyfikowane instrukcje systemowe (np. z Cursor Directory, z dodatkiem informacji o programowaniu w Google Colab) w polu konfiguracji instrukcji dla Twojego Custom GPT.
*   **Claude Projects:** Stwórz nowy projekt w Claude i w opisie projektu lub dedykowanym miejscu na instrukcje systemowe wprowadź swoje zasady.
*   **Google Gemini:** Skorzystaj z ikonki "System instruction" (lub analogicznej funkcji), aby wkleić przygotowane zasady programowania.

Możesz również znaleźć gotowe GPTs specjalizujące się w programowaniu, np. takie, które mają wgraną dokumentację wielu bibliotek Pythonowych (link do przykładowego GPT znajduje się w materiałach kursu).

### Krok 2: Kluczowa zasada – dzielenie projektów na mniejsze części
Podczas generowania skryptów Python za pomocą modeli językowych, niezwykle ważne jest, aby rozbijać większe zadania na małe, zarządzalne fragmenty kodu. Traktuj każdy skrypt jak mały mikroserwis.

**Dlaczego?** Modele językowe radzą sobie znacznie lepiej z generowaniem i debugowaniem krótkich, skoncentrowanych fragmentów kodu. Próba wygenerowania jednego, dużego skryptu obsługującego wiele operacji szybko prowadzi do problemów z zarządzaniem kodem i błędami.

**Przykład:** Projekt generowania nagłówków można podzielić na:
1.  Skrypt do keyword researchu.
2.  Skrypt do ekstrakcji faktów z treści.
3.  Skrypt do generowania nagłówków na podstawie zebranych danych.
Każdy z tych kroków powinien być osobnym skryptem, np. uruchamianym w Google Colab.

### Krok 3: Proces generowania skryptu Python – przykład praktyczny
Załóżmy, że chcemy użyć Gemini 2.5 Pro do wygenerowania skryptu.
1.  **Dokładnie opisz cel skryptu:**
    Przykład promptu:
    ```
    Chciałbym skrypt, który pobierze wyniki top 10 na określone słowo kluczowe z API SerpData IO.
    ```
2.  **Dostarcz kontekst i przykłady:**
    *   Link do dokumentacji API (np. SerpData.io).
    *   Przykładowe zapytanie do API (np. fragment kodu w Pythonie ze strony SerpData.io).
    *   Przykładowa odpowiedź API (struktura JSON).
    *   Dodatkowe wymagania:
        ```
        Chciałbym, aby skrypt zapisywał do pandas DataFrame top 10 wyników z tablicy (lub obiektu) 'organic', które mają pozycję (np. pole 'position') mniejszą niż 10. Programuję w Google Colab, więc wykorzystaj opcje interaktywnych formularzy do ustawienia zmiennych (np. klucza API i słowa kluczowego).
        ```
3.  **Poproś o plan działania (bardzo ważne!):**
    Dodaj do promptu (lub instrukcji systemowej):
    ```
    Zanim wygenerujesz skrypt, wygeneruj plan działania krok po kroku i opis działania poszczególnych części. Po mojej akceptacji planu, wygeneruj kompletny skrypt.
    ```
    To da Ci pewność, że model prawidłowo zrozumiał zadanie.
4.  **Zatwierdź plan:**
    Model powinien przedstawić plan, np.:
    1.  Instalacja potrzebnych bibliotek (np. `requests`, `pandas`).
    2.  Import bibliotek.
    3.  Definiowanie pól wejściowych dla klucza API i słowa kluczowego (formularze Colab).
    4.  Przygotowanie zapytania do API SerpData.
    5.  Wykonanie zapytania API.
    6.  Przetwarzanie odpowiedzi JSON.
    7.  Ekstrakcja i filtrowanie wyników organicznych.
    8.  Tworzenie ramki danych (DataFrame) z wynikami.
    9.  Wyświetlanie ramki danych.
    Jeśli plan jest zgodny z oczekiwaniami, potwierdź go.
5.  **Wygeneruj skrypt:** Po akceptacji planu, model wygeneruje kod.

### Krok 4: Uruchamianie i debugowanie skryptu (np. w Google Colab)
1.  Skopiuj wygenerowany skrypt i wklej go do nowego notatnika Google Colab.
2.  Uruchom komórki, podając wymagane dane (np. klucz API SerpData, słowo kluczowe).
3.  **Obsługa błędów:**
    Jeśli skrypt zwróci błąd:
    *   Skopiuj komunikat błędu oraz relevantne fragmenty z konsoli (np. otrzymaną odpowiedź API, jeśli jest widoczna).
    *   Wklej te informacje z powrotem do modelu, np.: `Otrzymuję następujący błąd: [tutaj wklej błąd i logi]. Wygląda na to, że klucz zawierający wyniki organiczne w odpowiedzi JSON jest inny niż zakładałeś. Sprawdź proszę strukturę odpowiedzi.`
    *   Model powinien zaproponować poprawkę. Czasem potrzebnych jest kilka iteracji.
    **Uwaga dot. kluczy API:** Staraj się nie wklejać kluczy API bezpośrednio do promptów. Korzystaj z mechanizmów zarządzania sekretami (np. w Google Colab). Modele językowe mogą próbować anonimizować klucze, które wykryją w treści.

Po udanym uruchomieniu i ewentualnym debugowaniu, skrypt powinien wyświetlić np. tabelę z wynikami top 10.

### Krok 5: Zapisywanie pracy i kontekstu (np. Claude Projects)
Jeśli pracujesz nad bardziej złożonym projektem, który wymaga wielu interakcji z modelem, warto korzystać z funkcji projektów (np. w Claude):
*   Stwórz nowy projekt (np. "Skrypty SerpData").
*   W instrukcjach systemowych projektu zapisz swoje standardowe zasady programowania w Pythonie i specyfikę pracy w Colab.
*   Możesz wgrywać pliki (np. z przykładowymi danymi, fragmentami kodu), aby model miał stały dostęp do kontekstu.

Dzięki temu model będzie lepiej dostosowany do Twoich potrzeb przy każdej kolejnej interakcji w ramach tego projektu.

### Podsumowanie
Generowanie skryptów Python przy użyciu modeli językowych, takich jak Claude czy Gemini, staje się coraz prostsze i bardziej efektywne. Kluczem jest dostarczanie jasnych instrukcji, dzielenie zadań na mniejsze części oraz iteracyjne podejście do debugowania. Zachęcam do eksperymentowania, ponieważ umiejętność ta znacznie ułatwi i przyspieszy wiele zadań programistycznych. 