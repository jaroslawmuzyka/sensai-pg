## Wprowadzenie do prompt engineeringu
Ta notatka przedstawia teoretyczne podstawy prompt engineeringu, czyli procesu optymalizacji zapytań (promptów) kierowanych do modeli językowych w celu uzyskania jak najdokładniejszych i najbardziej użytecznych odpowiedzi. Zrozumienie tych zasad pozwoli Ci efektywniej komunikować się z modelami AI i kształtować ich odpowiedzi zgodnie z Twoimi oczekiwaniami.

### Czym jest prompt engineering?
Prompt engineering to, w uproszczeniu, sztuka rozmawiania z modelami językowymi. Sposób, w jaki formułujesz swoje polecenia i pytania, ma kluczowy wpływ na jakość i trafność informacji, które otrzymasz. Celem jest nauczenie się takiej komunikacji, która prowadzi do pożądanych rezultatów.

## Ewolucja i znaczenie prompt engineeringu
Choć jeszcze niedawno prompt engineering był postrzegany jako potencjalny "zawód przyszłości" z wysokimi zarobkami, jego rola ewoluuje. Modele językowe stają się coraz inteligentniejsze (np. nowy model `O-One Preview` od OpenAI), wymagając mniej skomplikowanych instrukcji do przeprowadzenia złożonych procesów myślowych.

### Dlaczego wciąż warto się tego uczyć?
Obecnie używane modele wciąż wymagają precyzyjnych instrukcji, a konstrukcja promptu jest kluczowa dla jakości wyników. Mimo szybkiego postępu technologicznego, który prawdopodobnie zautomatyzuje wiele aspektów, posiadanie fundamentalnej wiedzy o tworzeniu promptów pozostaje wartościowe. Ta lekcja skupi się na uniwersalnym frameworku, który sprawdza się w praktyce i pozwala na automatyzację różnorodnych procesów.

## Podstawy skutecznego promptowania
Wielu użytkowników modeli językowych, takich jak Chat GPT, ogranicza się do wpisywania prostych komend i oczekuje skomplikowanych odpowiedzi. Próba napisania artykułu za pomocą polecenia "Napisz mi artykuł na temat X" jest przykładem podejścia, które zazwyczaj nie przynosi satysfakcjonujących rezultatów.

### Ograniczenia prostych zapytań
Prompty mogą być bardzo proste, ale te naprawdę efektywne są często złożone i szczegółowe. Przykładem może być wewnętrzna instrukcja systemowa Chata GPT czy GitHub Copilot, które są rozbudowane i precyzyjnie określają zachowanie modelu. Celem jest przejście od tworzenia prostych zapytań do konstruowania promptów dających optymalne wyniki.

### Analogia do ewolucji korzystania z wyszukiwarek
Podobnie jak użytkownicy Google'a nauczyli się przechodzić od ogólnych fraz (np. "kredyt") do bardziej sprecyzowanych zapytań ("kredyt hipoteczny 1 mln"), tak użytkownicy AI uczą się efektywniejszego formułowania poleceń. Obecnie jesteśmy na wczesnym etapie adaptacji tej technologii. Z czasem użytkownicy nauczą się wykorzystywać jej potencjał w bardziej zaawansowany sposób, podobnie jak opanowali operatory wyszukiwania w Google (np. `intitle:"kredyt 2%"`).

### Różnica między wyszukiwarką a modelem językowym
Kluczowe jest zrozumienie, że nie można przenosić nawyków z wyszukiwarek internetowych do interakcji z modelami językowymi. Wyszukiwarka to "search engine" (silnik wyszukiwania), podczas gdy AI to "answer engine" (silnik odpowiedzi). Wymaga to innego sposobu konstruowania zapytań.

## Czego unikać: pułapki i mity
Na rynku pojawiają się oferty typu "1057 promptów w Chat GPT, które odmienią Twoje życie". Należy podchodzić do nich z dużą ostrożnością.

### Nieefektywność gotowych list promptów
Takie gotowe zestawy promptów często są generowane automatycznie i mają niską wartość. Trudno jest znaleźć w internecie wysokiej jakości prompty, ponieważ twórcy traktują je jako swoją własność intelektualną lub po prostu niewiele osób potrafi je dobrze konstruować. Nie warto płacić za gotowe prompty.

### Brak "magicznych sztuczek"
Podobnie jak kiedyś w branży SEO istnieli "magicy" dysponujący rzekomo tajną wiedzą, tak teraz w świecie AI pojawiają się osoby twierdzące, że znają magiczne sztuczki. Jest to nieprawda. Zrozumienie zasad działania modeli i metodyczne podejście są kluczem do sukcesu.

## Struktura interakcji z modelem: role
W modelach językowych, szczególnie tych opartych na architekturze transformerów (jak Chat GPT), wyróżniamy zazwyczaj trzy główne role. Zrozumienie ich funkcji jest kluczowe dla skutecznego promptowania.

### **Rola systemowa (System)**
Jest to konfiguracja charakterystyki chatbota. Określa, kim "jest" model, jak ma odpowiadać, czego unikać. Wcześniej, przy braku bezpośredniego dostępu do tej konfiguracji w narzędziach takich jak Chat GPT, użytkownicy często wpisywali w promptach np. "**Jesteś profesjonalnym copywriterem**" – to właśnie próba zdefiniowania roli systemowej.
**W praktyce SEO:** W polu systemowym umieszcza się informacje, które pozostają stałe niezależnie od konkretnego zadania (np. pisania artykułu na dany temat). Można tu zdefiniować ogólny ton, styl, czy wytyczne dotyczące formatowania, które będą obowiązywać dla wielu różnych promptów użytkownika.
Obecnie narzędzia takie jak Chat GPT (poprzez Custom GPTs lub ustawienia niestandardowe) oraz Claude (np. w Claude Project) pozwalają na modyfikację instrukcji systemowej.
*Przykład:* Ustawienie roli systemowej na "**Jesteś Szekspirem, piszesz w stylu szekspirowskim**".

### **Rola użytkownika (User)**
To jest właściwy prompt, czyli polecenie lub pytanie wpisywane przez użytkownika w danym momencie. Treść tego promptu jest interpretowana w kontekście zdefiniowanym przez rolę systemową.
*Przykład (kontynuacja powyższego):* Jeśli w roli systemowej zdefiniowano Szekspira, a użytkownik wpisze "**Napisz wiersz**", model będzie starał się stworzyć wiersz w stylu szekspirowskim.

### **Rola asystenta (Assistant)**
To jest odpowiedź generowana przez model językowy (np. `GPT-4`, `GPT-4.01`).

**Kluczowa wskazówka:** W profesjonalnych zastosowaniach, w tym w SEO i automatyzacjach, kluczowe jest świadome konfigurowanie zarówno roli systemowej, jak i roli użytkownika. Często rola systemowa ma nawet większe znaczenie dla finalnego rezultatu niż sam prompt użytkownika.

## Kluczowe parametry modeli językowych
Parametry modeli językowych są istotne dla kontrolowania ich zachowania. W standardowym interfejsie Chat GPT nie ma bezpośredniej możliwości ich konfiguracji. Sugestie typu "**Bądź kreatywny**" w prompcie mogą wpływać na wewnętrzne ustawienia tych parametrów przez model, ale użytkownik nie ma nad tym precyzyjnej kontroli.

### Potrzeba korzystania z API dla pełnej kontroli
Aby profesjonalnie pracować z modelami językowymi i tworzyć zaawansowane automatyzacje, konieczne jest korzystanie z rozwiązań dających dostęp do **API (Application Programming Interface)**. Pozwala to na precyzyjną konfigurację parametrów.

### Główne parametry:
-   **Temperatura (Temperature):** Kontroluje losowość wyników.
-   **Top P (Top_p):** Ogranicza wybór tokenów do tych o najwyższym sumarycznym prawdopodobieństwie.
-   **Frequency Penalty:** Penalizuje tokeny, które już często pojawiły się w tekście, co może prowadzić do bardziej zróżnicowanego słownictwa, ale w SEO często nie jest to pożądane, gdyż może eliminować ważne słowa kluczowe.
-   **Presence Penalty:** Penalizuje tokeny za sam fakt ich pojawienia się, niezależnie od częstotliwości.

Najczęściej w praktyce będziesz korzystać z parametru **Temperatura**.

## Parametr temperatura: szczegółowe omówienie

### Definicja: Kontrola losowości i kreatywności
Temperatura to kluczowy parametr wpływający na "kreatywność" modelu.
-   **Niska temperatura:** Wyniki są bardziej zdeterminowane, powtarzalne i mniej losowe. Model wybiera najbardziej prawdopodobne tokeny (słowa/części słów).
-   **Wysoka temperatura:** Wyniki są bardziej losowe, zaskakujące i potencjalnie bardziej kreatywne.

### Zakres wartości (np. 0-2 w OpenAI)
W przypadku modeli OpenAI, temperatura zazwyczaj mieści się w zakresie od 0 do 2. W innych modelach zakres może być inny, ale zasada działania jest podobna.

### Praktyczne zastosowanie:
-   **Wysoka kreatywność (wysoka temperatura):** Używana przy generowaniu treści kreatywnych, np. wierszy, opowiadań, czy artykułów, gdzie pożądana jest pewna doza oryginalności. Dla tworzenia treści SEO, wartości w zakresie **0.7 do 1.0** są często optymalne, dając wyniki, które nie są zbyt losowe, ale zachowują sens.
-   **Powtarzalność i precyzja (niska temperatura):** Używana w zadaniach wymagających konkretnych, przewidywalnych odpowiedzi, np. klasyfikacja, analiza sentymentu, czy przypisywanie intencji do słów kluczowych (zadania NLP). W takich przypadkach temperatura często ustawiana jest na **0**.

**Ważne:** Nie ma uniwersalnego "idealnego" ustawienia temperatury. Zależy ono od konkretnego zadania. Zaleca się eksperymentowanie i przeprowadzanie kilku iteracji, aby znaleźć optymalną wartość dla danego przypadku.

### Jak temperatura wpływa na wybór tokenów
Model językowy, generując tekst, przewiduje kolejne tokeny. Na przykład, po słowie "**website**", może rozważać tokeny takie jak "**traffic**" (np. 57% prawdopodobieństwa), "**visibility**" (np. 16%), "**performance**" (np. 5%) itd.
-   Przy niskiej temperaturze, model wybierze najbardziej prawdopodobne tokeny (np. "**traffic**").
-   Przy wyższej temperaturze, model może wybrać mniej prawdopodobne, ale wciąż sensowne tokeny, co prowadzi do większej różnorodności.

Parametr **Top P** działa w połączeniu z temperaturą: jeśli ustawimy `top_p` na przykład na wartość odpowiadającą trzem najbardziej prawdopodobnym tokenom, model będzie losował (zgodnie z temperaturą) tylko spośród tych trzech opcji. Zbyt niska temperatura może prowadzić do tekstów lakonicznych, co często obserwuje się w domyślnych ustawieniach Chat GPT.

## Zarządzanie tokenami
Zrozumienie i zarządzanie tokenami jest fundamentalne w prompt engineeringu.

### Czym są tokeny?
Tokeny to jednostki, na które dzielony jest tekst przez model językowy przed przetworzeniem. Token to niekoniecznie pojedynczy znak czy słowo.
-   W języku polskim: średnio 1 token to około 2 znaki.
-   W języku angielskim: średnio 1 token to około 3 znaki.
Dokładna tokenizacja zależy od konkretnego modelu i jego tokenizera.

### Limity tokenów w modelach (wejście vs. wyjście)
Każdy model językowy ma limit całkowitej liczby tokenów, które może przetworzyć w jednym zapytaniu (suma tokenów na wejściu – prompt – i na wyjściu – odpowiedź).
-   **Przykład: `GPT-4`** (starsza wersja, dostępna przez API)
    -   Limit: 8000 tokenów (łącznie na wejście i wyjście).
    -   Parametr `max_tokens` (ustawiany przez API) określa maksymalną liczbę tokenów, jaką model może wygenerować jako odpowiedź. Jeśli `max_tokens` ustawimy na 6000, na prompt (wejście) pozostaje tylko 2000 tokenów.
-   **Przykład: `GPT-4.0`** (nowszy model)
    -   Limit: 128 000 tokenów (łącznie).
    -   **Ważne ograniczenie:** Maksymalna liczba tokenów na wyjściu (odpowiedź) to nadal około 4000 tokenów (podobnie jak w starszym `GPT-4`). Oznacza to, że model może przyjąć znacznie więcej informacji na wejściu (do 124 000 tokenów, jeśli odpowiedź ma mieć 4000), ale nie wygeneruje odpowiedzi dłuższej niż jego limit wyjściowy. 128 000 tokenów to odpowiednik prawie dwóch średniej długości książek.
-   **Przykład: `Gemini 1.5 Pro` (Google)**
    -   Limit: 1 milion tokenów na wejściu, co pozwala przetworzyć około 15 książek w jednym zapytaniu.

### Parametr `max_tokens`: Kontrola długości odpowiedzi
Ten parametr pozwala określić, jak długa (w tokenach) ma być maksymalnie odpowiedź modelu.

### Dlaczego przewidywanie liczby tokenów jest kluczowe
Tworząc prompty, musisz przewidzieć:
1.  Ile tokenów zużyje Twój prompt (wejście).
2.  Jakiej długości odpowiedzi oczekujesz (wyjście).
3.  Czy suma tych wartości mieści się w limicie danego modelu.

**Przykłady szacunkowe dla długości odpowiedzi:**
-   Post na Twittera: ~300 tokenów może wystarczyć.
-   Artykuł: ~2000 tokenów może być odpowiednie.

Niewłaściwe zarządzanie tokenami może prowadzić do obcięcia promptu lub odpowiedzi, co skutkuje niekompletnymi lub nieużytecznymi wynikami.

## Podsumowanie i następne kroki
Zrozumienie teoretycznych aspektów prompt engineeringu, w tym roli systemu, użytkownika i asystenta, a także wpływu kluczowych parametrów (zwłaszcza temperatury) i limitów tokenów, jest fundamentem do tworzenia skutecznych zapytań. Pamiętaj, że profesjonalne wykorzystanie modeli językowych często wymaga wyjścia poza proste interfejsy czatowe i skorzystania z API w celu pełnej kontroli nad procesem generowania.

W kolejnej lekcji poznasz 10 praktycznych wskazówek dotyczących tworzenia "superpromptów". 