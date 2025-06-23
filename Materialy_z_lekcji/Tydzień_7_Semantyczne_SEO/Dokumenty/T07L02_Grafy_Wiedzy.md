### Notatka:

Ta lekcja łączy dotychczasowe koncepcje, aby wyjaśnić, jak Google modeluje tematy i buduje mapy tematyczne. Zrozumiesz fundamentalną różnicę między grafem wiedzy a grafem informacji – dwoma kluczowymi narzędziami, których Google używa do porządkowania i rozumienia treści w internecie.

---

### Dwa typy grafów

Aby efektywnie zarządzać ogromem danych w internecie, Google stosuje podział na dwa rodzaje grafów. Utrzymywanie jednej, gigantycznej struktury dla całej sieci byłoby niewydajne. Dlatego wiedza jest organizowana na dwóch poziomach:

**Graf Wiedzy (Knowledge Graph):** Jego celem jest przedstawienie szerokiego obrazu tematu ("big picture", "helicopter view"). Łączy ze sobą główne pojęcia (encje) i pokazuje ich wzajemne relacje, np. jak "samochód" łączy się z "motocyklem" w ramach szerszej dziedziny motoryzacji. Jest to graf reprezentujący **szerokość** wiedzy. Używamy go do budowania struktury serwisu i map tematycznych.

**Graf Informacji (Information Graph):** Skupia się na szczegółach dotyczących jednego, konkretnego pojęcia. Zawiera listę suchych faktów i danych, np. "samochód ma cztery koła", "samochód ma silnik". Reprezentuje **głębokość** wiedzy. Jest idealną podstawą do tworzenia wyczerpujących i bogatych w fakty treści.

---

### Anatomia grafu wiedzy

Graf wiedzy, który będziemy tworzyć, składa się z trzech podstawowych elementów, które pozwalają na zaawansowane modelowanie tematu i budowanie kontekstowego linkowania wewnętrznego.

- **Encje (Węzły / Nodes):** Są to główne pojęcia lub obiekty w analizowanym temacie, np. "samochód", "silnik", "napęd hybrydowy". W SEO semantycznym myślimy w kategoriach encji, a nie słów kluczowych.
- **Relacje (Krawędzie / Edges):** To połączenia, które określają, w jaki sposób encje są ze sobą powiązane. Używamy standardowego słownika relacji (np. `is a` – jest rodzajem, `has part` – ma część), aby utrzymać spójność danych.
- **Etykiety (Właściwości / Labels):** To dodatkowe informacje opisujące relację. W naszym modelu wprowadzamy dwie etykiety: opis słowny relacji (np. "oba są pojazdami kołowymi, ale różnią się liczbą kół") oraz siłę powiązania (jak blisko powiązane są ze sobą dwie encje).

---

### Ćwiczenie: Tworzenie prostego grafu wiedzy

Korzystając z przygotowanego promptu i treści (np. z artykułu na Wikipedii o samochodach), tworzymy pierwszy graf wiedzy. Wprowadzamy do modelu AI treść oraz określamy centralną encję analizy (np. "samochód").

Wynikiem jest struktura w formacie JSON, która pokazuje powiązania między encjami. Na przykład:

- Encja źródłowa: `samochód` | Relacja: `is a` | Encja docelowa: `kołowy pojazd silnikowy`
- Encja źródłowa: `samochód` | Relacja: `has part` | Encja docelowa: `silnik`

Nawet z małej ilości tekstu uzyskujemy mapę kluczowych połączeń, która stanowi szkielet tematu.

---

### Anatomia grafu informacji

Graf informacji ma inną, prostszą strukturę, opartą na tzw. trójnikach semantycznych: **Podmiot – Orzeczenie – Dopełnienie (Subject – Predicate – Object)**. Jego celem jest ekstrakcja jak największej liczby konkretnych faktów z tekstu.

Każdy fakt jest rozbijany na ten trójkowy format, np.: "jabłko (podmiot) jest (orzeczenie) owocem (dopełnienie)". Na tej zasadzie zbudowana jest cała Wikidata, czyli bazodanowy odpowiednik Wikipedii.

---

### Ćwiczenie: Tworzenie grafu informacji

Używając drugiego promptu, przeprowadzamy ekstrakcję informacji z tego samego tekstu. W tym przypadku nie definiujemy centralnej encji, ponieważ celem jest wyciągnięcie wszystkich dostępnych faktów.

Wynikiem jest długa lista trójników w formacie JSON. Na przykład:

- Podmiot: `silnik spalinowy` | Orzeczenie: `wykorzystuje` | Dopełnienie: `benzynę lub olej napędowy`
- Podmiot: `emisja CO2 na osobę na kilometr dla samochodu` | Orzeczenie: `wynosi` | Dopełnienie: `271 gramów`

Taka lista jest bezcenna przy tworzeniu szczegółowego i wyczerpującego contentu.

---

### Podsumowanie i praktyczne zastosowanie

Zapamiętaj kluczową zasadę: **struktura Twojej strony internetowej to graf wiedzy, a jej treść to graf informacji**. Google analizuje Twoją witrynę w obu tych wymiarach, porównując ją do swojego globalnego rozumienia tematu.

Im bogatszy i dokładniejszy graf informacji dostarczysz w swoich treściach, tym Twoja strona będzie bardziej atrakcyjna dla mechanizmów AI Search i AI Overview. Jeśli chcesz zgłębić temat, zapoznaj się z koncepcją **Microsoft Graph RAG**, która potwierdza opisane tu podejście.

---

#### Prompt do stworzenia grafu wiedzy:

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
...
```

---

#### Prompt do stworzenia grafu informacji:

```
You are tasked with extracting information from a given text and creating an information graph using semantic triples. This process involves two main steps: information extraction and graph creation. Follow these instructions carefully to complete the task.

First, you will be presented with a text. Read it carefully and identify the key information, entities, and relationships within it.

Step 1: Information Extraction
- Carefully read through the text and identify important entities, concepts, and relationships.
- Pay attention to names, dates, locations, events, and any other significant information.
- Make note of how these elements relate to each other within the context of the text.

Step 2: Creating the Information Graph
- Using the extracted information, create an information graph represented as a set of semantic triples.
- Each triple should be in the json format:  
{
  "Subject": "value",
  "Predicate": "value",
  "Object": "value"
}
- The subject and object should be entities or concepts, while the predicate describes the relationship between them.
- Ensure that your triples cover all the key information present in the text.
- Aim for clarity and conciseness in your triples.

Guidelines for formatting your output:
- Present your semantic triples in a list format.
- Each triple should be on a new line.
- Use parentheses to enclose each triple.
- Separate the subject, predicate, and object with commas within the parentheses.
- Ensure that your triples, when read together, provide a comprehensive representation of the information in the text.

Here's an example of how your json output should be formatted:
[
  {
    "Subject": "Jan Kowalski",
    "Predicate": "jest",
    "Object": "polskim pisarzem"
  },
  ...
]

Output in Polish
``` 