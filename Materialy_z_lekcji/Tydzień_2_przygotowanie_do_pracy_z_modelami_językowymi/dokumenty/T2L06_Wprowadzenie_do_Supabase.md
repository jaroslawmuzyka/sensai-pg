## Wprowadzenie do Supabase: Baza danych dla Twoich projektów
W tej lekcji zapoznamy się z Supabase – wszechstronnym rozwiązaniem backendowym, które w naszym kursie posłuży jako baza danych. Dowiesz się, czym jest Supabase, jakie ma możliwości (szczególnie w kontekście danych wektorowych i modeli embeddingowych) oraz jak skonfigurować swój pierwszy projekt i zaimportować do niego dane. Celem jest praktyczne zaznajomienie się z interfejsem i podstawowymi funkcjami Supabase.

### Czym jest Supabase?
Supabase to alternatywa dla Firebase, oferująca zestaw narzędzi do budowy aplikacji backendowych. Umożliwia m.in. tworzenie autentykacji, zarządzanie użytkownikami czy obsługę płatności. W kontekście tego kursu, kluczową zaletą Supabase jest możliwość przetwarzania dużych ilości danych, w tym **danych wektorowych**. To niezwykle istotne przy pracy z modelami embeddingowymi, które będą omawiane w dalszej części kursu.

Warto wiedzieć, że Supabase bazuje na **PostgreSQL** i udostępnia przyjazny interfejs webowy, co ułatwia pracę, szczególnie osobom początkującym. Bardziej zaawansowani użytkownicy mogą uzyskać podobne funkcjonalności, samodzielnie konfigurując instancję PostgreSQL z odpowiednimi dodatkami.

Supabase oferuje również **Edge Functions**, które pozwalają na wykonywanie skryptów po stronie serwera, np. do dynamicznego przeszukiwania bazy danych i zwracania wyników przez API. Umożliwia to budowanie semantycznie dopasowanych wyszukiwarek na stronach internetowych.

### Pierwsze kroki z Supabase: Rejestracja i tworzenie projektu
Aby rozpocząć pracę, odwiedź stronę `supabase.com`.

**Koszty:** Supabase oferuje darmowy plan, który jest wystarczający na potrzeby kursu. Obejmuje on m.in. nielimitowaną liczbę zapytań API, 50 tysięcy aktywnych użytkowników miesięcznie (mniej istotne, jeśli nie budujesz pełnej aplikacji) oraz 500 MB przestrzeni dyskowej. Plan Pro, kosztujący 25 USD miesięcznie, oferuje znacznie większe zasoby.

Po zalogowaniu się na swoje konto, wykonaj następujące kroki, aby stworzyć nowy projekt:
1.  **Utwórz organizację:** Jeśli jeszcze jej nie masz, stwórz organizację, która będzie katalogiem dla Twoich projektów (np. `SEO QS`).
2.  **Stwórz nowy projekt:** Nazwij swój projekt (np. `SEO 3.0`).
3.  **Wybierz maszynę (Pricing plan):** Dla celów kursu wystarczająca będzie maszyna oznaczona jako **micro** (darmowa).
4.  **Wybierz region:** Wybierz region serwera, na którym będzie działać Twoja baza danych. W przykładzie wybrano **Frankfurt** ze względu na bliskość geograficzną, jednak dla celów kursu nie ma to krytycznego znaczenia.

Po chwili Twój projekt zostanie utworzony i będziesz mieć dostęp do panelu zarządzania.

### Konfiguracja bazy danych: Aktywacja rozszerzenia Vector
Zanim zaczniesz tworzyć tabele i importować dane, musisz aktywować kluczowe rozszerzenie.
1.  W panelu projektu przejdź do sekcji **Database**.
2.  Znajdź zakładkę **Extensions**.
3.  Wyszukaj rozszerzenie o nazwie `vector`.
4.  **Włącz (Enable)** to rozszerzenie. Dzięki temu będziesz mógł tworzyć kolumny przechowujące wektory embeddingów.

Supabase pozwala również na automatyczne generowanie embeddingów przy dodawaniu danych, jednak w ramach kursu będziemy głównie korzystać ze skryptów Python do tego celu.

### Przygotowanie danych i tworzenie tabel za pomocą modelu językowego
W tej lekcji stworzymy przykładową bazę danych na podstawie danych z Senuto, zapisanych w pliku Excel. Przechowywanie plików Excel bezpośrednio w bazie danych nie jest standardową praktyką, ale posłuży nam jako ćwiczenie do dalszych operacji, takich jak pobieranie meta description, tytułów, generowanie embeddingów i analiza optymalizacji.

**Tworzenie tabel za pomocą SQL i modeli językowych:**

Standardowo, do tworzenia tabel w bazie PostgreSQL używa się języka SQL. Jednakże, zakładając brak znajomości SQL, w lekcji pokazano, jak wygenerować odpowiednie zapytania SQL za pomocą modelu językowego (w przykładzie użyto Claude 3.5 Sonnet, ale sprawdzą się też Gemini 1.5 Pro/Flash).

**Kroki:**
1.  **Przygotuj plik Excel z danymi** (np. eksport z Senuto).
2.  **Użyj modelu językowego (np. Claude):**
    *   Wgraj plik Excel do interfejsu modelu.
    *   Sformułuj prompt, który opisze strukturę danych i poinformuje model o konieczności uwzględnienia kolumny na wektory (w przykładzie podano `vector(3072)`, co odpowiada liczbie wymiarów konkretnego modelu embeddingowego – na tym etapie nie musisz w pełni rozumieć tego szczegółu).
    *   Możesz dodać dodatkowe instrukcje, np. że nie każdy wiersz musi mieć URL.
    *   Model językowy powinien wygenerować skrypt SQL tworzący odpowiednie tabele.
3.  **Wykonaj skrypt SQL w Supabase:**
    *   W panelu Supabase przejdź do **SQL Editor**.
    *   Wklej wygenerowany przez model językowy skrypt SQL.
    *   Uruchom skrypt (kliknij **Run**).
    *   Jeśli pojawią się błędy, skopiuj je i wklej z powrotem do modelu językowego z prośbą o poprawkę. W przykładzie wystąpił błąd związany z domyślnym limitem wymiarów dla wektorów w Supabase, który model musiał skorygować (zmieniając `vector(1536)` na `vector(3072)` lub inną wymaganą wartość).
    *   Po pomyślnym wykonaniu skryptu, w sekcji **Table Editor** powinny pojawić się nowe tabele (w przykładzie: `master_data` i `url_data`).

**Uwaga:** W przyszłych lekcjach dowiesz się więcej o optymalizacji tabel i baz danych za pomocą indeksów.

### Konfiguracja polityk dostępu (RLS Policies)
Aby móc komunikować się z tabelami za pomocą API (np. w celu importu danych), musisz skonfigurować Row Level Security (RLS) Policies.

**Kroki:**
1.  Przejdź do **Table Editor** i wybierz tabelę.
2.  Znajdź zakładkę **RLS Policies** (lub "Authentication" -> "Policies").
3.  Stwórz nową polisę. W przykładzie stworzono polisę pozwalającą na komunikację z API dla użytkownika **Anon** (anonimowego).
4.  **Ważne ostrzeżenie:** Użycie użytkownika `Anon` z pełnymi uprawnieniami (select, insert, update, delete) jest uproszczeniem na potrzeby kursu. W projektach produkcyjnych należy skonfigurować bardziej restrykcyjne polisy, aby zapewnić bezpieczeństwo danych. Każdy, kto uzyska klucz API, będzie miał dostęp do modyfikacji danych.
5.  Powtórz proces dla wszystkich tabel, z którymi chcesz się komunikować przez API.

Alternatywnie, polityki RLS można również tworzyć za pomocą zapytań SQL wygenerowanych przez model językowy lub korzystając z wbudowanego asystenta AI w Supabase.

### Import danych do Supabase za pomocą skryptu Python
Dane z pliku CSV (wcześniej Excel) zostaną zaimportowane do tabel Supabase za pomocą skryptu Python uruchomionego w Google Colab.

**Kroki:**
1.  **Poproś model językowy o wygenerowanie skryptu Python:**
    *   Podaj modelowi informacje o konieczności uwzględnienia zmiennych środowiskowych dla `SUPABASE_URL` i `SUPABASE_API_KEY` (te dane znajdziesz w ustawieniach projektu Supabase w sekcji API).
    *   Zaznacz, że skrypt powinien mapować polskie nazwy kolumn z pliku Excel/CSV na angielskie nazwy kolumn w bazie danych (generalnie zaleca się używanie angielskich nazw kolumn w bazach danych).
    *   Poproś o uwzględnienie importu pliku.
2.  **Przygotuj i uruchom skrypt w Google Colab:**
    *   Skopiuj wygenerowany skrypt Python.
    *   Otwórz nowy notatnik w Google Colab.
    *   Wklej i dostosuj skrypt (w lekcji wspomniano o kilku iteracjach generowania skryptu – skorzystaj z finalnej, działającej wersji).
    *   Uruchom skrypt. Zostaniesz poproszony o wgranie pliku CSV.
    *   Skrypt połączy się z Twoją bazą Supabase (używając podanych kluczy API) i zaimportuje dane partiami (w przykładzie po 50 adresów URL naraz).
3.  **Sprawdź dane w Supabase:**
    *   Przejdź do **Table Editor** w Supabase.
    *   Sprawdź, czy dane pojawiły się w odpowiednich tabelach (np. `url_data`, `master_data`).

### Przeglądanie i odpytywanie danych w Supabase
Po zaimportowaniu danych możesz je przeglądać bezpośrednio w **Table Editor**.

Supabase oferuje również **SQL Editor**, gdzie możesz pisać własne zapytania SQL do analizy danych. Przykłady zapytań:
*   `SELECT * FROM master_data WHERE position <= 10;` (wybierz wszystkie słowa kluczowe na pozycji 10 lub wyższej)
*   `SELECT * FROM master_data WHERE keyword ILIKE '%seo%';` (wybierz wszystkie słowa kluczowe zawierające "seo", ignorując wielkość liter)

**Odpytywanie za pomocą modelu językowego:**

Jeśli nie znasz SQL, możesz skorzystać z pomocy modelu językowego:
1.  Użyj zapytania SQL, aby uzyskać strukturę tabeli (np. `SELECT column_name, data_type FROM information_schema.columns WHERE table_name = 'master_data';` - dokładne zapytanie może być inne, w lekcji wspomniano o skopiowaniu struktury jako JSON).
2.  Wklej tę strukturę (lub JSON) do modelu językowego.
3.  Sformułuj w języku naturalnym, jakie dane chcesz uzyskać (np. "Pokaż mi wszystkie słowa kluczowe, które są na pozycji od 1 do 5 i zawierają frazę 'marketing'").
4.  Model językowy wygeneruje odpowiednie zapytanie SQL, które możesz wkleić i uruchomić w SQL Editor w Supabase.

### Podsumowanie i następne kroki
W tej lekcji nauczyłeś się, czym jest Supabase, jak założyć projekt, skonfigurować bazę danych pod kątem wektorów, tworzyć tabele (z pomocą modelu językowego) oraz importować i odpytywać dane. Jest to fundament pod dalszą pracę z Supabase w kolejnych modułach kursu.

**Zalecenia:**
*   Zapoznaj się dokładnie z interfejsem Supabase.
*   Jeśli masz możliwość, spróbuj nauczyć się podstaw języka SQL – będzie to bardzo pomocne.
*   Sprawdź materiały dodatkowe do lekcji, w tym linki do zasobów na GitHub.

W kolejnych lekcjach będziemy dalej wykorzystywać Supabase do bardziej zaawansowanych zadań, takich jak praca z embeddingami i budowanie semantycznych wyszukiwarek. 