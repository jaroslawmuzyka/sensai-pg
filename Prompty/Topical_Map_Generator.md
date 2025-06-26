# Prompt do budowy mapy tematycznej (Topical Map)

You are an expert SEO Content Strategist and Knowledge Architect. Your task is to analyze a provided knowledge graph for the central entity *Keyword* and transform it into a comprehensive, hierarchical semantic topical map. This map will serve as the master blueprint for a website's content strategy, designed to establish absolute topical authority.

# Input Data:
You will be provided with a knowledge graph in the following format:

  {
    "source_entity": "samochód",
    "relationship": "ma_typ",
    "target_entity": "samochód z napędem hybrydowym",
    "relationship_description": "samochód może być z napędem hybrydowym, co wyróżnia się ekonomicznością i niższymi kosztami eksploatacji",
    "relationship_strength": 98
  },
  ...


# Critical Instructions:
Structure your output into two primary sections: "Core Section (Main Topics)" and "Outer Section (Supplementary Topics)".

You can only use data from given knowledge graph

## Core Section (Main Topics):
This section must contain the foundational pillar topics that are essential for covering the central entity *Keyword* comprehensively. Give all possible topics to cover central entity

Criteria for Inclusion:
- Identify the entities with "relationship_strength">=80 from the knowledge graph. These are your primary candidates for pillar pages.
- Analyze the primary attributes and defining characteristics of the central entity *Keyword*.
- Group the most fundamental user_questions (e.g., "What is...", "How does it work...", "Benefits of...", "Types of...").

Output Format: Present this as a full hierarchical list. Each item should represent a proposed pillar content piece.

## Outer Section (Supplementary Topics):
This section must cover the peripheral, supporting, and niche topics that provide depth and demonstrate true expertise beyond the basics. Give all possible topics based on given knowledge graph.

Criteria for Inclusion:
- Include topics based on "relationship_strength"<80 but still important.
- Address highly specific user_questions and those that represent "information gain" opportunities (topics competitors might miss).
- Incorporate comparison topics (e.g., "vs" queries).
- Group niche sub-topics and related concepts (e.g., specific car types, technologies, expert opinions).

Output Format: Present this as a full categorized list. Group related topics into logical sub-clusters (e.g., "Car Types," "Maintenance," "Advanced Technologies").

# Example Structure:

Primary Entity: Car

Core Section (Main Topics)
1. What is a Car? (The Definitive Guide)
2. How Cars Work: Engine, Transmission, and Key Components
3. Types of Cars: From Sedans to SUVs
4. Benefits of Car Ownership
5. Car Safety Features and Regulations

Outer Section (Supplementary Topics)
Cluster: Car Maintenance
- Essential Car Maintenance Tips
- DIY Car Repairs for Beginners

Cluster: Car Technologies
- Electric vs. Hybrid vs. Gasoline Cars
- Advanced Driver Assistance Systems (ADAS)

Cluster: Car Buying Guide
- New vs. Used Cars: Pros and Cons
- How to Negotiate Car Prices

Cluster: Car Culture
- Famous Car Brands and Their Histories
- Car Enthusiast Communities and Events


# Task:

Analyze the provided knowledge graph and generate the Semantic Topical Map according to all the instructions above. Ensure the structure is clear, logical, and directly actionable for a content team. In each cluster, add all possible topics derived from the knowledge graph.

Format your output in the form of a logical table with the following columns:
1. Section (Core or Outer)
2. Topic/Cluster
3. Subtopics (if applicable)

Your final output should only include the formatted table without any additional explanations or notes.

Output in Polish



Keyword:  {fraza kluczowa}

Knowledge graph: 

{knowledge graph tutaj}