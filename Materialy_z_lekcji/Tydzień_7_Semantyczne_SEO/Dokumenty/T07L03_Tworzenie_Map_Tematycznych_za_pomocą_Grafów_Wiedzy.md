# Tworzenie map tematycznych za pomocą grafów wiedzy

Ta lekcja koncentruje się na praktycznym zastosowaniu **grafów wiedzy** do budowania **map tematycznych**. Nauczysz się, jak z wykorzystaniem dużych korpusów danych generować grafy wiedzy, które następnie posłużą do tworzenia struktury treści i efektywnego linkowania wewnętrznego. To prosty i szybki sposób na rozpoczęcie pracy z semantyką w SEO.

---

## Wyzwania związane z korpusem danych

W poprzedniej lekcji budowany graf wiedzy był minimalny, ponieważ korpus danych wejściowych (jedna strona Wikipedii) był zbyt mały. Aby stworzyć użyteczną mapę tematyczną, potrzebny jest znacznie obszerniejszy wsad danych. Przykładowo, deep research wykonany w Gemini może dostarczyć 30-40 stron A4, co zapewni więcej encji, powiązań i lepszą reprezentację tematu.

Najlepsze narzędzia do deep researchu to obecnie:

- **Gemini:** Uważany za najlepszy na rynku, szczególnie w kontekście semantyki i grafów wiedzy dla Google.
- **OpenAI:** Akceptowalne, choć nie tak obszerne jak Gemini.
- **Claude:** Oferuje przyzwoity deep research, ale nie tak dużą objętość treści.
- **Groq:** Przydatny dla aktualnych informacji z X (dawnego Twittera), np. w branży krypto, giełdowej czy politycznej.

---

## Budowanie Grafu Wiedzy z Deep Researchu

Aby stworzyć graf wiedzy na podstawie obszernego deep researchu, wykonaj następujące kroki:

1. **Wykonaj Deep Research:** Przygotuj kompleksowy korpus danych dotyczący wybranego tematu (np. "samochody").
2. **Skonfiguruj Projekt / Gema:**
   - **OpenAI (Projekty):** Utwórz nowy projekt (np. "Knowledge Graph"). Skopiuj przygotowany prompt (dostępny w plikach lekcji) do instrukcji projektu. Od czerwca 2024 OpenAI umożliwia wybór większej liczby modeli i narzędzi w projektach, co pozwala na dedykowane środowisko do budowania grafów wiedzy.
   - **Gemini (Gemy):** Przejdź do "Explore gems" i utwórz "new gem" (np. "Knowledge Graph"). Skopiuj ten sam prompt do instrukcji gema. Gemy w Gemini działają podobnie do projektów OpenAI, pozwalając na tworzenie niestandardowych narzędzi.
3. **Wprowadź Dane:**
   - Wklej skopiowany kontent z deep researchu do skonfigurowanego projektu/gema.
   - Określ **centralną encję** (np. "samochód").
   - Podaj język operacji (np. "język polski").
4. **Generowanie Grafu:**
   - Uruchom proces. Modele (szczególnie te bardziej zaawansowane jak GPT-3 lub Gemini 2.5 Pro) wygenerują graf wiedzy w formacie JSON. Pamiętaj, że czatboty (jak OpenAI) mogą generować krótsze odpowiedzi, podczas gdy dedykowane narzędzia (jak AI Studio) mogą dawać obszerniejsze grafy, choć w AI Studio należy ustawić temperaturę na zero dla lepszej ekstrakcji.

Im większy i bardziej szczegółowy korpus danych, tym bogatszy i bardziej użyteczny graf wiedzy uzyskasz. Możesz stworzyć wiele grafów z różnych źródeł deep researchu, a następnie połączyć je w jeden, używając prostego skryptu w Pythonie (pamiętaj o usunięciu duplikacji).

---

## Budowanie Map Tematycznych (Topical Maps)

Mapy tematyczne buduje się na podstawie wygenerowanych grafów wiedzy. Przygotowany prompt (dostępny na GitHubie i w notatkach do lekcji) służy do tego celu.

1. **Skonfiguruj Projekt / Gema dla Mapy Tematycznej:**
   - Podobnie jak w przypadku grafów wiedzy, utwórz nowy projekt w OpenAI (np. "TopicalMap") lub gema w Gemini (np. "Topical Map") i wklej do niego prompt do budowania map tematycznych.
2. **Wprowadź Dane:**
   - Podaj **centralną encję** (np. "samochód").
   - Wklej wcześniej wygenerowany graf wiedzy w formacie JSON.
   - Określ język (np. "język polski").
3. **Generowanie Mapy Tematycznej:**
   - Model wygeneruje mapę tematyczną, podzieloną na dwie główne sekcje, bazując na sile powiązania encji z centralną encją:
     - **Core Section (Sekcja Główna):** Zawiera tematy i encje najsilniej powiązane z centralną encją (np. siła powiązania ≥ 80). Są to kluczowe klastry tematyczne, które w pełni opisują centralną encję (np. "samochód jako pojazd mechaniczny", "układ napędowy samochodu", "podwozie samochodowe", "nadwozie samochodu"). To te tematy powinieneś pokryć w głównej treści.
     - **Outer Section (Sekcja Rozwojowa/Suplementacyjna):** Zawiera tematy słabiej powiązane z centralną encją (np. siła powiązania < 80). Są to tematy uzupełniające, które mogą posłużyć do rozbudowy treści, np. na blogu (np. "wymogi formalno-prawne", "analiza popularnych modeli").

Możesz dostosować wartości siły powiązania, aby precyzyjniej określić, które tematy znajdą się w sekcji głównej, a które w sekcji rozwojowej. Im większy i bardziej szczegółowy graf wiedzy, tym bardziej rozbudowane i precyzyjne będą mapy tematyczne.

---

## Linkowanie Wewnętrzne i Semantyka

Mapy tematyczne pozwalają na tworzenie inteligentnego **linkowania wewnętrznego** (Contextual Bridge). Wiedząc, jakie są relacje między encjami i jak są one silnie powiązane, możesz tworzyć linki w najbardziej logicznych i semantycznie poprawnych kontekstach. Na przykład, wiedząc, że "samochód" ma "silnik spalinowy" jako "część" z wysoką siłą powiązania (np. 95), możesz tworzyć linki w tekście w taki sposób, aby Bert (model językowy Google) doskonale rozumiał kontekst. Im większe grafy, tym większe możliwości budowania rozbudowanych struktur adresów URL i strategii linkowania.

---

## Prompt do tworzenia grafu wiedzy

```
# Goal
From the provided text, identify and extract key entities and their relationships, with a strong emphasis on those **directly and uniquely related to the central entity <central_entity>**. The extraction should prioritize information that a user specifically searching for <central_entity> would find most valuable and insightful. Consider the original source's intent and how it connects to <central_entity>.

**Focus on extracting entities that are strongly related to <central_entity>. A strong relationship implies a direct, explicit, and significant connection that provides core information or unique insights about <central_entity>.**

Analyze the content and perform the following steps:
1. **Identify Key Entities:** Extract all relevant entities (people, places, organizations, concepts, events) present in the text.
2. **Determine Relationships:** Identify precise relationships between these entities, especially focusing on their connection to <central_entity>.
3. **Construct Knowledge Graph:** Create a knowledge graph in <language_name> where:
   * Each entity is a node.
   * Relationships are edges connecting nodes.

# Relationships you can use to build a knowledge graph. Use only accurate ones.
## Hierarchical Relations (Taxonomic and Meronomic)
- is_a (type_of): Specifies that one entity is a generalization of another.
- instance_of: Specifies that one entity is a specific example of another.
- part_of: Indicates that an entity is a component of a larger whole.
- has_part: The inverse of part_of.
## Causal Relations
- causes: Indicates that one entity or event is the cause of another.
- is_caused_by: The inverse of causes.
- prevents: One entity stops another from occurring.
- enables: One entity is a necessary condition for or facilitates another.
## Functional and Attributive Relations
- has_attribute (has_property): Assigns a property to an entity.
- uses: An entity utilizes another entity to perform a task.
- produces: An entity creates or generates another entity.
- consumes: An entity uses up another entity.
## Spatial and Temporal Relations
- located_in (is_in): Specifies the location of an entity within another.
- contains: The inverse of located_in.
- precedes: An event occurs before another event.
- follows: An event occurs after another event.
## Social and Organizational Relations
- works_at: Specifies a person's place of employment.
- is_member_of: Indicates membership in a group or organization.
- knows: A relationship of acquaintance between people.
- owns: Specifies ownership.
## Conceptual Relations
- is_opposite_of: Defines antonyms.
- is_similar_to: Indicates a similarity between concepts.
- represents: An entity is a symbol or representation of another idea.

The knowledge graph should use the following format:
-   source_entity: Name of the entity from which the relationship originates.
-   target_entity: Name of the entity to which the relationship connects.
-   relationship_description: A concise and precise description of the link between source_entity and target_entity, **derived exclusively from the provided text**. This should clearly explain *how* they are related.
-   relationship_strength: A numeric score (50-100) indicating the **strength and directness of the relationship to <central_entity>**.

**Prioritize extracting relationships where <central_entity> is either the source_entity or target_entity, or where both source_entity and target_entity have a clear, strong, and direct link back to <central_entity>.**

Use the json format:
{
  "source_entity": "source_entity",
  "relationship": "relationship",
  "target_entity": "target_entity",
  "relationship_description": "relationship_description",
  "relationship_strength": "relationship_strength"
}

After creating the knowledge graph, translate **all entities and descriptions)** into <language_name>.

Present your final result in the following ordered format, prioritizing relationships where <central_entity> is involved, and then by relationship_strength (highest first).

# Output in json format:
[
  {
    "source_entity": "value1",
    "relationship": "value1",
    "target_entity": "value1",
    "relationship_description": "value1",
    "relationship_strength": "value1"
  },
  ...
]

Ensure that entities (source_entity, target_entity) relationship_description in the knowledge graph, is in <language_name>.

<central_entity>
Centralna encja lub keyword
</central_entity>
<language_name>
Język w którym operujemy
</language_name>

Here is the content for analysis:
-----TEXT-----
[content1]
-----TEXT-----
[content2]
-----TEXT-----
[content3]
-----TEXT-----
[content4]
-----TEXT-----
[content5]
-----TEXT-----
``` 