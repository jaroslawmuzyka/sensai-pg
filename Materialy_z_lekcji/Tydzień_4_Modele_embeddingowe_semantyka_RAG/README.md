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



**Przydatne linki:**
- [Porównanie baz wektorowych (Superlinked)](https://superlinked.com/vector-db-comparison)
- [Qdrant – baza wektorowa](https://qdrant.tech/)

**Notatki z lekcji:** [./Dokumenty/T4L02_Przechowywanie_Embeddingow.md](./Dokumenty/T4L02_Przechowywanie_Embeddingow.md)

**Zapytanie SQL do utworzenia tabeli wykorzystywanej w lekcji:**

```sql
CREATE TABLE senuto_crawl_embeddings (
  id SERIAL PRIMARY KEY,
  url TEXT,
  title TEXT,
  description TEXT,
  embedding_content VECTOR(768),
  content TEXT,
  embedding_title VECTOR(768)
);
```

**Aby tabela mogła przyjmować dane, należy utworzyć odpowiednią policy.**

> **Uwaga:** W projektach komercyjnych należy zwrócić szczególną uwagę na bezpieczeństwo i ograniczenia dostępu do danych!

**Policy nr 1 – przykładowa polityka (umożliwia usuwanie danych przez użytkownika anonimowego):**

```sql
create policy "Anon can delete from senuto_crawl_embeddings"
on public.senuto_crawl_embeddings
for delete
to anon
using (
  true
);
```

**Policy nr 2 – przykładowa polityka (umożliwia dodawanie danych przez użytkownika anonimowego):**

```sql
create policy "Anon can insert into senuto_crawl_embeddings"
on public.senuto_crawl_embeddings
for insert
to anon
with check (
  true
);
```

**Policy nr 3 – przykładowa polityka (umożliwia odczyt danych przez użytkownika anonimowego):**

```sql
create policy "Anon can select from senuto_crawl_embeddings"
on public.senuto_crawl_embeddings
for select
to anon
using (
  true
);
```

**Policy nr 4 – przykładowa polityka (umożliwia aktualizację danych przez użytkownika anonimowego):**

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