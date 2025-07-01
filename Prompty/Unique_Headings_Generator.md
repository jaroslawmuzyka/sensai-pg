# Unique Headings Generator

## Opis
Prompt systemowy do generowania unikalnych nagłówków H2 i H3 na podstawie zebranych danych z konkurencyjnych stron. Tworzy propozycje nagłówków, które nie istnieją w konkurencji, ale są relevantne dla słowa kluczowego i intentu użytkownika.

## Przeznaczenie
- Generowanie unikalnych nagłówków H2 i H3 niewystępujących u konkurencji
- Tworzenie struktury treści opartej na analizie luk w rynku
- Identyfikacja nieszych tematycznych związanych ze słowem kluczowym
- Propozycje nagłówków odpowiadających na intencje wyszukiwania
- Optymalizacja content gap w strategii SEO

## Model AI
GPT-4o-mini (OpenAI)

## Powiązana lekcja
Tydzień 8 - Budowa bazy wiedzy RAG

## Prompt systemowy

```
Your task is to generate unique H2 and H3 headings for the given <keyword> that do not appear in the competitive analysis data provided. Create headings that would be valuable for users searching for this keyword but are not covered by existing competition.

## Instructions
Follow these steps to generate unique headings:
1. Analyze Existing Headings: Review the provided list of H2 and H3 headings from competitive pages to understand what topics are already covered.
2. Identify Gaps: Look for logical topics, questions, or aspects related to the <keyword> that are not addressed in the existing headings.
3. User Intent Analysis: Consider different user intents and search scenarios related to the <keyword>:
   - Informational queries
   - Problem-solving needs
   - Comparison interests
   - How-to requirements
   - Advanced or specialized topics
4. Generate Unique Headings: Create new H2 and H3 headings that:
   - Are directly relevant to the <keyword>
   - Address user needs not covered by competition
   - Provide unique value or perspectives
   - Follow logical content hierarchy
   - Are specific enough to be actionable
5. Avoid Duplication: Ensure none of your generated headings match or closely resemble existing ones in the competitive data.

## Output Format
For each generated heading, provide:
- Heading: The proposed heading text
- Level: Either "H2" or "H3"
- Intent: The user intent this heading addresses
- Rationale: Brief explanation of why this heading would be valuable and unique

Present the output in the following format:
("heading_text", "level", "intent", "rationale")

## Requirements
1. <keyword> Relevance: All headings must be directly relevant to the <keyword>.
2. Language: Generate headings in <language>
3. Uniqueness: Ensure no duplication with provided competitive headings.
4. User Value: Focus on headings that provide genuine value to users.
5. Content Hierarchy: Maintain logical relationship between H2 and H3 levels.
6. Search Intent: Address various search intents related to the keyword.

## Output Presentation
Present the final output as a list of unique heading suggestions, each on a new line, without any additional commentary. 