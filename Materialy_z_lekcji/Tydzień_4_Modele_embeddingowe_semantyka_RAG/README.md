# Materiały do Tygodnia 4

Ten katalog zawiera materiały dodatkowe do lekcji z czwartego tygodnia kursu SEO 3.0.

## Spis treści
- [Notatniki Colab](#notatniki-colab)
- [Dostępne Zestawy Danych](#dostępne-zestawy-danych)
- [Lekcja: Embeddingi – Teoria](#lekcja-embeddingi--teoria)
- [Lekcja: Przechowywanie embeddingów](#lekcja-przechowywanie-embeddingów)
- [Przydatne linki](#przydatne-linki)

---

### Dostępne Zestawy Danych

*   **`senuto_crawl - crawl_senuto (11) (1) (1).csv`**: Crawl domeny Senuto do importu do bazy danych w tygodniu 4. Plik zawiera dane o stronach, tytułach, opisach i treściach, które będą wykorzystywane do generowania embeddingów i testowania zapytań SQL. [Pobierz dataset](../Datasety/senuto_crawl%20-%20crawl_senuto%20(11)%20(1)%20(1).csv)

### Notatniki Colab

| Notatnik                                    | Opis                                                                                                              | Link                                                                                         |
| :------------------------------------------ | :--------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------- |
| Podstawy embeddingów                        | Wprowadzenie do modeli embeddingowych, ich działania i zastosowania w SEO.                                      | [Otwórz w Colab](https://colab.research.google.com/drive/1phQj24TXDi8RJ0-cDCXcG_8qqoW3Cs7u?usp=sharing) |
| Przechowywanie embeddingów | Notatnik pokazujący, jak wrzucić dane z datasetu do Qdrant i Supabase wraz z wektorami wygenerowanymi przez Gemini. | [Otwórz w Colab](https://colab.research.google.com/drive/1Ic2yXVuoBSVKKZRHmZXxjXDYkm2py5y4?usp=sharing) |

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

### Konfiguracja Qdrant

Przed rozpoczęciem pracy z notatnikiem Colab, musisz skonfigurować swoje konto w Qdrant Cloud. Poniżej znajdziesz szczegółową instrukcję krok po kroku:

# 🎯 Przewodnik krok po kroku: Rejestracja i konfiguracja Qdrant Cloud

## 🆕 Krok 1: Rejestracja w Qdrant Cloud

1. **Przejdź na stronę Qdrant:**
   - Otwórz przeglądarkę i wejdź na: **https://qdrant.tech/**

2. **Rozpocznij rejestrację:**
   - Kliknij przycisk **"Get Started"** lub **"Try Qdrant Cloud"** na stronie głównej
   - Alternatywnie przejdź bezpośrednio na: **https://cloud.qdrant.io/**

3. **Wypełnij formularz rejestracyjny:**
   - **Email:** Wprowadź swój adres email
   - **Hasło:** Ustaw bezpieczne hasło
   - **Nazwa organizacji:** Podaj nazwę firmy lub projektu
   - Zaakceptuj regulamin i politykę prywatności
   - Kliknij **"Sign Up"**

4. **Potwierdź email:**
   - Sprawdź skrzynkę pocztową
   - Kliknij link aktywacyjny w emailu od Qdrant
   - Zostaniesz przekierowany z powrotem do panelu

## 🏗️ Krok 2: Tworzenie klastra

1. **Zaloguj się do panelu Qdrant Cloud:**
   - Wejdź na: **https://cloud.qdrant.io/**
   - Wprowadź swoje dane logowania

2. **Utwórz pierwszy klaster:**
   - Po zalogowaniu kliknij **"Create Cluster"**
   - **Nazwa klastra:** Wprowadź nazwę (np. "my-first-cluster")
   - **Region:** Wybierz region najbliższy Twojej lokalizacji (Europa: `europe-west3`)
   - **Plan:** Wybierz plan (Free Tier dla testów, Paid dla produkcji)
   - Kliknij **"Create"**

3. **Poczekaj na utworzenie:**
   - Proces może potrwać 1-3 minuty
   - Status klastra zmieni się z "Creating" na "Running"

## 📍 Krok 3: Pozyskanie URL klastra

1. **Przejdź do szczegółów klastra:**
   - W panelu Qdrant Cloud kliknij na nazwę swojego klastra
   - Zostaniesz przeniesiony do sekcji "Overview"

2. **Skopiuj Cluster URL:**
   - W sekcji **"Connection"** znajdziesz **"Cluster URL"**
   - URL ma format: `https://xxx-xxx-xxx.region.gcp.cloud.qdrant.io:6333`
   - Kliknij ikonę kopiowania lub zaznacz i skopiuj pełny URL

**Przykład URL:**
```
https://1fdea6b6-5293-4e9c-8508-d620241a8208.europe-west3-0.gcp.cloud.qdrant.io:6333
```

## 🔐 Krok 4: Generowanie klucza API

1. **Przejdź do sekcji API Keys:**
   - W panelu klastra kliknij zakładkę **"API Keys"** w menu po lewej stronie

2. **Utwórz nowy klucz API:**
   - Kliknij przycisk **"Create API Key"**
   - **Nazwa klucza:** Wprowadź opisową nazwę (np. "colab-notebook-key")
   - **Uprawnienia:** Zostaw domyślne (pełne uprawnienia) lub dostosuj według potrzeb
   - Kliknij **"Create"**

3. **Skopiuj wygenerowany klucz:**
   - **WAŻNE:** Klucz zostanie wyświetlony tylko raz!
   - Skopiuj cały klucz API (zaczyna się od `eyJ...`)
   - Zapisz go w bezpiecznym miejscu

**Przykład klucza API:**
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhY2Nlc3MiOiJtIn0.caWZvtwlzNK1N-dHA1HV64YDL0cDG4YwdWfwuGU42GE
```

## 🔍 Krok 5: Weryfikacja połączenia

1. **Przetestuj połączenie:**
   - W panelu klastra przejdź do sekcji **"Console"**
   - Możesz tam wykonać podstawowe operacje testowe
   - Sprawdź, czy klaster odpowiada na zapytania

2. **Sprawdź status klastra:**
   - W sekcji "Overview" status powinien być **"Running"** (zielony)
   - Sprawdź wykorzystanie zasobów i limity

## ⚠️ Ważne uwagi bezpieczeństwa

- **Nigdy nie udostępniaj** klucza API publicznie
- **Regeneruj klucz** jeśli podejrzewasz kompromitację
- **Używaj różnych kluczy** dla różnych aplikacji/środowisk
- **Regularnie sprawdzaj** logi dostępu w panelu Qdrant

## 💰 Informacje o kosztach

- **Free Tier:** 1GB storage, 100K operacji/miesiąc
- **Paid Plans:** Skalowanie według potrzeb
- **Monitorowanie:** Sprawdzaj wykorzystanie w sekcji "Usage" panelu

## ✅ Podsumowanie

Po wykonaniu wszystkich kroków będziesz mieć:

1. ✅ Konto w Qdrant Cloud
2. ✅ Aktywny klaster bazy danych
3. ✅ URL klastra do połączenia
4. ✅ Klucz API do uwierzytelnienia
5. ✅ Gotową infrastrukturę do pracy z wektorami

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

**Przydatne linki:**
- [Porównanie baz wektorowych (Superlinked)](https://superlinked.com/vector-db-comparison)
- [Qdrant – baza wektorowa](https://qdrant.tech/)