# Proces tworzenia promptu

Ta lekcja ma na celu przybliżenie procesu tworzenia efektywnych promptów dla modeli językowych. Obejmuje omówienie różnych metod promptowania, szczegółowe podejście do konstruowania promptów oraz kluczowe zasady, które warto stosować, szczególnie w kontekście zadań SEO. Zrozumienie tych elementów pozwoli na lepsze wykorzystanie potencjału modeli językowych w praktycznych zastosowaniach.

## Metody promptowania: od ogółu do szczegółu

Istnieje wiele technik tworzenia promptów, jednak warto poznać trzy podstawowe, które różnią się poziomem dostarczanych modelowi informacji i przykładów.

- **Zero-shot prompting (promptowanie bez przykładów)**

  **Co to jest:** W tej metodzie zlecasz modelowi językowemu zadanie, nie dostarczając mu żadnych konkretnych przykładów ani szczegółowych instrukcji wykonania.

  **Przykład:**
  ```
  Classify the text into natural, negative or positive. Text: [tutaj wstawiasz tekst do analizy]
  ```

  **Charakterystyka:** Model może za każdym razem zwracać odpowiedź w nieco innym formacie, ponieważ nie ma jasnych wytycznych, jak ma się zachować. Może to być użyteczne w niektórych sytuacjach, np. przy generowaniu skryptu Python do specyficznego zadania, gdzie trudno o dobre przykłady.

- **One-shot prompting (promptowanie z jednym przykładem)**

  **Co to jest:** Polega na zadaniu pytania lub zleceniu zadania wraz z jednym przykładem oczekiwanego rezultatu.

  **Przykład:**
  ```
  generate a recipe for chocolate chip cookies
  [przykładowy przepis]
  ```

  **Charakterystyka:** Model stara się dostosować do podanego formatu, jednak ze względu na obecność tylko jednego przykładu, format odpowiedzi nadal może być zmienny.

- **Few-shot prompting (promptowanie z kilkoma przykładami)**

  **Co to jest:** Jest to najbardziej rekomendowana metoda, szczególnie w kontekście SEO. Polega na dostarczeniu modelowi zadania wraz z kilkoma przykładami jego prawidłowej realizacji.

  **Przykład:**
  ```
  classify the sentiment into the given text as either positive, negative or neutral
  Tekst 1: ... — pozytywny
  Tekst 2: ... — negatywny
  Tekst 3: ... — neutralny
  ...
  ```

  **Charakterystyka:** Dzięki temu podejściu można osiągnąć wysoką powtarzalność odpowiedzi. Model językowy wie, jak się zachować, a format odpowiedzi jest spójny.

**Ważne dla SEO:** Zawsze, gdy to możliwe, stosuj **Few-shot prompting** w zadaniach SEO. Ta technika zapewnia najlepszą jakość i spójność wyników.

---

## Struktura efektywnego promptu: podział na role

Zaawansowane tworzenie promptów często opiera się na podziale instrukcji na dwie główne części: pole "System" i pole "Prompt" (nazywane też "User").

- **Pole System**

  **Cel:** Służy do zdefiniowania, czym jest model językowy (jego rolą), jak ma się zachowywać oraz do umieszczenia informacji, które pozostają niezmienne, niezależnie od konkretnego zadania realizowanego w danym momencie.

  **Zawartość:**
  - Definicja roli: Określenie, kim jest chatbot/agent (np. "jesteś ekspertem w danej dziedzinie X").
  - Cel działania: Co agent ma osiągnąć (np. "tworzy treści informacyjne").
  - Baza wiedzy/Kontekst: Na podstawie jakich typów informacji ma działać.
  - Zasady i wytyczne: Konkretne instrukcje do przestrzegania (np. "używaj słów kluczowych w sposób naturalny", "stosuj poprawne formatowanie HTML", "trzymaj się określonego tonu i głosu marki").
  - Przykłady: Wzorce dobrych i złych odpowiedzi.
  - Instrukcje formatowania: Jak ma wyglądać tekst, w tym styl komunikacji marki.

  **Struktura:** Poszczególne instrukcje warto oddzielać separatorami, np. `###` lub `##`. Różna liczba znaków (np. hashy) może sugerować hierarchię, choć model często interpretuje to elastycznie.

- **Pole Prompt/User**

  **Cel:** Zawiera informacje, które są specyficzne dla aktualnie wykonywanego zadania i zmieniają się przy każdej nowej instrukcji.

  **Zawartość:**
  - Cel (opcjonalnie, jeśli dobrze zdefiniowany w polu System): Krótki, jednozdaniowy opis zadania.
  - Dane wejściowe (input): Konkretne informacje, które model ma przetworzyć w ramach danego zadania. Jest to kluczowe, ponieważ model językowy powinien być traktowany jako procesor językowy, a nie jako samodzielne źródło wiedzy.
  - Instrukcje (specyficzne dla danych wejściowych): Jak zrealizować zadanie na podstawie dostarczonych danych.
  - Przykłady (specyficzne dla danych wejściowych, jeśli potrzebne): Jak wykonać zadanie z użyciem konkretnych danych wejściowych.

---

## Fundamentalna zasada: model językowy jako procesor, nie źródło wiedzy

Największym błędem popełnianym przez użytkowników modeli językowych jest traktowanie ich jak wszechwiedzącej wyroczni. Znacznie efektywniej jest postrzegać je jako **zaawansowane procesory językowe**.

- **Zasada "śmieci na wejściu, śmieci na wyjściu":** Jeśli dostarczysz modelowi słabej jakości lub niewystarczające dane wejściowe, możesz oczekiwać równie słabych wyników. Przykładowo, prośba o napisanie artykułu na podstawie jednego słowa kluczowego prawdopodobnie nie przyniesie satysfakcjonujących rezultatów.
- **Karm model danymi:** Twoim zadaniem, szczególnie w kontekście SEO, jest dostarczanie modelowi niezbędnych danych i kontekstu, aby mógł on wygenerować pożądane treści lub wykonać inne zadania, a nie oczekiwanie, że sam wyszuka informacje w swojej bazie wiedzy. Modele językowe same w sobie są zazwyczaj słabe w takich zadaniach jak keyword research czy rozumienie złożonych relacji między słowami kluczowymi bez odpowiedniego wsadu informacyjnego.

---

## Przykład rozbudowanego promptu: generowanie treści dla sekcji H2/H3

Poniżej przedstawiono strukturę promptu służącego do generowania tekstu dla konkretnej sekcji artykułu, np. dla nagłówka H2 i powiązanych z nim nagłówków H3.

- **Pole System (elementy stałe):**
  - Rola: "Jesteś ekspertem w temacie [nazwa tematu]..."
  - Zadanie: "...tworzysz wartościowe treści informacyjne, jesteś zaznajomiony z zasadami SEO..."
  - Cel: Precyzyjnie określony dla agenta.
  - Baza wiedzy: Typy informacji, na których ma bazować.
  - Zasady:
    - Wplataj słowa kluczowe w sposób naturalny i poprawny gramatycznie.
    - Używaj poprawnego kodu HTML.
    - Stosuj zdefiniowany ton i głos marki (brand voice).
    - Mieszaj zdania krótkie i długie (uwaga: to może wymagać późniejszej iteracji).
  - Przykłady: Dobre i złe wzorce odpowiedzi.
  - Separatory: Używaj `###` lub `##` do oddzielania poszczególnych instrukcji.

- **Pole User/Prompt (elementy zmienne dla każdej sekcji H2/H3):**
  - Instrukcja: "Wygeneruj treść dla poniższego nagłówka H2 i jego nagłówków H3."
  - Dane wejściowe:
    - Nagłówki H2 i H3: Konkretne nagłówki, dla których ma powstać treść.
    - Fakty: Istotne fakty dotyczące danego zagadnienia (np. wyekstrahowane z treści znajdujących się w TOP10 wyników wyszukiwania).
    - Encje (Entities): Pojęcia/obiekty, które mają zostać uwzględnione w treści.
    - Słowa kluczowe: Lista słów kluczowych do wykorzystania.
    - Nagłówki do użycia: Dokładne brzmienie nagłówków, jeśli jest to istotne.
    - Relacje między encjami: Aby wspomóc strukturę i logikę treści.
  - Informacje kontekstowe:
    - Pełna struktura artykułu (outline): Cały zestaw nagłówków artykułu, aby model miał pełen kontekst.
    - Poprzednio wygenerowana treść: Informacje o tym, co już zostało napisane w poprzednich sekcjach, aby unikać powtórzeń i zapewnić spójność. Model wie, co już napisał i o czym będzie pisał dalej (jeśli to nie jest ostatni nagłówek).

Taki sposób tworzenia promptów, gdzie dostarczamy modelowi zarówno instrukcje, jak i konkretne dane do przetworzenia, jest bardzo efektywny. Często informacje wejściowe dla jednego promptu są generowane przez szereg wcześniejszych promptów.

---

## Proces iteracyjny i doskonalenie

Należy pamiętać, że nawet przy bardzo szczegółowych promptach model językowy może nie zinterpretować idealnie wszystkich instrukcji za pierwszym razem. Na przykład, polecenie "mieszaj zdania krótkie i długie" może początkowo skutkować generowaniem zdań o podobnej długości. Dlatego kluczowe jest przygotowanie się na proces iteracyjny, który może obejmować kilkukrotne "przepisywanie" lub modyfikowanie wygenerowanej treści w celu osiągnięcia optymalnego rezultatu.

---

## Podsumowanie

Lekcja ta przybliżyła trzy główne metody promptowania: Zero-shot, One-shot oraz Few-shot, przy czym ta ostatnia jest szczególnie rekomendowana dla zadań SEO. Skuteczne tworzenie promptów opiera się na jasnym zdefiniowaniu roli i zadań modelu w polu "System" (instrukcje stałe) oraz dostarczaniu konkretnych, zmiennych danych i zadań w polu "Prompt/User". Co najważniejsze, modele językowe należy traktować jako procesory danych, które przekształcają dostarczone informacje, a nie jako samodzielne źródła wiedzy. Precyzyjne, bogate w kontekst prompty prowadzą do lepszych i bardziej spójnych wyników, chociaż proces iteracyjnego doskonalenia jest często nieodzownym elementem pracy. 