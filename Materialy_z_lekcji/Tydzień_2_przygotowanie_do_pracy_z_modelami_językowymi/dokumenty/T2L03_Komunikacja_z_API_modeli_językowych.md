# Przewodnik po Komunikacji z Modelami Językowymi przez API

Ten przewodnik krok po kroku pomoże Ci zrozumieć podstawy komunikacji z modelami językowymi (LLM) poprzez API. Dowiesz się, czym jest API, jak z niego korzystać, jakie są kluczowe koncepcje oraz jakie zaawansowane funkcje oferują poszczególni dostawcy modeli. Zrozumienie tych zagadnień jest kluczowe dla tworzenia automatyzacji i pracy z modelami językowymi w sposób programistyczny.

## Wprowadzenie: Czym jest komunikacja z modelami językowymi przez API?
Większość automatyzacji i zaawansowanych zastosowań modeli językowych opiera się na komunikacji poprzez API (Interfejs Programowania Aplikacji). Pozwala to na integrację modeli z własnymi aplikacjami, skryptami (np. w Pythonie) czy narzędziami do automatyzacji takimi jak Make czy N8N. Ta lekcja przeprowadzi Cię przez podstawowe koncepcje i praktyczne aspekty korzystania z API różnych modeli językowych.

## Zanim zaczniesz: Playgroundy jako wstęp do API
Każdy dostawca modeli językowych udostępnia tzw. **Playground**. Jest to interfejs graficzny, który pozwala na testowanie zapytań do API bez pisania kodu. Można tam:
*   Wybrać model.
*   Skonfigurować parametry zapytania (np. `system message`).
*   Wysłać prompt.
*   Wygenerować kod potrzebny do odtworzenia tego samego zapytania w wybranym języku programowania.
*   Zazwyczaj w takich serwisach generuje się również klucze API.

**Przykłady Playgroundów:**
*   **OpenAI Playground:** Umożliwia interakcję z modelami OpenAI i generowanie kluczy API (zakładka "API keys" w panelu użytkownika).
*   **Google AI Studio:** Analogiczne narzędzie dla modeli Google. Aby wygenerować klucz API, konieczne może być wcześniejsze założenie projektu w Google Cloud.

Playgroundy są świetnym miejscem do przetestowania konfiguracji zapytania przed implementacją w kodzie.

## Krok 1: Przygotowanie środowiska w Google Colab
Do praktycznej nauki komunikacji z API wykorzystamy interaktywny notatnik Google Colab.

**1. Instalacja potrzebnych bibliotek:**
Na początku pracy z notatnikiem konieczne jest zainstalowanie bibliotek, które umożliwią komunikację z API różnych dostawców (OpenAI, Google Generative AI, Anthropic, itp.) oraz obsługę żądań HTTP.
```python
# Przykładowa komenda instalacji (w notatniku Colab)
# !pip install openai google-generativeai anthropic requests
```
Pamiętaj, że biblioteki te należy instalować za każdym razem, gdy uruchamiasz notatnik od nowa.

**2. Konfiguracja kluczy API:**
Aby móc komunikować się z API, potrzebujesz unikalnych kluczy dostępowych. W notatniku Google Colab znajdziesz linki do miejsc, gdzie można wygenerować klucze dla:
*   OpenAI
*   Gemini (Google)
*   Claude (Anthropic)
*   Gina
*   OpenRouter

Wygenerowane klucze należy zapisać w Google Colab jako tzw. "Secrets". Nazwy sekretów muszą odpowiadać tym użytym w kodzie notatnika. Dzięki temu klucze są przechowywane bezpiecznie i dostępne we wszystkich Twoich notatnikach bez potrzeby ponownej konfiguracji.

## Krok 2: Zrozumienie podstaw API

**Co to jest API?**
API (Application Programming Interface) to zestaw reguł i protokołów umożliwiający różnym aplikacjom komunikację między sobą. W kontekście modeli językowych, API pozwala Twojemu programowi wysyłać zapytania (prompty) do serwera dostawcy modelu i otrzymywać odpowiedzi.

**Jak działa HTTP API?**
Komunikacja odbywa się zazwyczaj poprzez protokół HTTP i przebiega w następujących krokach:
1.  **Klient tworzy żądanie HTTP:** Twoja aplikacja lub skrypt formułuje zapytanie.
2.  **Klient wysyła żądanie:** Żądanie jest wysyłane na określony adres serwera API.
3.  **Serwer odbiera żądanie:** Serwer dostawcy modelu otrzymuje Twoje zapytanie.
4.  **Serwer weryfikuje żądanie:** Sprawdzana jest poprawność żądania, w tym autentykacja (np. czy dołączono prawidłowy klucz API).
5.  **Serwer tworzy odpowiedź:** Model językowy przetwarza Twój prompt i generuje odpowiedź.
6.  **Serwer wysyła odpowiedź:** Odpowiedź jest odsyłana do Twojej aplikacji.
7.  **Klient odbiera odpowiedź:** Twoja aplikacja otrzymuje dane z API.

**Podstawowe koncepcje API:**
*   **Endpoint:** Specyficzny adres URL, do którego kierowane są żądania API. Np. dla OpenAI może to być `api.openai.com/v1/chat/completions`.
*   **Metody HTTP:**
    *   **POST:** Najczęściej używana metoda do wysyłania danych (np. promptu) do serwera w celu ich przetworzenia.
    *   **GET:** Służy do pobierania danych z serwera (np. listy dostępnych modeli).
*   **Statusy HTTP serwera:** Kody informujące o wyniku żądania.
    *   `200 OK`: Żądanie zakończone sukcesem.
    *   `400 Bad Request`: Błędne żądanie (np. przekroczenie limitu tokenów).
    *   `401 Unauthorized`: Błąd autentykacji (np. nieprawidłowy klucz API).
    *   `404 Not Found`: Nie znaleziono zasobu (np. błędny endpoint).
*   **Format danych JSON (JavaScript Object Notation):** Większość API, w tym te od modeli językowych, komunikuje się przy użyciu formatu JSON. Jest to standardowy sposób strukturyzacji danych. Twoim zadaniem często będzie poprawne sformatowanie zapytania w JSON i przetworzenie odpowiedzi w tym samym formacie.

## Krok 3: Sposoby komunikacji z API modeli językowych
Istnieją dwa główne podejścia do komunikacji z API:

**1. Bezpośrednie żądania HTTP:**
Polega na samodzielnym konstruowaniu i wysyłaniu żądań HTTP (np. przy użyciu biblioteki `requests` w Pythonie). Wymaga to ręcznej obsługi wszystkich aspektów komunikacji, w tym autentykacji i obsługi błędów.

**2. Korzystanie z bibliotek SDK (Software Development Kit):**
Dostawcy modeli językowych często udostępniają dedykowane biblioteki (SDK) dla popularnych języków programowania (np. Python). Biblioteki te znacznie upraszczają komunikację, oferując gotowe funkcje do wysyłania zapytań, obsługi autentykacji i błędów. **Zazwyczaj jest to zalecane podejście.**
*   **OpenAI SDK:** Umożliwia łatwą integrację z modelami OpenAI.
*   **Google Generative AI SDK:** Biblioteka do komunikacji z modelami Gemini. Należy zwrócić uwagę na różnice między usługami Vertex AI a Google Generative AI.
*   **Anthropic SDK:** Do interakcji z modelami Claude.

## Krok 4: OpenRouter – centrum wielu modeli
**OpenRouter** to usługa, która agreguje dostęp do ponad 300 modeli językowych od różnych dostawców poprzez jeden, ustandaryzowany interfejs API.

**Zalety OpenRouter:**
*   **Uproszczona zmiana modeli:** Jeśli chcesz przetestować lub zmienić model (np. z OpenAI na nowy model od Google), często wystarczy zmiana nazwy modelu w zapytaniu, bez konieczności przepisywania dużej części kodu.
*   **Jednolity format zapytań:** Zapytania do różnych modeli są zazwyczaj konstruowane w podobny sposób (np. używając `raw_content` i `raw_system`).
*   **Dostępność:** W jednym miejscu masz dostęp do modeli od OpenAI, Google, Anthropic i wielu innych.
*   **Ceny:** Koszty korzystania z modeli przez OpenRouter są zazwyczaj takie same, jak przy bezpośredniej komunikacji z dostawcą.

## Krok 5: Tokeny – waluta w świecie API modeli językowych
W odróżnieniu od subskrypcji chatów (np. ChatGPT Plus), korzystanie z API rozliczane jest na podstawie **liczby tokenów**.
*   **Tokenizacja:** Model językowy dzieli tekst wejściowy (prompt) i tekst wyjściowy (odpowiedź) na mniejsze jednostki zwane tokenami.
*   **Koszt:** Cenniki modeli językowych podają zazwyczaj koszt za 1000 tokenów.
*   **Tokeny na wejściu (input) vs. na wyjściu (output):** Zazwyczaj tokeny wejściowe są tańsze niż tokeny wyjściowe. Różnica w cenie może być od dwu- do pięciokrotna.
*   **Szacowanie liczby tokenów:** Można użyć bibliotek takich jak `TikToken` (dla modeli OpenAI) do oszacowania liczby tokenów dla danego tekstu. Należy pamiętać, że różni dostawcy mogą używać różnych tokenizerów, więc wyniki mogą się nieznacznie różnić.
    *   Przybliżone założenie: 1 token to średnio 2-3 znaki (w języku polskim może być to więcej, w angielskim mniej). Emotikony mogą zajmować znacznie więcej tokenów.

W Google Colab przygotowany został **kalkulator kosztów użycia API**, który po wprowadzeniu długości promptu, oczekiwanej długości odpowiedzi oraz liczby zapytań, oszacuje miesięczny koszt dla różnych modeli.

## Krok 6: Limity API
Modele językowe mają określone limity, których należy przestrzegać:
*   **Limit tokenów (Context Length):** Każdy model ma maksymalną liczbę tokenów, jaką może przyjąć na wejściu (w prompcie) i wygenerować na wyjściu. Przekroczenie tego limitu spowoduje błąd (np. `400 Bad Request` z informacją o `context length exceeded` lub `max_token limit exceeded`).
    *   Przykład: GPT-4o może przyjąć 128 000 tokenów na wejściu i wygenerować 16 000 tokenów na wyjściu.
*   **Inne limity:** Mogą istnieć również limity dotyczące liczby zapytań na minutę/dzień (Rate Limits).

Projektując automatyzacje lub skrypty, należy przewidzieć potencjalną długość danych wejściowych i wyjściowych, aby nie przekraczać tych limitów.

## Krok 7: Zaawansowane funkcje API modeli językowych
Nowoczesne modele językowe oferują dodatkowe funkcje rozszerzające ich możliwości:

**1. Function Calling (Wywoływanie funkcji) / Tools:**
*   **Cel:** Umożliwia modelowi językowemu korzystanie z zewnętrznych narzędzi lub funkcji w celu uzyskania dodatkowych informacji lub wykonania określonych akcji.
*   **Jak to działa:**
    1.  Definiujesz zestaw narzędzi (funkcji), które model może użyć, opisując, co każde narzędzie robi i jakie przyjmuje parametry.
    2.  Gdy model otrzymuje prompt, który według niego wymaga użycia jednego z tych narzędzi (np. zapytanie o aktualną pogodę, a model ma dostęp do narzędzia pogodowego), zamiast generować bezpośrednią odpowiedź, model zwraca informację, że chce wywołać konkretną funkcję wraz z potrzebnymi argumentami.
    3.  Twój kod (aplikacja) odbiera tę informację, wykonuje zdefiniowaną funkcję (np. odpytuje API pogodowe).
    4.  Wynik działania funkcji jest odsyłany z powrotem do modelu.
    5.  Model wykorzystuje ten wynik do sformułowania ostatecznej odpowiedzi dla użytkownika.
*   **Przykład:** Pytanie "Która jest teraz godzina w Nowym Jorku?". Model, mając dostęp do funkcji sprawdzającej czas, wywoła ją, a następnie na podstawie wyniku poda aktualną godzinę.
*   **Dostępność:** OpenAI, Gemini.

**2. Ustrukturyzowana odpowiedź (np. JSON Mode):**
*   **Cel:** Zmuszenie modelu do generowania odpowiedzi w określonym formacie strukturalnym, najczęściej JSON.
*   **Jak to działa:** W zapytaniu do API można określić, że odpowiedź ma być w formacie JSON. Można:
    *   Użyć ogólnego trybu `JSON Object`: Model sam zdecyduje o strukturze JSON na podstawie treści odpowiedzi.
    *   Zdefiniować `JSON Schema`: Określić dokładną strukturę (pola, typy danych), w jakiej model ma zwrócić odpowiedź.
*   **Użyteczność:** Kluczowe dla agentów AI, gdzie dane muszą być przekazywane między systemami w spójnym formacie, oraz dla skryptów, które oczekują danych w określonej strukturze.
*   **Dostępność:** OpenAI (jako `response_format`), inne modele mogą mieć podobne funkcje.

**3. Narzędzia hostowane przez dostawcę (np. WebSearch od OpenAI):**
*   **Cel:** Umożliwienie modelowi korzystania z narzędzi zintegrowanych bezpośrednio z infrastrukturą dostawcy, np. wyszukiwarki internetowej.
*   **Jak to działa:** Włączając odpowiednią opcję w zapytaniu API (np. `websearch` dla konkretnego kraju), model może samodzielnie zdecydować o przeszukaniu internetu (np. przez Bing), aby uzyskać aktualne informacje potrzebne do odpowiedzi na prompt.
*   **Przykład:** Pytanie "Jakie restauracje z kebabem polecisz dzisiaj na Mokotowie w Warszawie?". Model użyje wyszukiwarki, aby znaleźć aktualnie otwarte i polecane miejsca.
*   **Dostępność:** OpenAI (GPT-4o i inne).

**4. File Search (OpenAI):**
*   **Cel:** Umożliwienie modelowi przeszukiwania treści przesłanych plików (np. PDF, dokumenty tekstowe) w celu znalezienia odpowiedzi na pytania. Jest to element koncepcji RAG (Retrieval Augmented Generation).
*   **Jak to działa:** Przesyłasz pliki do OpenAI, a następnie w zapytaniu API możesz wskazać, że model ma korzystać z tych plików jako źródła wiedzy.
*   **Przykład:** Przesłanie firmowej bazy wiedzy i zadawanie pytań dotyczących wewnętrznych procedur.

**5. Batch API (OpenAI):**
*   **Cel:** Przetwarzanie dużej liczby zapytań (do 50 000 promptów w jednym pliku, maks. 200 MB) w sposób asynchroniczny, z możliwością uzyskania niższej ceny za tokeny (np. 50% zniżki).
*   **Jak to działa:**
    **Krok 1:** Przygotowujesz plik zawierający wszystkie prompty.
    **Krok 2:** Wysyłasz plik do specjalnego endpointu Batch API.
    **Krok 3:** Otrzymujesz `job ID`.
    **Krok 4:** Okresowo sprawdzasz status zadania, używając `job ID`.
    **Krok 5:** Po zakończeniu przetwarzania (może to zająć do 24 godzin), otrzymujesz plik z wynikami dla wszystkich promptów.
*   **Użyteczność:** Gdy natychmiastowa odpowiedź nie jest wymagana, np. przy generowaniu dużej liczby artykułów, analizie danych itp.

## Podsumowanie i następne kroki
Zrozumienie działania API modeli językowych, tokenów, limitów oraz zaawansowanych funkcji jest kluczowe dla efektywnego wykorzystania ich potencjału. Zachęcamy do samodzielnego przejścia przez przygotowany notatnik Google Colab, przeczytania komentarzy w komórkach tekstowych i eksperymentowania z kodem. Nie musisz na tym etapie rozumieć każdej linijki kodu, ale ważne jest zrozumienie ogólnych koncepcji.

W notatniku znajduje się również quiz sprawdzający wiedzę, który pomoże Ci utrwalić najważniejsze informacje z tej lekcji. 