# Goal
 
Identify and extract key entities and their relationships from the provided text, focusing on specific and unique information related to the central keyword while considering the source of each piece of information and the likely intent of users searching
for the central keyword "[[keyword]]".
 
 
## Input Structure
 
The input consists of two parts:
1. The central keyword, provided in the format: "Central Keyword: [[keyword]]"
2. A TXT file containing content from multiple web pages
The central keyword is the main focus of the entity extraction task. All identified entities and relationships should be relevant to this central keyword and align with the likely intent of users searching for this keyword.
The TXT file is structured as follows:
-----TEXT1-----
URL: [url1]
Content: [content1]
-----TEXT2-----
URL: [url2]
Content: [content2]
-----TEXT3-----
URL: [url3]
Content: [content3]
-----TEXT4-----
URL: [url4]
Content: [content4]
-----TEXT5-----
URL: [url5]
Content: [content5]
-----TEXT6-----
...
Copy- The `-----TEXT1-----`, `-----TEXT2-----`, etc. markers separate content from different web pages.
- Each section contains:
 - A URL line indicating the source of the content
 - A Content line containing the actual text content of the web page
- The last section will be followed by an additional `-----TEXTx-----` marker to indicate the end of the input.
When processing this input:
- Treat each section (from one marker to the next) as content from a single web page.
- Use the URL to identify the source of the content. This is crucial for determining if an entity is specific to a particular source or more generally applicable.
- The Content part contains the actual text to analyze for entities and relationships.
 
## Entity Definition and Guidelines
 
An entity is a specific, well-defined element providing meaningful and unique information related to the central keyword. Entities should be more specific than broad categories but not excessively detailed.
 
### Guidelines for identifying entities:
 
1. **User Intent**: Consider the likely intent of users searching for the central keyword. Entities should align with what users are most likely looking for when they search for this keyword.
2. **Specificity**: Entities should be specific but not overly detailed. Include various types of related items and specific aspects related to the central keyword.
3. **Relevance**: Each entity must directly relate to the central keyword and provide unique information that aligns with user intent.
4. **Informativeness**: Entities should offer valuable insights about the topic, not just broad categories.
5. **Distinctiveness**: Include entities that are distinct from each other, even if they are subtypes of a broader category.
6. **Language**: Keep entity names in their original language, but translate entity types to [[language_name]].
7. **Named Entities**: Include company names, brands, or products if they are strongly related to the central keyword, not just providing a service.
8. **People**: Include names of people only if they are inventors of a concept or strongly associated with the central keyword.
9. **Uniqueness**: Each entity should appear only once, but can have multiple relationships and aspects.
10. **Multi-aspect**: If an entity describes multiple elements, assign it 2-3 types.
11. **Detailed subtypes**: Include specific subtypes of main categories related to the central keyword.
12. **Source consideration**: Pay attention to the URL of each text segment. If an entity appears only on one specific website, it may be unique to that source and should be treated cautiously.
13. **Generalization**: While including specific entities, also create generalized entities that group similar concepts when appropriate.
14. **Avoiding URL-specific entities**: Do not list specific products or brands from a single URL unless they are highly relevant to the central keyword and appear in multiple sources.
15. **Merging similar entities**: If two entities have the same name but different types, merge them into a single entity combining all unique types.
16. **Semantic similarity**: If two entities have different names but identical meanings, merge them into a single entity using the most appropriate name.
17. The current date is {current_date}.
18. **Brand-specific entities**: Do not generate entities that are specific to a single brand, product, or website unless ALL of the following conditions are met:
    a. The brand, product, or website name appears in multiple sources (at least two different URLs) from the provided text.
    b. The central keyword explicitly contains the brand or website name.
    c. The brand, product, or website is highly relevant and innovative in the field related to the central keyword.
19. **Strict multi-source requirement**: For any brand-related entity, it MUST appear in more than one source (URL) from the provided text to be included as an entity. If it appears only once, it should be excluded regardless of its perceived importance.
20. **Relevance to central keyword**: Even if a brand or website is mentioned across multiple sources, do not include it as an entity if it's not particularly relevant to the central keyword.
21. **Brand mentions in product descriptions**: Be cautious of brand names mentioned in product descriptions or titles. These should not be considered as separate entities unless they meet all the criteria in point 18.
 
When generating content:
 
- For elements that occurred before this date, use appropriate language indicating the past.
- For elements occurring on or after this date, use appropriate language indicating the future.
- For ongoing or general elements, use appropriate language indicating the present.
 
Adjust the language and structure appropriately for the type of content being generated while maintaining temporal consistency.
 
### Handling source-specific entities:
 
- If an entity appears in multiple text segments from different URLs, it's more likely to be a general, reliable entity.
- If an entity appears only in one text segment (i.e., from a single URL), consider it carefully:
 - If it's a well-known concept related to the central keyword and aligns with user intent, it can be included.
 - If it's a specific product, service, or feature unique to that website, it should be excluded unless it's highly relevant and innovative in the field related to the central keyword and aligns with user intent.
- For entities found in a single source, add a note in the entity type like "Potential source-specific concept" to indicate its limited appearance.
 
### Examples of entities to avoid:
 
- Overly broad categories: "Transport", "Entertainment", "Food"
- Non-specific descriptors: "Good", "New", "Popular"
- Excessively detailed variations: "Green Parvi Stabilized Eucalyptus", "Red Cinerea Stabilized Eucalyptus"
- Irrelevant products: "SFD B Complex 25 Methyl" (unless the keyword is "Vitamin B complex SFD")
- Irrelevant people: "John Smith - SEO specialist" (unless John Smith is the creator of a breakthrough SEO technique)
- Multiple entities with the same pattern: "Product for occasion X", "Product for occasion Y", etc.
- URL-specific product lists: "Brand A eyeglass cleaning cloth", "Brand B eyeglass cleaning cloth", etc.
- Entities not aligned with user intent: For "Mazury" (Masuria), avoid entities like "Mazurskie miejsca administracyjne" (Masurian administrative places) as they don't align with the likely tourist intent of the search.
- Brand-specific products appearing in only one source: "Sukienki damskie Mosquito" (even if it seems relevant, it should be excluded if it only appears once)
- Specific product lines or collections mentioned only once: "Kolekcja wiosna/lato 2024 marki X" (unless the brand X is the central keyword and appears in multiple sources)
- Website-specific features or services: "Program lojalnościowy sklepu Y" (unless Y is the central keyword and this feature is mentioned across multiple sources)
 
## Steps
 
1. Analyze the central keyword and determine the likely intent of users searching for this keyword. Consider what information or aspects of the topic users are most likely interested in.
2. Read through all text segments, keeping track of which entities appear in which sources (URLs).
3. Identify all relevant entities within the text segments, considering the likely user intent. For each identified entity, extract:
- entity_name: Name of the entity in its original language, avoid duplications
- entity_type: Propose 2-3 broad, generally applicable categories for the entity (in [[language_name]])
- entity_definition: short definition of the entity extracted from the provided text
- entity_strength: Numeric score (0-100) indicating the strength of the relationship between the central keyword and this entity, considering user intent
4. Create a temporary list of all identified entities.
5. Process the temporary list to remove duplicates and merge similar entities:
  a. Sort the list alphabetically by entity_name.
  b. For each entity, compare it with the next entity in the list.
  c. If two entities have the same name:
     - If they have the same types, keep only one instance with the highest entity_strength.
     - If they have different types, merge them into a single entity, combining all unique types and keeping the highest entity_strength.
  d. If an entity is very similar to another (e.g., plural vs singular form, slight variation in wording), consider merging them into a more general entity.
  e. If two entities have different names but identical meanings (e.g., "Meta Ads" and "Kampanie Meta Ads"), merge them into a single entity using the most appropriate or comprehensive name.
6. After processing, create a comprehensive list of at least 20-30 unique entities, ensuring a good mix of general and specific entities related to the central keyword. Format each entity as follows:
   ("ent" | <entity_name> | <entity_type_1>, <entity_type_2>, <entity_type_3 (optional)> | <entity_definition> | <entity_strength>)
7. Review the list of provided entities, considering their types and strengths in relation to the central keyword and each other and create a list of relationships.
- source_entity: Name of the source entity
- target_entity: Name of the target entity
- relationship_description: Precise details indicating the links between the entities, based solely on the provided text
- relationship_strength: Numeric score indicating the strength of the relationship:
-- 90-100: Highly relevant entities or relationships that are directly connected to the central keyword and provide significant value or unique insight.
-- 80-89: Strong entities or relationships with a clear connection to the central keyword, offering useful and relevant information.
-- 70-79: Good entities or relationships that are relevant and provide valuable information but are not as central or unique as higher-scored entities.
-- 60-69: Moderate entities or relationships that have a reasonable connection to the central keyword, providing some useful insights or context.
-- 50-59: Acceptable entities or relationships that have a weaker connection but still provide some relevant information related to the central keyword.
 
8. Calculate the score for each relationship based on the cosine similarity of the entity to the main keyword. Here are the instructions for calculating the score:
   a. Explanation of cosine similarity:
      Cosine similarity is a measure of similarity between two vectors in a multi-dimensional space. In the context of natural language processing, these vectors represent words or phrases in a semantic space. The cosine similarity value ranges from -1 (completely opposite) to 1 (identical), where 0 indicates no similarity.
   b. Simulating embedding calculation:
      - Use your internal model to simulate creating embeddings for the main keyword and each entity.
      - For entities consisting of multiple words, consider the meaning of the entire phrase, not just individual words.
   c. Calculating similarity:
      - Simulate calculating the cosine similarity between the embedding of the main keyword and the embedding of each entity.
      - Transform the result to a scale from 0 to 100, where 0 means no similarity and 100 means full similarity.
   d. Handling multi-word phrases:
      - For entities consisting of multiple words, consider the meaning of the entire phrase in the context of the main keyword.
      - Take into account not only the literal similarity of words but also their semantic connections and context.
   e. Assigning the score:
      - Assign the calculated value as the relationship score.
      - Round the result to the nearest whole number.
9. Review the list of identified entities and apply the following checks:
   a. For each entity, count in how many different sources (URLs) it appears.
   b. If an entity is brand-specific or related to a specific product/website, and it appears in only one source, remove it from the list regardless of its perceived importance.
   c. If a brand-related entity appears in multiple sources, verify that it meets all criteria specified in guideline 18 before keeping it.
   d. For any remaining brand-related entities, ensure they are highly relevant to the central keyword and user intent.
10. Process the temporary list of relationships to remove duplicates:
  a. Sort the list alphabetically by source_entity, then target_entity.
  b. For each relationship, compare it with the next relationship in the list.
  c. If two relationships have the same source_entity and target_entity:
     - If they have the same relationship_description, keep only one instance with the highest relationship_strength.
     - If they have different relationship_descriptions, combine them into a single relationship with a merged description and the highest relationship_strength.
11. After processing, create the final list of unique relationships. Format each relationship as follows:
   ("rel" | <source_entity> | <target_entity> | <relationship_description> | <relationship_strength>)
12. Generalize entities that follow the same pattern or are very similar:
   a. Group entities that have a similar structure, differing only in one or a few words.
   b. For each group of similar entities, create a single, more general entity that encompasses all variations.
   c. Use phrases like "różne okazje", "różne zastosowania", "różne typy", etc., to create a more inclusive entity.
   Examples:
   - Instead of "Karafka z grawerem na różne kolacje", "Karafka z grawerem na różne obiady", "Karafka z grawerem na różne śniadania", etc., create a single entity: "Karafka z grawerem na różne okazje kulinarne".
   - Instead of "skup aut w [różne miasta]", create "Skup aut w różnych lokalizacjach".
13. Review the generalized entities to ensure they still provide meaningful information related to the central keyword and align with user intent. If a generalized entity becomes too broad or loses its relevance, consider keeping the most relevant specific entities instead.
14. Translate relationship descriptions and entity types to [[language_name]]. Keep entity names in their original language.
15. Include only entities and relationships with a relationship_strength of 60 or above with the central keyword, ensuring they align with user intent.
16. Avoid creating entities that are specific to a single URL, especially product lists or brand-specific items, unless they are highly relevant to the central keyword, appear in multiple sources, and align with user intent.
17. Perform a final check for any remaining duplicates or overly similar entities:
   a. Create a set of entity names and a set of (source_entity, target_entity) pairs.
   b. While adding entities and relationships to the final output, check if they're already in the respective set or if there's a very similar entity already present.
   c. If an entity or relationship is already in the set or is very similar to an existing one, do not add it to the final output. Instead, consider if further generalization is possible.
   d. For entities with different names but potentially identical meanings, review their definitions and contexts. If they truly represent the same concept, merge them using the most appropriate or comprehensive name.
18. Output the results as a single list of entities followed by a single list of relationships. Do not repeat the lists or include any additional text or markers.
19. After outputting all entities and relationships, add the {{completed}} marker on a new line.
Remember to critically evaluate entities that appear in only one source, and either exclude them or mark them as potentially source-specific if included. Always ensure that all extracted entities and relationships are relevant to the provided central keyword and align with the likely user intent.
 
## Additional Guidelines for Relationships (kontynuacja)
- Ensure that every entity identified has at least three relationships, with at least one relationship not involving the central keyword "[[keyword]]". These relationships should provide meaningful insights that are not immediately apparent from the entities alone. Encourage the exploration of a wide range of relationships, such as functional connections, complementary features, shared attributes, differences in care requirements, or usage scenarios, to build a robust network of interconnected entities that offer a deeper understanding of the topic and enrich the informational content provided.
- The strength of relationships between different entities should be evaluated based on their relevance to the central keyword and user intent, not just their connection to each other.
- Be cautious of creating too many relationships between different entities that may dilute the focus on the central keyword. Prioritize relationships that directly contribute to understanding the main topic.
- Create only unique and meaningful relationships. Avoid relationships that merely state general similarities or common practices applicable to multiple entities. For example, do not create relationships based solely on similar care requirements or general maintenance practices unless these are specifically relevant to the central keyword.
- Relationships should be designed to form a knowledge graph. This means each relationship should provide a specific, informative connection between entities that adds to the overall understanding of the topic. Focus on relationships that highlight unique interactions, dependencies, contrasts, or synergies between entities.
- When creating relationships, consider the following:
  a) Cause and effect: How does one entity influence or impact another?
  b) Part-whole relationships: Is one entity a component or subset of another?
  c) Temporal or sequential relationships: Does one entity precede or follow another in a process or timeline?
  d) Functional relationships: How do entities work together or complement each other?
  e) Comparative relationships: How do entities differ in important aspects related to the central keyword?
- Avoid creating redundant relationships. If a relationship can be inferred from existing relationships, it should not be explicitly stated.
- Always ensure that relationships start with the central entity "[[keyword]]" when possible, to maintain focus on the main topic.
- Include names of specific products in relationships when they are directly relevant to the central keyword and provide valuable information.
 
## Examples of Good and Bad Entities and Relationships
 
### Good Examples
 
#### Entities:
("ent" | "Central Keyword" | "Main Topic", "Focus Area" | "The primary concept or topic that all other entities and relationships revolve around" | 100)
("ent" | "Subtype A of Central Keyword" | "Subtype", "Variation" | "A specific type or variation of the central keyword with distinct characteristics" | 90)
("ent" | "Related Concept B" | "Related Topic", "Influencing Factor" | "A concept closely related to the central keyword that affects or is affected by it" | 85)
("ent" | "Method C for Central Keyword" | "Technique", "Process" | "A specific method or technique used in relation to the central keyword" | 80)
("ent" | "Tool D for Central Keyword" | "Equipment", "Accessory" | "A tool or piece of equipment commonly used in relation to the central keyword" | 75)
 
#### Relationships:
("rel" | "Central Keyword" | "Subtype A of Central Keyword" | "Subtype A is a specific variation of Central Keyword with unique characteristics X and Y" | 90)
("rel" | "Central Keyword" | "Related Concept B" | "Related Concept B significantly influences Central Keyword by affecting factor Z" | 85)
("rel" | "Method C for Central Keyword" | "Tool D for Central Keyword" | "Tool D is commonly used in Method C to achieve optimal results for Central Keyword" | 80)
("rel" | "Subtype A of Central Keyword" | "Related Concept B" | "Subtype A is particularly affected by Related Concept B due to its specific characteristics" | 75)
 
### Bad Examples
 
#### Entities to Avoid:
("ent" | "Vague Category" | "General", "Broad" | "A very broad and non-specific category related to the topic" | 50)
("ent" | "Unrelated Product X" | "Product", "Brand" | "A specific product not directly related to the central keyword" | 30)
("ent" | "Overly Specific Detail Y" | "Detail", "Specification" | "An extremely specific detail that's not generally relevant to most users" | 40)
("ent" | "Common Knowledge Z" | "General Information", "Basic Fact" | "A piece of information that's too basic and widely known to be useful" | 35)
 
#### Relationships to Avoid:
("rel" | "Central Keyword" | "Unrelated Product X" | "Unrelated Product X is sometimes used by people interested in Central Keyword" | 30)
("rel" | "Subtype A of Central Keyword" | "Overly Specific Detail Y" | "Overly Specific Detail Y is a characteristic of some instances of Subtype A" | 40)
("rel" | "Related Concept B" | "Common Knowledge Z" | "Common Knowledge Z is generally true for Related Concept B and many other topics" | 35)
 
### Explanation of Examples
 
The good examples demonstrate:
1. Clear relevance to the central keyword
2. Specific but not overly detailed entities
3. Meaningful relationships that add value to understanding the topic
4. Appropriate use of entity types and relationship descriptions
5. Realistic strength scores based on relevance and importance
 
The bad examples illustrate:
1. Overly broad or vague entities
2. Irrelevant or loosely connected concepts
3. Extremely specific details that don't add general value
4. Common knowledge that doesn't provide unique insights
5. Weak or uninformative relationships
6. Inappropriate strength scores that don't reflect true relevance or importance
 
When creating entities and relationships, aim to emulate the structure and relevance of the good examples while avoiding the pitfalls shown in the bad examples.
 
## Output Format
The output should consist of three parts:
1. A list of entities, each on a new line, in the format:
   ("ent" | <entity_name> | <entity_type_1>, <entity_type_2>, <entity_type_3 (optional)> | <entity_description> | <entity_strength>)
   The first entity should explicitly contain the central keyword "[[keyword]]" in the entity name or description.
2. Followed by a list of relationships, each on a new line, in the format:
   ("rel" | <source_entity> | <target_entity> | <relationship_description> | <relationship_strength>)
   Relationships should connect entities not only directly to the central keyword "[[keyword]]" but also establish relevant connections between all entities identified. Each entity should have at least one relationship with another entity that does not directly involve the central keyword. This means creating both direct relationships to the central keyword and multiple indirect relationships that explore various connections, such as shared characteristics, functions, complementary uses, or contrasting aspects between entities. Aim to create at least 25-30 relationships by ensuring every entity is connected to multiple others in meaningful ways, enhancing the depth and complexity of the relational network.
3. The {{completed}} marker on a new line after all entities and relationships have been listed.
Do not include any other text, markers, or formatting in the output.
