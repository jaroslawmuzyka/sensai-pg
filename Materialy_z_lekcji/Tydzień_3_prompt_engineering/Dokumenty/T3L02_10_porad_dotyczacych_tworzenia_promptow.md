## Wprowadzenie: 10 wskazówek dla idealnych promptów
W tej lekcji przedstawione zostanie 10 praktycznych wskazówek dotyczących tworzenia skutecznych promptów. Są to metody często stosowane w codziennej pracy, które znacząco poprawiają jakość interakcji z modelami językowymi. Celem jest przekazanie wiedzy, która pozwoli na uzyskiwanie lepszych i bardziej precyzyjnych odpowiedzi od AI.

### Wskazówka 1: Pisz prompty w języku angielskim
Nawet jeśli oczekujesz odpowiedzi w języku polskim, zaleca się pisanie promptów po angielsku. Istnieje ku temu kilka powodów:
*   **Koszt:** W języku polskim na jeden token przypada średnio więcej znaków (ok. 3) niż w języku angielskim (ok. 2). Oznacza to, że prompty w języku angielskim mogą być tańsze w przetwarzaniu.
*   **Skuteczność:** Modele takie jak GPT-4 wykazują wyższą skuteczność w języku angielskim (np. 85%) w porównaniu do innych języków, w tym polskiego (np. 82%). Choć różnica 3 punktów procentowych może wydawać się niewielka, przy dużej liczbie zadań (np. 100 000) przekłada się to na znaczącą liczbę dodatkowych błędów (w tym przypadku 3000).

Dlatego, dla optymalizacji kosztów i zwiększenia precyzji, warto rozważyć pisanie promptów po angielsku, nawet prosząc o odpowiedź po polsku.

### Wskazówka 2: Stosuj jasne formatowanie
Wytyczne od głównych dostawców modeli językowych (Google, OpenAI, Anthropic/Claude) zgodnie zalecają oddzielanie poszczególnych elementów promptu za pomocą wyraźnego formatowania. Pomaga to modelowi lepiej zrozumieć strukturę zapytania.

**Praktyka:** Często stosuje się znaki hasztagu (`#`) do oddzielania kluczowych sekcji, takich jak instrukcje od żądanego formatu odpowiedzi.

Przykład:
```
# Instrukcja
Przeanalizuj poniższy tekst i zidentyfikuj główne tematy.

# Tekst do analizy
[tutaj wklej tekst]

# Żądany format odpowiedzi
Lista punktowana głównych tematów.
```

### Wskazówka 3: Nakazuj, nie zakazuj
Modele językowe generalnie lepiej reagują na polecenia pozytywne (nakazy) niż negatywne (zakazy). Zamiast mówić modelowi, czego ma *nie robić*, powiedz mu, na czym ma się *skupić*.
*   Zamiast: `Don't think about on-page SEO` (Nie myśl o SEO na stronie)
*   Napisz: `Focus on link building` (Skup się na budowaniu linków)
*   Zamiast: `Don't use exclamation marks` (Nie używaj wykrzykników)
*   Napisz: `End every sentence with a period` (Zakończ każde zdanie kropką)

Chociaż nowoczesne modele (jak GPT-4) mogą poprawnie interpretować zakazy, stosowanie nakazów jest bezpieczniejszą i często skuteczniejszą praktyką.

### Wskazówka 4: Trzymaj się jednego słownictwa (unikaj synonimów w obrębie promptu)
Podczas pisania promptu staraj się konsekwentnie używać tych samych terminów na określenie tych samych konceptów. Używanie synonimów może wprowadzić model w błąd, ponieważ różne słowa to różne tokeny, co może prowadzić do odmiennej interpretacji instrukcji.

**Przykład:** Jeśli w jednej części promptu używasz terminu `keywords`, kontynuuj używanie `keywords` w dalszej części, zamiast przechodzić na `phrases`, jeśli odnosisz się do tego samego pojęcia.

### Wskazówka 5: Używaj mocnych czasowników
Stosuj bezpośrednie i jednoznaczne czasowniki (w języku angielskim określane jako "strong verbs"), aby precyzyjnie komunikować, czego oczekujesz od modelu.
*   Zamiast: `write a summary of a case` (napisz podsumowanie sprawy)
*   Napisz: `summarize the case` (podsumuj sprawę)
*   Zamiast: `make a list of a key points` (zrób listę kluczowych punktów)
*   Napisz: `list the key points` (wymień kluczowe punkty)

Taki sposób formułowania poleceń jest bardziej klarowny i efektywny.

### Wskazówka 6: Proś o pełne odpowiedzi (szczególnie w Chat GPT)
Korzystając z interfejsów czatowych takich jak Chat GPT czy Claude, warto jawnie prosić o kompletne odpowiedzi. Modele te są czasem konfigurowane tak, aby były "leniwe" i oszczędzały na długości odpowiedzi, co jest podyktowane kosztami operacyjnymi dla firm takich jak OpenAI.

Może to prowadzić do ucinania myśli lub generowania zbyt krótkich tekstów. Aby temu zaradzić, można dodać do promptu frazy typu:
*   `give me a complete list` (daj mi pełną listę)
*   `give me the whole text` (daj mi cały tekst)

**Uwaga:** Ta wskazówka ma mniejsze zastosowanie przy korzystaniu z API, gdzie masz większą kontrolę nad parametrem maksymalnej długości odpowiedzi.

### Wskazówka 7: Rozbijaj skomplikowane instrukcje na kilka promptów
To jedna z najważniejszych zasad i częsty błąd początkujących. Zamiast tworzyć jeden, bardzo długi i złożony prompt, który ma wykonać wiele zadań jednocześnie (np. "zrób keyword research, napisz tytuł, napisz nagłówki, napisz artykuł"), znacznie lepsze rezultaty osiąga się przez podzielenie procesu na mniejsze, oddzielne kroki (prompty).

**Przykład: Proces tworzenia opisów kategorii (np. dla sklepu OBI):**
1.  **Wybór głównego słowa kluczowego:** Pierwszy prompt przypisuje główne słowo kluczowe do danej kategorii (np. "kosiarki" dla kategorii kosiarek, na podstawie listy z Senuto).
2.  **Crawling wyników wyszukiwania:** Zebranie danych z TOP 100 wyników wyszukiwania dla wybranych fraz.
3.  **Ekstrakcja słów kluczowych (Content Writer):** Wyodrębnienie powiązanych słów kluczowych z treści konkurentów (np. dla "kosiarek" mogą to być "kosiarki spalinowe", "roboty koszące", "szerokość koszenia").
4.  **Filtracja słów kluczowych:** Ten prompt porównuje wyekstrahowane słowa kluczowe z ofertą konkretnego sklepu (np. OBI) dla danej kategorii, aby upewnić się, że odpowiadają asortymentowi (np. odrzucenie "kosza na trawę", jeśli OBI ich nie sprzedaje w tej kategorii). Do promptu wysyłana jest oferta sklepu.
5.  **Generowanie struktury nagłówków:** Na podstawie przefiltrowanych słów kluczowych, ten prompt tworzy proponowaną listę nagłówków (H2, H3 itd.) dla opisu kategorii.
6.  **Przypisywanie słów kluczowych do nagłówków:** Ten prompt rozdziela słowa kluczowe pomiędzy wygenerowane nagłówki, aby wiadomo było, jakie terminy powinny znaleźć się w poszczególnych sekcjach.
7.  **Przypisywanie filtrów facetowych (opcjonalnie):** Jeśli dostępne, filtry ze strony sklepu mogą być również przypisane do odpowiednich nagłówków.
8.  **Generowanie briefu dla każdego nagłówka:** Dla każdego nagłówka (lub sekcji H2) tworzony jest krótki opis (brief), co powinno się w nim znaleźć (np. dla nagłówka o kosiarkach autonomicznych, brief może sugerować opisanie ich funkcji, zalet, sposobu działania). Na tym etapie treść jeszcze nie jest pisana.
9.  **RAG - Pobieranie treści konkurentów:** Treści od konkurentów są dzielone na mniejsze fragmenty (chunks) i zapisywane w bazie wektorowej.
10. **Generowanie treści dla każdego nagłówka:** Model pisze treść dla każdej sekcji (np. H2 wraz z podległymi H3) oddzielnie. Prompt dla tego kroku otrzymuje: słowa kluczowe, filtry, nagłówki (z tej sekcji), brief dla tej sekcji oraz informacje z RAG.
11. **Humanizacja tekstu:** Wygenerowany tekst jest następnie kilkukrotnie przepisywany (np. 3 razy), aby nadać mu bardziej naturalny charakter i poprawić jakość.

**Kluczowe w procesie wieloetapowym:**
*   Każdy krok (prompt) otrzymuje dane z poprzedniego kroku.
*   Model jest informowany o kontekście: "Piszesz tekst do sekcji X, w poprzedniej sekcji napisałeś Y, a kolejna sekcja zawiera nagłówki Z". To pomaga uniknąć powielania informacji.

**Dlaczego warto rozbijać zadania?**
*   **Problem "lost in the middle":** Modele językowe, nawet te z dużym oknem kontekstowym (np. 128 000 tokenów jak GPT-4 Turbo/O), mają tendencję do "gubienia" lub pomijania informacji znajdujących się w środku bardzo długiego inputu. Badania wskazują, że informacja umieszczona np. w okolicach 70-tysięcznego tokena w modelu 128k ma około 55% szans na bycie pominiętą.
*   **Lepsza kontrola i jakość:** Krótsze prompty z ograniczonym inputem (tylko niezbędne informacje) pozwalają modelowi lepiej przetworzyć dane i skupić się na konkretnym zadaniu, co prowadzi do wyższej jakości wyników.

### Wskazówka 8: Używaj "magicznych" wyrazów/fraz
Chociaż nie ma prawdziwych "magicznych sztuczek", pewne frazy mogą pozytywnie wpłynąć na zachowanie modelu:
*   `Think step by step` (Myśl krok po kroku): Dodanie tej instrukcji może skłonić starsze modele (jak GPT-4, GPT-4 Turbo, GPT-4O) do bardziej złożonego "procesu myślowego" przed udzieleniem odpowiedzi.
    *Uwaga:* Nowsze modele, jak `GPT-01 Preview` (prawdopodobnie chodzi o GPT-4o mini lub podobny zoptymalizowany model), mają często wbudowane mechanizmy typu "Chain of Thought" (łańcuch myśli), więc ta fraza może być zbędna.
*   `Write a draft` (Napisz wersję roboczą): Użyteczne, gdy model (szczególnie w interfejsie czatowym) wydaje się niechętny do współpracy lub generowania pełnej odpowiedzi.
*   `Be creative` (Bądź kreatywny): W Chat GPT, gdzie nie ma bezpośredniego dostępu do parametrów takich jak "temperatura", ta fraza może zwiększyć prawdopodobieństwo, że model wewnętrznie ustawi wyższą temperaturę, co prowadzi do bardziej kreatywnych odpowiedzi.

### Wskazówka 9: Proś model o wyjaśnienie promptu
Po stworzeniu promptu, zwłaszcza bardziej złożonego, warto poprosić model językowy o jego interpretację. Można to zrobić, wysyłając prompt do modelu z dodatkowym poleceniem:

`"Explain step by step what you will do based on the following prompt: [tutaj wklej swój prompt]"`

Odpowiedź modelu pokaże, jak zrozumiał poszczególne części instrukcji. Jeśli jego interpretacja odbiega od Twoich intencji (np. "Ok, ja tego kroku konkretnie to nie chciałem w sumie realizować"), możesz zmodyfikować prompt, aby był bardziej precyzyjny.

### Wskazówka 10: Dawaj przykłady (pozytywne i negatywne)
Modele językowe uczą się i działają bardzo dobrze na przykładach (tzw. "few-shot learning" lub "one-shot learning"). Jeśli chcesz, aby model wygenerował dane lub treść w określonym formacie lub stylu, pokaż mu, jak to zrobić.

**Co warto pokazać:**
*   **Dobre przykłady (pozytywne):** Ilustrują pożądany rezultat.
*   **Złe przykłady (negatywne):** Pokazują, czego unikać.

**Przykład:** Przy generowaniu encji (entities) można podać listę poprawnie sformatowanych encji oraz listę błędnych, aby model zrozumiał kryteria.

Dzięki przykładom model lepiej zrozumie Twoje oczekiwania i będzie w stanie dokładniej je zrealizować.

## Podsumowanie
Stosowanie tych dziesięciu wskazówek może znacząco podnieść jakość i efektywność Twoich promptów. Pamiętaj, że prompt engineering to proces iteracyjny – testuj różne podejścia i obserwuj, co działa najlepiej dla Twoich konkretnych zadań. W kolejnych lekcjach zaprezentowane zostaną bardziej szczegółowe przykłady i praktyczne zastosowania. 