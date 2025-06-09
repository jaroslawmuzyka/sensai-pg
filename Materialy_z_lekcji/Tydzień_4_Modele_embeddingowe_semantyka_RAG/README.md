# Materiały do Tygodnia 4

Ten katalog zawiera materiały dodatkowe do lekcji z czwartego tygodnia kursu SEO 3.0.

## Spis treści
- [Notatniki Colab](#notatniki-colab)
- [Dostępne Zestawy Danych](#dostępne-zestawy-danych)
- [Lekcja: Embeddingi – Teoria](#lekcja-embeddingi--teoria)
- [Lekcja: Przechowywanie embeddingów](#lekcja-przechowywanie-embeddingów)
- [Lekcja: Pamięć długoterminowa modeli językowych + re-ranking](#lekcja-pamięć-długoterminowa-modeli-językowych--re-ranking)
- [Lekcja: Re-ranking w praktyce](#lekcja-re-ranking-w-praktyce)
- [Lekcja: [Ćwiczenie] Różne metody wykorzystania embeddingów i semantyki w pracy nad SEO](#lekcja-ćwiczenie-różne-metody-wykorzystania-embeddingów-i-semantyki-w-pracy-nad-seo)
- [Lekcja: Site Focus & Site Radius](#lekcja-site-focus--site-radius)

---

### Dostępne Zestawy Danych

*   **`senuto_crawl - crawl_senuto (11) (1) (1).csv`**: Crawl domeny Senuto do importu do bazy danych w tygodniu 4. Plik zawiera dane o stronach, tytułach, opisach i treściach, które będą wykorzystywane do generowania embeddingów i testowania zapytań SQL. [Pobierz dataset](https://github.com/sensai-academy/seo3.0/blob/main/Datasety/senuto_crawl%20-%20crawl_senuto%20(11)%20(1)%20(1).csv)

### Notatniki Colab

| Notatnik | Opis | Link |
|:---------|:-----|:----:|
| Podstawy embeddingów | Wprowadzenie do modeli embeddingowych, ich działania i zastosowania w SEO. | [Otwórz w Colab](https://colab.research.google.com/drive/1phQj24TXDi8RJ0-cDCXcG_8qqoW3Cs7u?usp=sharing) |
| Przechowywanie embeddingów | Notatnik pokazujący, jak wrzucić dane z datasetu do Qdrant i Supabase wraz z wektorami wygenerowanymi przez Gemini. | [Otwórz w Colab](https://colab.research.google.com/drive/1Ic2yXVuoBSVKKZRHmZXxjXDYkm2py5y4?usp=sharing) |
| Indeksowanie danych do baz wektorowych | Notatnik pokazujący, jak indeksować dane w bazach wektorowych i wykonywać zapytania semantyczne. | [Otwórz w Colab](https://colab.research.google.com/drive/1phQj24TXDi8RJ0-cDCXcG_8qqoW3Cs7u?usp=sharing) |
| Re-ranking w praktyce | Praktyczne zastosowanie modeli re-rankingowych do poprawy jakości wyników wyszukiwania semantycznego | [Otwórz w Colab](https://colab.research.google.com/drive/1J_35X0ee4_OjZjP4cX3N9O6iqI3e2mXH?usp=sharing) |
| [Ćwiczenie] Różne metody wykorzystania embeddingów i semantyki w pracy nad SEO | Praktyczne przykłady wykorzystania embeddingów do analizy i optymalizacji strony www | [Otwórz w Colab](https://colab.research.google.com/drive/1KFgH7utwJ4imqQjO1mM8L560q9Zb63Zu?usp=sharing) |
| Site Focus & Site Radius | Analiza i obliczanie metryk Site Focus i Site Radius dla strony www | [Otwórz w Colab](https://colab.research.google.com/drive/1KFgH7utwJ4imqQjO1mM8L560q9Zb63Zu?usp=sharing) |

---

## Lekcja: Embeddingi – Teoria

W tej lekcji poznasz podstawy modeli embeddingowych, ich działanie i zastosowanie w SEO. Dowiesz się, jak modele embeddingowe pomagają w analizie semantycznej treści i jak wykorzystać je do poprawy widoczności w wyszukiwarkach.



**Dodatkowe linki:**
- [Ranking modeli embeddingowych (MTEB Leaderboard)](https://huggingface.co/spaces/mteb/leaderboard)
- [Transformer Explainer – wizualne wyjaśnienie działania modeli językowych](https://poloclub.github.io/transformer-explainer/)
- [Dokumentacja modeli embeddingowych Google Gemini](https://ai.google.dev/gemini-api/docs/embeddings?hl=pl)
- [Dokumentacja modeli embeddingowych OpenAI](https://platform.openai.com/docs/guides/embeddings)
- [Zastosowanie modeli embeddingowych w Screaming Frog](https://www.screamingfrog.co.uk/blog/map-related-pages-at-scale/)

---

## Lekcja: Przechowywanie embeddingów

**Notatnik Colab:** [Przechowywanie embeddingów](https://colab.research.google.com/drive/1Ic2yXVuoBSVKKZRHmZXxjXDYkm2py5y4?usp=sharing) - ten notatnik pozwoli Ci zaimportować crawl domeny do bazy danych Supabase i Qdrant. 

**Dataset do importu:** [senuto_crawl - crawl_senuto (11) (1) (1).csv](https://github.com/sensai-academy/seo3.0/blob/main/Datasety/senuto_crawl%20-%20crawl_senuto%20(11)%20(1)%20(1).csv)

Jest to crawl domeny Senuto, który będzie importowany do bazy danych w ramach lekcji. Plik zawiera dane o stronach, tytułach, opisach i treściach, które będą wykorzystywane do generowania embeddingów i testowania zapytań SQL.

W tej lekcji poznasz sposoby przechowywania embeddingów w bazach danych oraz strukturę przykładowej tabeli wykorzystywanej do przechowywania embeddingów i metadanych.

### Przechowywanie embeddingów w Supabase

Poniżej znajdziesz przykładowe zapytania SQL wykorzystywane w lekcji:

**1. Utworzenie tabeli do przechowywania embeddingów:**

```sql
CREATE TABLE senuto_crawl_embeddings (
  id SERIAL PRIMARY KEY,
  url TEXT UNIQUE, -- Dodano unikalny indeks na kolumnie url
  title TEXT,
  description TEXT,
  embedding_content VECTOR(768),
  content TEXT,
  embedding_title VECTOR(768)
);
```

**2. Polityki dostępu (policy) – należy uruchomić w bazie danych:**

> **Uwaga:** W projektach komercyjnych należy zwrócić szczególną uwagę na bezpieczeństwo i ograniczenia dostępu do danych!

Poniższe polityki należy uruchomić w bazie danych, aby umożliwić import, odczyt, aktualizację i usuwanie danych przez użytkownika anonimowego:

- Policy nr 1 – umożliwia usuwanie danych przez użytkownika anonimowego:

```sql
create policy "Anon can delete from senuto_crawl_embeddings"
on public.senuto_crawl_embeddings
for delete
to anon
using (
  true
);
```

- Policy nr 2 – umożliwia dodawanie danych przez użytkownika anonimowego:

```sql
create policy "Anon can insert into senuto_crawl_embeddings"
on public.senuto_crawl_embeddings
for insert
to anon
with check (
  true
);
```

- Policy nr 3 – umożliwia odczyt danych przez użytkownika anonimowego:

```sql
create policy "Anon can select from senuto_crawl_embeddings"
on public.senuto_crawl_embeddings
for select
to anon
using (
  true
);
```

- Policy nr 4 – umożliwia aktualizację danych przez użytkownika anonimowego:

```sql
create policy "Anon can update senuto_crawl_embeddings"
on public.senuto_crawl_embeddings
for update
to anon
using (
  true
)
with check (
  true
);
```

**3. Zapytanie do wyznaczenia 20 najbardziej zbliżonych URLi do każdego URLa:**

To zapytanie zwraca dla każdego rekordu (URL-a) listę 20 najbardziej podobnych URLi na podstawie embeddingu tytułu (cosine similarity).

```sql
SELECT
    su.url AS source_url,
    jsonb_agg(
        jsonb_build_object(
            'url', sim.url,
            'similarity', 1 - (su.embedding_title <=> sim.embedding_title) -- Cosine similarity (1 - distance)
        )
        ORDER BY (su.embedding_title <=> sim.embedding_title) ASC -- Order within the JSON array by distance (most similar first)
    ) AS top_20_similar_urls_with_similarity
FROM
    senuto_crawl_embeddings su
JOIN LATERAL (
    SELECT
        id,
        url,
        embedding_title
    FROM
        senuto_crawl_embeddings
    WHERE
        id != su.id -- Wyklucz rekord źródłowy
        AND embedding_title IS NOT NULL -- Upewnij się, że wektor nie jest pusty dla porównywanych rekordów
    ORDER BY
        su.embedding_title <=> embedding_title -- Sortuj według odległości kosinusowej (im mniejsza wartość, tym bardziej podobne)
    LIMIT 20 -- Ogranicz do 20 najbardziej podobnych dla każdego rekordu źródłowego
) sim ON TRUE
WHERE su.embedding_title IS NOT NULL -- Tylko uwzględnij rekordy źródłowe, które mają embedding
GROUP BY su.id, su.url -- Grupuj po rekordzie źródłowym
ORDER BY su.url; -- Opcjonalnie: sortuj wyniki po URL-u źródłowym dla czytelności
```

### Przechowywanie embeddingów w Qdrant

Przed rozpoczęciem pracy z notatnikiem Colab, musisz skonfigurować swoje konto w Qdrant Cloud. Poniżej znajdziesz szczegółową instrukcję krok po kroku:

**1. Rejestracja w Qdrant Cloud:**

1. Przejdź na stronę Qdrant: [https://qdrant.tech/](https://qdrant.tech/)
2. Kliknij przycisk "Get Started" lub "Try Qdrant Cloud"
3. Wypełnij formularz rejestracyjny:
   - Email
   - Hasło
   - Nazwa organizacji
4. Potwierdź email poprzez kliknięcie linku aktywacyjnego

**2. Tworzenie klastra:**

1. Zaloguj się do panelu Qdrant Cloud: [https://cloud.qdrant.io/](https://cloud.qdrant.io/)
2. Utwórz pierwszy klaster:
   - Nazwa klastra (np. "my-first-cluster")
   - Region (Europa: `europe-west3`)
   - Plan (Free Tier dla testów)
3. Poczekaj na utworzenie klastra (1-3 minuty)

**3. Pozyskanie URL klastra:**

1. Przejdź do szczegółów klastra w panelu
2. W sekcji "Connection" znajdź "Cluster URL"
3. Skopiuj URL w formacie: `https://xxx-xxx-xxx.region.gcp.cloud.qdrant.io:6333`

**4. Generowanie klucza API:**

1. Przejdź do sekcji "API Keys" w panelu klastra
2. Utwórz nowy klucz API:
   - Nazwa klucza (np. "colab-notebook-key")
   - Domyślne uprawnienia
3. **WAŻNE:** Skopiuj i zapisz klucz API (zaczyna się od `eyJ...`)

**5. Weryfikacja połączenia:**

1. Przejdź do sekcji "Console" w panelu
2. Wykonaj podstawowe operacje testowe
3. Sprawdź status klastra (powinien być "Running")

**Ważne uwagi bezpieczeństwa:**

- Nigdy nie udostępniaj klucza API publicznie
- Regeneruj klucz jeśli podejrzewasz kompromitację
- Używaj różnych kluczy dla różnych aplikacji
- Regularnie sprawdzaj logi dostępu

**Informacje o kosztach:**

- Free Tier: 1GB storage, 100K operacji/miesiąc
- Paid Plans: Skalowanie według potrzeb
- Monitorowanie: Sprawdzaj wykorzystanie w sekcji "Usage"

**Przydatne linki:**
- [Porównanie baz wektorowych (Superlinked)](https://superlinked.com/vector-db-comparison)
- [Qdrant – baza wektorowa](https://qdrant.tech/)

## Lekcja: Pamięć długoterminowa modeli językowych + re-ranking

W tej lekcji poznasz koncepcję pamięci długoterminowej w modelach językowych oraz technikę re-rankingu, która pozwala na poprawę jakości odpowiedzi poprzez ponowne ocenianie i sortowanie wyników.

### Prompt do sprawdzenia pamięci modelu

```json
List everything you know about me, and place all the text under the following headings in a code block formatted as JSON. Complete and verbatim
```

Ten prompt służy do sprawdzenia, jakie informacje model językowy przechowuje na nasz temat. Możesz go użyć, aby zobaczyć, co model "pamięta" z poprzednich interakcji.

## Lekcja: Re-ranking w praktyce

W tej lekcji pokażemy na praktycznym przykładzie jak działają modele re-rankingowe. Zobaczymy jak można wykorzystać re-ranking do poprawy jakości wyników wyszukiwania semantycznego.

### Materiały do lekcji:
- [Notatnik Colab: Re-ranking w praktyce](https://colab.research.google.com/drive/1J_35X0ee4_OjZjP4cX3N9O6iqI3e2mXH?usp=sharing)

### Modele do re-rankingu:
1. **GTE-ModernColBERT-v1** - model oparty na architekturze ColBERT, który osiąga najlepsze wyniki na benchmarku BEIR. Szczególnie skuteczny w zadaniach re-rankingu długich dokumentów.
   - Link: [GTE-ModernColBERT-v1](https://huggingface.co/lightonai/GTE-ModernColBERT-v1)

2. **Cohere Rerank** - dedykowane API do re-rankingu oferowane przez Cohere.
   - Link: [Cohere Rerank](https://cohere.com/rerank)
   - Proste w użyciu API REST
   - Optymalizowane pod kątem re-rankingu wyników wyszukiwania

## Lekcja: [Ćwiczenie] Różne metody wykorzystania embeddingów i semantyki w pracy nad SEO

W tej lekcji poznasz różne praktyczne metody wykorzystania modeli embeddingowych w pracy nad SEO. 

### Materiały do lekcji:
- [Notatnik Colab: [Ćwiczenie] Różne metody wykorzystania embeddingów i semantyki w pracy nad SEO](https://colab.research.google.com/drive/1KFgH7utwJ4imqQjO1mM8L560q9Zb63Zu?usp=sharing)

### Dodatkowe pomysły wykorzystania embeddingów w SEO:

1. **Klasteryzacja danych**
   - Grupowanie podobnych treści na stronie
   - Identyfikacja powtarzających się tematów
   - Optymalizacja struktury wewnętrznej
   - [Przykład implementacji z Gemini API](https://github.com/google/generative-ai-docs/blob/main/site/en/gemini-api/tutorials/text_classifier_embeddings.ipynb)

2. **Mapowanie przekierowań na nowej stronie**
   - Automatyczne dopasowanie starych URL-i do nowych
   - Optymalizacja struktury przekierowań
   - Zachowanie wartości SEO przy migracji

3. **Wyznaczanie content GAP do konkurencji**
   - Identyfikacja brakujących tematów
   - Analiza różnic w pokryciu tematycznym
   - Generowanie rekomendacji contentowych

## Lekcja: Site Focus & Site Radius

W tej lekcji poznasz koncepcje Site Focus i Site Radius, które są kluczowymi metrykami w ocenie jakości i spójności tematycznej strony internetowej. Te metryki zostały potwierdzone w wycieku dokumentacji Google Content Warehouse API.

### Materiały do lekcji:
- [Notatnik Colab: Site Focus & Site Radius](https://colab.research.google.com/drive/1KFgH7utwJ4imqQjO1mM8L560q9Zb63Zu?usp=sharing) - skrypt do obliczania metryk znajduje się na końcu notatnika

### Przydatne linki:
- [Jak SEO rozwija się po wycieku algorytmu Google](https://searchengineland.com/how-seo-moves-forward-google-leak-442749)
- [Tajemnice algorytmu: wyciek wewnętrznej dokumentacji Google Search](https://ipullrank.com/google-algo-leak)
- [Czym jest Site Focus i Site Radius? Krytyczne czynniki kształtujące sukces eSEO](https://promotraffic.pl/blog/czym-jest-site-focus-i-site-radius-krytyczne-czynniki-ksztaltujace-sukces-eseo)
- [Website Focus - analiza spójności tematycznej](https://inlinks.com/insight/website_focus/)

### Narzędzia:
- [Site Focus Calculator by Roman Rozenberger](https://github.com/romek-rozen/siteFocusOllama) - narzędzie do obliczania metryk Site Focus i Site Radius

### Co to jest Site Focus?
Site Focus to metryka określająca, jak bardzo strona internetowa jest skupiona na konkretnym temacie lub niszy. Wysoki Site Focus oznacza, że strona jest spójna tematycznie i specjalizuje się w określonej dziedzinie.

### Co to jest Site Radius?
Site Radius to metryka pokazująca, jak szeroki jest zakres tematyczny strony. Określa, jak daleko od głównego tematu strony znajdują się poszczególne podstrony w przestrzeni semantycznej.




