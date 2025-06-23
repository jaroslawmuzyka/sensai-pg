# Materiały do Tygodnia 7: Semantyczne SEO

Ten katalog zawiera materiały dodatkowe do lekcji z siódmego tygodnia kursu SEO 3.0, poświęconego semantycznemu SEO, budowie map tematycznych oraz modelowaniu wiedzy i informacji.

## Spis treści
- [Wprowadzenie do Semantycznego SEO](#lekcja-wprowadzenie-do-semantycznego-seo)
- [Grafy wiedzy i grafy informacji](#lekcja-grafy-wiedzy-i-grafy-informacji)
- [Tworzenie map tematycznych za pomocą grafów wiedzy](#lekcja-tworzenie-map-tematycznych-za-pomocą-grafów-wiedzy)
- [Proces budowy map tematycznych](#lekcja-proces-budowy-map-tematycznych)
- [Query expansion](#lekcja-query-expansion)
- [T07L06 Deep SERP analysis](#lekcja-deep-serp-analysis)
- [T07L07 Dekompozycja SERP](#lekcja-dekompozycja-serp)
- [T07L08 Baza grafowa Neo4j](#lekcja-baza-grafowa-neo4j)
- [T07L09 Indeksowanie i wizualizacja grafu wiedzy](#lekcja-indeksowanie-i-wizualizacja-grafu-wiedzy)
- [T07L10 Pobieranie danych z grafów wiedzy](#lekcja-pobieranie-danych-z-grafów-wiedzy)

---

## Lekcja: Wprowadzenie do Semantycznego SEO

W tej lekcji poznasz podstawy semantycznego SEO – nowoczesnego podejścia do optymalizacji stron, które skupia się na znaczeniach, powiązaniach kontekstowych i intencjach użytkowników, a nie tylko na słowach kluczowych. Dowiesz się, jak Google ewoluowało w kierunku wyszukiwarki semantycznej (Hummingbird, RankBrain, BERT, Gemini), dlaczego budowa topical authority jest kluczowa oraz jak planować architekturę informacji i topical mapy, by skutecznie odpowiadać na potrzeby użytkowników i algorytmów AI Search. Lekcja omawia także pojęcia takie jak encje, atrybuty, cost of retrieval oraz różnice między tradycyjnym SEO a podejściem semantycznym.

**Materiały:**
- Notatka z lekcji: [T07L01_Wprowadzenie_do_Semantycznego_SEO.md](./Dokumenty/T07L01_Wprowadzenie_do_Semantycznego_SEO.md)
- Transkrypcja: [T07L01_Wprowadzenie_do_Semantycznego_SEO_Transkrypcja.md](./Dokumenty/T07L01_Wprowadzenie_do_Semantycznego_SEO_Transkrypcja.md)
- Link do lekcji na platformie: [SensAI Academy](https://learn.sensai.academy/next/public/lesson/333)

---

## Lekcja: Grafy wiedzy i grafy informacji

Ta lekcja wyjaśnia, jak Google porządkuje wiedzę w internecie, wykorzystując dwa typy grafów: graf wiedzy (knowledge graph) i graf informacji (information graph). Poznasz różnice między nimi – graf wiedzy służy do budowy struktury i map tematycznych (big picture, relacje między encjami), a graf informacji do szczegółowego opisu faktów i tworzenia bogatych treści. Lekcja pokazuje, jak samodzielnie tworzyć oba typy grafów, jak je wykorzystać do planowania contentu i linkowania wewnętrznego oraz dlaczego oba są kluczowe dla skutecznego SEO w erze AI. Praktyczne ćwiczenia pozwalają zrozumieć, jak wyodrębniać encje, relacje i fakty z tekstu.

**Materiały:**
- Notatka z lekcji: [T07L02_Grafy_Wiedzy.md](./Dokumenty/T07L02_Grafy_Wiedzy.md)
- Transkrypcja: [T07L02_Grafy_Wiedzy_Transkrypcja.md](./Dokumenty/T07L02_Grafy_Wiedzy_Transkrypcja.md)
- Link do lekcji na platformie: [SensAI Academy](https://learn.sensai.academy/next/public/lesson/337)

---

## Lekcja: Tworzenie map tematycznych za pomocą grafów wiedzy

W tej lekcji skupisz się na praktycznym wykorzystaniu grafów wiedzy do budowania map tematycznych. Dowiesz się, jak generować rozbudowane grafy wiedzy na podstawie dużych korpusów danych (deep research), a następnie przekształcać je w mapy tematyczne, które ułatwiają planowanie treści i inteligentne linkowanie wewnętrzne. Poznasz narzędzia (Gemini, OpenAI, Claude, Groq) oraz workflow od researchu po generowanie mapy tematycznej i jej zastosowanie w SEO semantycznym.

**Materiały:**
- Notatka z lekcji: [T07L03_Tworzenie_Map_Tematycznych_za_pomocą_Grafów_Wiedzy.md](./Dokumenty/T07L03_Tworzenie_Map_Tematycznych_za_pomocą_Grafów_Wiedzy.md)
- Transkrypcja: [T07L03_Tworzenie_Map_Tematycznych_za_pomocą_Grafów_Wiedzy_Transkrypcja.md](./Dokumenty/T07L03_Tworzenie_Map_Tematycznych_za_pomocą_Grafów_Wiedzy_Transkrypcja.md)
- Link do lekcji na platformie: [SensAI Academy](https://learn.sensai.academy/next/public/lesson/334)

---

## Lekcja: Proces budowy map tematycznych

Ta lekcja wprowadza w zaawansowany proces budowania mapy tematycznej (topical map) w SEO. Poznasz kolejne etapy: od rozbudowy zapytań, przez analizę SERP, dekompozycję i rekompozycję wiedzy, aż po wykorzystanie grafowej bazy danych (Neo4j) i wnioskowanie na podstawie powstałych struktur. Dzięki temu nauczysz się, jak tworzyć kompleksowe strategie contentowe oparte na dogłębnej analizie działania wyszukiwarki Google i nowoczesnych narzędziach do wizualizacji relacji.

**Materiały:**
- Notatka z lekcji: [T07L04_Proces_budowy_map_tematycznych.md](./Dokumenty/T07L04_Proces_budowy_map_tematycznych.md)
- Transkrypcja: [T07L04_Proces_budowy_map_tematycznych_Transkrypcja.md](./Dokumenty/T07L04_Proces_budowy_map_tematycznych_Transkrypcja.md)
- Link do lekcji na platformie: [SensAI Academy](https://learn.sensai.academy/next/public/lesson/335)

---

## Lekcja: Query expansion

W tej lekcji poznasz technikę query expansion (rozszerzania zapytań) – pierwszy krok w budowaniu mapy tematycznej. Dowiesz się, jak automatycznie generować zestaw powiązanych fraz i pytań na podstawie jednego słowa kluczowego, wykorzystując narzędzia AI oraz dedykowany skrypt Google Colab. Poznasz zasady rozszerzania (synonimy, warianty, pytania, porównania) i zobaczysz przykładowe wyniki dla frazy „samochód”.

**Materiały:**
- Notatka z lekcji: [T07L05_Query_expansion.md](./Dokumenty/T07L05_Query_expansion.md)
- Transkrypcja: [T07L05_Query_expansion_Transkrypcja.md](./Dokumenty/T07L05_Query_expansion_Transkrypcja.md)
- Google Colab: [Automatyzacja query expansion](https://colab.research.google.com/drive/1kTx9_TbA43a0hmoOnWI_FhFeoXBZsz6q?usp=sharing)
- Link do lekcji na platformie: [SensAI Academy](https://learn.sensai.academy/next/public/lesson/336)

---

### T07L06 Deep SERP analysis

- **Notatka:** [Dokumenty/T07L06_Deep_SERP_analysis.md](./Dokumenty/T07L06_Deep_SERP_analysis.md)
- **Google Colab:** [Deep Search Analysis](https://colab.research.google.com/drive/1kTx9_TbA43a0hmoOnWI_FhFeoXBZsz6q?usp=sharing)
- **Platforma SensAI:** [Lekcja na platformie](https://learn.sensai.academy/next/public/lesson/338)
- **Transkrypcja:** [Dokumenty/T07L06_Deep_SERP_analysis_Transkrypcja.md](./Dokumenty/T07L06_Deep_SERP_analysis_Transkrypcja.md)

**Opis:**
Lekcja pokazuje, jak przejść od listy rozszerzonych słów kluczowych do głębokiej analizy wyników wyszukiwania (SERP) i budowy mapy powiązań tematycznych. Uczestnicy poznają automatyzację procesu za pomocą Google Colab i narzędzia Serpdata, a także analizę wyników i eliminację szumu w danych.

---

### T07L07 Dekompozycja SERP

- **Notatka:** [Dokumenty/T07L07_Dekompozycja_SERP.md](./Dokumenty/T07L07_Dekompozycja_SERP.md)
- **Platforma SensAI:** [Lekcja na platformie](https://learn.sensai.academy/next/public/lesson/339)
- **Transkrypcja:** [Dokumenty/T07L07_Dekompozycja_SERP_Transkrypcja.md](./Dokumenty/T07L07_Dekompozycja_SERP_Transkrypcja.md)

**Opis:**
Lekcja pokazuje, jak przekształcić surową treść setek stron w ustrukturyzowaną wiedzę w postaci grafów. Omawia konfigurację narzędzi, podwójną perspektywę grafów oraz problem skali danych.

---

### T07L08 Baza grafowa Neo4j

- **Notatka:** [Dokumenty/T07L08_Baza_grafowa_Neo4j.md](./Dokumenty/T07L08_Baza_grafowa_Neo4j.md)
- **Platforma SensAI:** [Lekcja na platformie](https://learn.sensai.academy/next/public/lesson/340)
- **Strona Neo4j:** [https://neo4j.com](https://neo4j.com)
- **Transkrypcja:** [Dokumenty/T07L08_Baza_grafowa_Neo4j_Transkrypcja.md](./Dokumenty/T07L08_Baza_grafowa_Neo4j_Transkrypcja.md)

**Opis:**
Lekcja wprowadza do pracy z profesjonalną bazą grafową Neo4j, pokazuje jak założyć darmową instancję AuraDB i przygotować środowisko do dalszej pracy z grafami wiedzy.

---

### T07L09 Indeksowanie i wizualizacja grafu wiedzy

- **Notatka:** [Dokumenty/T07L09_Indeksowanie_i_wizualizacja_grafu_wiedzy.md](./Dokumenty/T07L09_Indeksowanie_i_wizualizacja_grafu_wiedzy.md)
- **Platforma SensAI:** [Lekcja na platformie](https://learn.sensai.academy/next/public/lesson/341)
- **Transkrypcja:** [Dokumenty/T07L09_Indeksowanie_i_wizualizacja_grafu_wiedzy_Transkrypcja.md](./Dokumenty/T07L09_Indeksowanie_i_wizualizacja_grafu_wiedzy_Transkrypcja.md)

**Opis:**
Lekcja pokazuje, jak zaindeksować graf wiedzy w bazie Neo4j i zwizualizować go w formie interaktywnego grafu, umożliwiając eksplorację i analizę powiązań między encjami.

---

### T07L10 Pobieranie danych z grafów wiedzy

- **Notatka:** [Dokumenty/T07L10_Pobieranie_danych_z_grafow_wiedzy.md](./Dokumenty/T07L10_Pobieranie_danych_z_grafow_wiedzy.md)
- **Platforma SensAI:** [Lekcja na platformie](https://learn.sensai.academy/next/public/lesson/342)
- **Transkrypcja:** [Dokumenty/T07L10_Pobieranie_danych_z_grafow_wiedzy_Transkrypcja.md](./Dokumenty/T07L10_Pobieranie_danych_z_grafow_wiedzy_Transkrypcja.md)

**Opis:**
Lekcja pokazuje, jak wyeksportować dane z grafu wiedzy i wykorzystać je do budowy mapy tematycznej oraz planowania linkowania wewnętrznego na stronie. 