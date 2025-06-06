# Pamięć długoterminowa modeli językowych i retrieval augmented generation (RAG)

Ta notatka wyjaśnia koncepcję pamięci długoterminowej w modelach językowych, przedstawiając technologię Retrieval Augmented Generation (RAG) jako kluczowe rozwiązanie. Dowiesz się, jak RAG umożliwia modelom korzystanie z zewnętrznej wiedzy, jak działa ten proces oraz jakie są jego praktyczne zastosowania.

## Czym (nie) jest pamięć długoterminowa modeli językowych?

Wbrew powszechnemu przekonaniu, modele językowe same w sobie nie posiadają pamięci długoterminowej i nie aktualizują swojej wiedzy na bieżąco po wytrenowaniu. Termin "pamięć długoterminowa" w kontekście modeli odnosi się do technologii i procesów, które zasilają model zewnętrznym kontekstem, wzmacniając jego zdolność do odpowiedzi na podstawie aktualnych lub specyficznych informacji.

**Knowledge Cut-Off:** Każdy model językowy ma datę graniczną swojej wiedzy (Knowledge Cut-Off). Na przykład, model `Gemini 2.5 Flash Preview` z maja 2024 ma wiedzę do stycznia 2025 roku i nie będzie znał wydarzeń po tej dacie, chyba że dostarczymy mu te informacje jako kontekst.

**Przykład pamięci w ChatGPT:** Funkcja pamięci w **ChatGPT** (np. w modelu **GPT-4o**) nie oznacza, że model zapamiętuje wszystkie konwersacje. Zamiast tego, przetwarza rozmowy, zapisuje kluczowe informacje w zewnętrznej bazie i ładuje je jako kontekst, gdy bieżąca konwersacja nawiązuje do tych zapisanych danych. Można sprawdzić, jakie informacje **ChatGPT** zebrał, używając odpowiedniego promptu (wymagany model **GPT-4o**). Przykładowo, może to być podsumowanie informacji takich jak imię, nazwisko, lokalizacja, preferowany format odpowiedzi, zainteresowania, ekspertyza czy projekty.

## Retrieval augmented generation (RAG) – wzmocnienie modeli kontekstem

**RAG** to technologia umożliwiająca dostarczanie modelom językowym relevantnego kontekstu z zewnętrznych źródeł danych w momencie generowania odpowiedzi. Dzięki temu model może opierać swoje odpowiedzi na informacjach, których nie posiadał w swojej pierwotnej bazie wiedzy treningowej.

### Jak działa proces RAG?

Proces RAG można podzielić na kilka kluczowych etapów:

1. **Przygotowanie bazy wiedzy:** Gromadzenie dokumentów (np. PDF, JSON, obrazki, strony internetowe), które mają stanowić zewnętrzną pamięć dla modelu.

2. **Chunking (dzielenie na fragmenty):** Duże dokumenty są dzielone na mniejsze kawałki (chunki). Jest to ważne, ponieważ:
   - **Lepsze działanie modeli embeddingowych:** Modele embeddingowe, używane w kolejnym kroku, działają lepiej na krótszych tekstach, unikając "rozmycia" semantycznego znaczenia przy długich tekstach, gdzie kontekst może się uśredniać i spłaszczać semantyczność.
   - **Precyzyjniejsze wyszukiwanie:** Umożliwia precyzyjniejsze wyszukiwanie relevantnych fragmentów. Google również dzieli strony na kawałki.
   - Przykład: PDF z instrukcjami dotyczącymi **Senuto** jest dzielony na np. 30 mniejszych części.

3. **Embedding (tworzenie wektorów):** Każdy chunk jest przekształcany w wektor liczbowy za pomocą modelu embeddingowego. Wektory te reprezentują semantyczne znaczenie chunków w przestrzeni wielowymiarowej.

4. **Zapis do bazy wektorowej:** Utworzone wektory są zapisywane w specjalnej bazie danych, zwanej bazą wektorową (np. przy wykorzystaniu `subabase` czy `Quadrant`).

5. **Wyszukiwanie (Retrieval):**
   - **Wektoryzacja zapytania:** Gdy użytkownik zadaje pytanie (np. "Ile kosztuje pakiet Basic w **Senuto**?"), jego zapytanie również jest przekształcane na wektor za pomocą tego samego modelu embeddingowego.
   - **Wyszukiwanie w bazie:** Następnie w bazie wektorowej wyszukiwane są chunki (fragmenty treści), których wektory są najbliższe (najbardziej podobne semantycznie) do wektora zapytania. Zazwyczaj wybiera się kilka najbardziej pasujących chunków.

6. **Generowanie odpowiedzi (Augmented Generation):**
   - **Konstrukcja promptu:** Wybrane chunki (kontekst) wraz z oryginalnym pytaniem użytkownika są przekazywane do modelu językowego za pomocą specjalnie skonstruowanego promptu. Prompt wygląda mniej więcej tak: "Tu jest kilka chunków, tu jest pytanie użytkownika [...], odpowiedz na to pytanie w oparciu o te kawałki treści, które ci dostarczam."
   - **Generowanie przez model:** Model generuje odpowiedź, wykorzystując informacje z dostarczonych chunków. Sam model nie posiadał tej wiedzy, ale dzięki procesowi RAG jest w stanie jej użyć.
   - Dzięki temu model może odpowiedzieć na pytanie, nawet jeśli informacja (np. nowa cena pakietu) pojawiła się po jego dacie **Knowledge Cut-Off**.

### Reranking – precyzyjniejsze sortowanie wyników

Czasami same embeddingi mogą nie być wystarczająco precyzyjne, szczególnie przy złożonych zapytaniach, długich tekstach lub bardzo podobnych dokumentach, gdzie porównanie uśrednionych wektorów może nie być skuteczne. W takich przypadkach stosuje się **reranking**:

**Proces rerankingu:** Po wstępnym wyszukaniu przez embeddingi (np. 20 najbardziej pasujących chunków), model rerankingowy ponownie ocenia te chunki. Model rerankingowy jest bardziej zaawansowany, zawiera więcej elementów z modelu językowego (np. enkoder, dekoder, ale nie generuje odpowiedzi) i jest wytrenowany do szeregowania dokumentów według dopasowania do zapytania, lepiej rozumiejąc kontekst i znaczenie.

**Zastosowanie:** Układa chunki w kolejności od najbardziej do najmniej relevantnego względem zapytania. Dopiero te najlepiej ocenione chunki są przekazywane do modelu językowego. Przykład: model rerankingowy może z 20 chunków wybrać te, które na 100% zawierają odpowiedź.

**Reranking w Google:** Google również wykorzystuje (lub wykorzystywał) podobne mechanizmy, np. `Neural Matching` (wspominane w kontekście 2017-2018 roku), do ustalania rankingu na podstawie samej treści strony, co pozwalało na ustalanie rankingu nawet bez uwzględniania linków na tym etapie. Może to oznaczać, że dojście do top 10 wymaga spełnienia wielu czynników, ale pozycja w top 10 może zależeć głównie od treści. Obecnie Google może używać bardziej zaawansowanych technologii.

## Dlaczego RAG jest ważny i jakie problemy rozwiązuje?

**Ograniczenie okna kontekstowego:** Modele mają limit tokenów (jednostek tekstu), które mogą przyjąć w jednym prompcie. Chociaż nowoczesne modele (np. z oknem 10 milionów tokenów) mogą przyjąć dużo danych (kilkadziesiąt książek), to całościowa baza wiedzy firmy (np. o **Senuto**, zawierająca wewnętrzne procesy) może być znacznie większa. RAG pozwala dostarczyć tylko te fragmenty wiedzy, które są aktualnie potrzebne.

**Koszty:** Przesyłanie dużej ilości danych w każdym zapytaniu generuje koszty, ponieważ płaci się za każdy token. RAG, dostarczając tylko relevantne chunki, znacząco redukuje liczbę tokenów i tym samym koszty (nawet o 99%). Zapytanie o cenę pakietu Basic w **Senuto**, które wymagałoby załadowania 60 książek wiedzy, byłoby nieekonomiczne (np. kilkadziesiąt centów za pytanie), podczas gdy z RAG koszt jest znacznie niższy.

**Skupienie i dokładność modelu:** Dostarczenie zbyt dużej ilości informacji, nawet jeśli mieści się w oknie kontekstowym, może spowodować, że model "zgubi się", pominie kluczowe fragmenty lub straci fokus (tzw. "pomijanie informacji w środku"). RAG pomaga modelowi skoncentrować się na najważniejszych danych, dostarczając kontekst, jakiego model aktualnie potrzebuje.

Mimo rosnących okien kontekstowych i spadających cen tokenów, RAG pozostaje kluczowy, zwłaszcza dla bardzo dużych baz danych i dla systemów takich jak wyszukiwarki (np. Google), które zawsze będą potrzebowały efektywnych metod przeszukiwania ogromnych indeksów. Modele także coraz lepiej radzą sobie ze skupieniem, a ich cena dąży do zera, co może zmniejszyć znaczenie RAG w niektórych zastosowaniach generowania treści, ale nie dla wyszukiwarek czy bardzo dużych korpusów wiedzy.

## Zastosowania RAG

Technologia RAG znajduje szerokie zastosowanie w różnych narzędziach i systemach:

**Chatboty i asystenci konwersacyjni:** Na przykład chatbot głosowy na stronie Sensei Academy, który rozmawiał głosem prelegenta. Miał wgraną bazę wiedzy o Sensei (pobraną ze strony i przeformatowaną na Q&A). Pytanie użytkownika było wektoryzowane, wyszukiwane były pasujące odpowiedzi Q&A z bazy, a następnie model generował odpowiedź głosową. Podobnie działają chatboty firmowe.

**Wyszukiwarki semantyczne:** Google wykorzystuje RAG w funkcjach takich jak `AI Overview` i przyszłym `AI Mode`. Zrozumienie RAG pozwala lepiej dostosować treści do tych mechanizmów i potencjalnie odtworzyć ich działanie za pomocą inżynierii wstecznej.

**Generowanie treści:** Chociaż przy obecnych dużych oknach kontekstowych (np. milion tokenów w `Gemini 2.5`) RAG jest mniej konieczny dla generowania pojedynczych artykułów (można załadować cały kontekst konkurencji), nadal jest użyteczny przy pracy z dużymi serwisami (np. Onet, gdzie można wykorzystać archiwalne artykuły, fakty, wewnętrzne dokumenty) lub specyficznymi, obszernymi bazami danych (np. informacje o produktach w e-commerce). Dwa lata temu, przy oknach 8 tys. tokenów, RAG był kluczowy do wyciągania relevantnego kontekstu od konkurencji dla konkretnych nagłówków.

**Asystenci osobiści i "pamięć absolutna":** Wizja narzędzi, które zapisują nasze rozmowy, myśli i doświadczenia (jak w odcinku "Black Mirror" czy urządzeniu `OMI` – które można nosić na skroni lub jako naszyjnik, zapisuje myśli, wektoryzuje i przechowuje w bazie wektorowej do późniejszego czatowania). Przykład: zapisywanie notatek głosowych do bazy wektorowej (np. przez `N8N` i `Quadrant`) i odpytywanie jej później o zapomniane informacje (np. kod do bramy przedszkola). Można by stworzyć model mentalny osoby, który na podstawie historii decyzji mógłby np. zarządzać firmą. Można też komunikować się ze swoimi myślami, konfrontując je z wiedzą np. Marka Aureliusza.

**Narzędzia analityczne i edukacyjne:**

- **`NotebookLM`:** Umożliwia wgranie dokumentów (np. 50 PDF-ów) i zadawanie pytań dotyczących ich treści. Wykorzystuje RAG do ekstrakcji wiedzy. Jest to przykład sprytnego wykorzystania modelu językowego, systemu RAG i przyjaznego interfejsu.

- **Customowe GPTs (w ramach ChatGPT):** Pozwalają na wgrywanie plików, które stają się bazą wiedzy dla GPT. OpenAI przetwarza te pliki, zapisuje w jakiejś bazie wektorowej i wykorzystuje RAG do odpowiadania na pytania zadawane temu customowemu GPT.

## Jak wdrożyć RAG?

Istnieje kilka podejść do implementacji systemu RAG:

1. **OpenAI `Assistant API`:**
   - **Opis:** Najprostsze rozwiązanie, określane jako "no-brainer". Umożliwia tworzenie asystentów, którzy mogą korzystać z wgranych plików (`File Search`), interpretować kod (`Code Interpreter`) i wywoływać zewnętrzne funkcje (`Functions`). Można stworzyć np. inteligentnego asystenta SEO dla **Senuto**, który na podstawie opisu endpointów API **Senuto** i bazy wiedzy o produkcie, mógłby odpowiadać na zapytania typu "wybierz mi wszystkie słowa kluczowe, na które widoczny jest onet", odpytując API, a następnie kategoryzując wyniki za pomocą `Code Interpreter`.
   - **Proces tworzenia w Playground OpenAI:**
     1. **Utwórz VectorStore:** Nazwij go (np. `sensor AI 0.3.0`). Koszt hostowania to np. 10 centów za gigabajt za dzień.
     2. **Stwórz asystenta:** W zakładce "Assistants" nadaj mu nazwę (np. `sensor AI 3.0`) i instrukcję systemową (np. "jesteś inteligentnym asystentem **Senuto**...").
     3. **Wgraj pliki:** Wgraj dokumenty, które mają stanowić bazę wiedzy (np. dokument naukowy "Attention Is All You Need"). OpenAI zajmie się ich podziałem na chunki (można wybrać `chunk size` i `chunk overlap`, ale kontrola jest ograniczona).
     4. **Wybierz model i narzędzia:** Skonfiguruj model i włącz potrzebne narzędzia (np. `File Search`, opcjonalnie `Code Interpreter`, `Functions`).
     5. **Używaj:** Komunikuj się z asystentem przez Playground (np. zadając pytanie "what is encoder?") lub przez API. Asystent odpowie na podstawie wgranego dokumentu.
   - **Ograniczenia:** Mniejsza kontrola nad procesem chunkingu, działaniem bazy wektorowej i samym procesem RAG.

2. **Narzędzia No-Code/Low-Code (`N8N`, `Make`, `DeFi`):**
   - **`N8N`, `Make`:** Wymagają samodzielnej konfiguracji usługi bazy wektorowej (np. konto w `Quadrant`) i połączenia jej w tworzonym przepływie automatyzacji.
   - **`DeFi`:** Często dostarczane z wbudowaną bazą wektorową i gotowymi funkcjami RAG.
   - Narzędzia te będą omawiane w kolejnych tygodniach kursu.

3. **Samodzielne tworzenie (np. `Python` + `Next.js`):**
   - **Opis:** Daje pełną kontrolę nad każdym elementem systemu RAG.
   - **Wymagania:** Wymaga większych umiejętności programistycznych do stworzenia backendu i frontendu.

## Co dalej?

Zrozumienie mechaniki RAG, w tym roli modeli embeddingowych i rerankingowych, jest kluczowe. W kolejnych lekcjach skupimy się na praktycznym aspekcie modeli rerankingowych, aby zobaczyć, jak wpływają na wyniki. Następnie, przy okazji omawiania `AI Overview` i `AI Mode`, zaprojektujemy cały proces RAG w ramach notebooka, aby dokładnie zrozumieć jego działanie. Chociaż produkcyjne wdrożenia RAG będą prawdopodobnie realizowane za pomocą `Assistant API` lub narzędzi No-Code, dogłębne zrozumienie jego mechaniki pozwoli efektywniej wykorzystywać te technologie. Ten tydzień poświęcony jest zrozumieniu mechaniki i procesów RAG. 