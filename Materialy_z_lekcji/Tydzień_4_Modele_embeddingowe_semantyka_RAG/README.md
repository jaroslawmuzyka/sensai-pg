# Materiały do Tygodnia 4

Ten katalog zawiera materiały dodatkowe do lekcji z czwartego tygodnia kursu SEO 3.0.

## Spis treści
- [Notatniki Colab](#notatniki-colab)
- [Lekcja: Embeddingi – Teoria](#lekcja-embeddingi--teoria)
- [Lekcja: Przechowywanie embeddingów](#lekcja-przechowywanie-embeddingów)

---

### Notatniki Colab

| Notatnik                                    | Opis                                                                                                              | Link                                                                                         |
| :------------------------------------------ | :--------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------- |
| Podstawy embeddingów                        | Wprowadzenie do modeli embeddingowych, ich działania i zastosowania w SEO.                                      | [Otwórz w Colab](https://colab.research.google.com/drive/1phQj24TXDi8RJ0-cDCXcG_8qqoW3Cs7u?usp=sharing) |

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

---

**Przydatne linki:**
- [Porównanie baz wektorowych (Superlinked)](https://superlinked.com/vector-db-comparison)
- [Qdrant – baza wektorowa](https://qdrant.tech/)

**Dataset do importu:** [senuto_crawl - crawl_senuto (11) (1) (1).csv](https://github.com/sensai-academy/seo3.0/blob/main/Datasety/senuto_crawl%20-%20crawl_senuto%20(11)%20(1)%20(1).csv)

Jest to crawl domeny Senuto, który będzie importowany do bazy danych w ramach lekcji. 