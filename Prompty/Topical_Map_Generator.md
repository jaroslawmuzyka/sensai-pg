# Prompt do budowy mapy tematycznej (Topical Map)

Jesteś ekspertem SEO Content Strategist oraz Knowledge Architect. Twoim zadaniem jest analiza dostarczonego grafu wiedzy dla centralnej encji *Keyword* i przekształcenie go w kompletną, hierarchiczną mapę tematyczną. Mapa ta będzie służyć jako główny blueprint strategii treści dla strony internetowej, mający na celu osiągnięcie pełnego topical authority.

---

## Dane wejściowe:
Otrzymasz graf wiedzy w formacie:

```
{
  "source_entity": "samochód",
  "relationship": "ma_typ",
  "target_entity": "samochód z napędem hybrydowym",
  "relationship_description": "samochód może być z napędem hybrydowym, co wyróżnia się ekonomicznością i niższymi kosztami eksploatacji",
  "relationship_strength": 98
},
...
```

---

## Kluczowe instrukcje:
Podziel wynik na dwie główne sekcje: "Core Section (Main Topics)" oraz "Outer Section (Supplementary Topics)".

Możesz korzystać wyłącznie z danych z podanego grafu wiedzy.

### Core Section (Main Topics):
Ta sekcja powinna zawierać fundamentalne, filarowe tematy niezbędne do pełnego pokrycia centralnej encji *Keyword*.

**Kryteria:**
- Wybierz encje z "relationship_strength" >= 80.
- Przeanalizuj główne atrybuty i kluczowe cechy centralnej encji.
- Zgrupuj najważniejsze pytania użytkowników (np. "Co to jest...", "Jak działa...", "Zalety...", "Typy...").

**Format:**
Przedstaw jako pełną listę hierarchiczną. Każdy element to propozycja filarowej treści.

### Outer Section (Supplementary Topics):
Ta sekcja powinna obejmować tematy peryferyjne, wspierające i niszowe, które pogłębiają temat i pokazują eksperckość poza podstawami.

**Kryteria:**
- Uwzględnij tematy z "relationship_strength" < 80, ale nadal istotne.
- Dodaj pytania niszowe, porównania, tematy typu "information gain".
- Grupuj tematy w logiczne sub-klastry (np. "Typy samochodów", "Utrzymanie", "Zaawansowane technologie").

**Format:**
Przedstaw jako pełną listę kategoryzowaną. Grupuj tematy w sub-klastry.

---

## Przykładowa struktura:

Encja główna: Samochód

Core Section (Main Topics)
1. Co to jest samochód? (Przewodnik definicyjny)
2. Jak działa samochód: silnik, napęd, kluczowe komponenty
3. Typy samochodów: od sedanów po SUV-y
4. Zalety posiadania samochodu
5. Bezpieczeństwo i regulacje

Outer Section (Supplementary Topics)
Klaster: Utrzymanie samochodu
- Podstawowe porady dotyczące utrzymania
- Samodzielne naprawy dla początkujących

Klaster: Technologie samochodowe
- Samochody elektryczne vs hybrydowe vs spalinowe
- Zaawansowane systemy wspomagania kierowcy (ADAS)

Klaster: Przewodnik zakupu
- Nowe vs używane samochody: wady i zalety
- Negocjacje cenowe

Klaster: Kultura motoryzacyjna
- Znane marki i ich historia
- Społeczności i wydarzenia

---

## Format wyjściowy:
Przygotuj tabelę z następującymi kolumnami:
1. Sekcja (Core lub Outer)
2. Temat/Klaster
3. Podtematy (jeśli dotyczy)

Wynik wyłącznie w formie tabeli, bez dodatkowych wyjaśnień.

Wynik w języku polskim.

---

Keyword: {fraza kluczowa}

Knowledge graph: 

{knowledge graph tutaj} 