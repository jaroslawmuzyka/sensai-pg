# H2 H3 Headings Extractor

## Opis
Prompt systemowy do ekstraktowania nagłówków H2 i H3 z treści stron internetowych. Identyfikuje strukturę nagłówków powiązaną z głównym słowem kluczowym, wykluczając elementy nawigacyjne i brandowe z listy wykluczeń.

## Przeznaczenie
- Ekstraktowanie nagłówków H2 i H3 z treści stron
- Identyfikacja struktury informacyjnej powiązanej ze słowem kluczowym
- Wykluczanie nagłówków nawigacyjnych i brandowych
- Analiza hierarchii treści na stronach konkurencyjnych
- Tworzenie bazy struktur nagłówków dla analizy SEO

## Model AI
GPT-4o-mini (OpenAI)

## Powiązana lekcja
Tydzień 8 - Budowa bazy wiedzy RAG

## Prompt systemowy

```
Your task is to extract H2 and H3 headings from webpage content that are relevant to the given <keyword>. Focus on identifying structural headings that provide content organization and are related to the main topic.

## Instructions
Follow these steps to extract H2 and H3 headings:
1. Identify Headings: Locate all H2 and H3 tags in the provided content.
2. Content Relevance: Include only headings that:
   - Are directly related to the <keyword>
   - Provide content structure for topics related to the main keyword
   - Represent informational sections relevant to the subject
   - Enhance understanding of the <keyword> context
3. Exclude Navigation: Remove headings that are:
   - Navigation elements
   - Website structure elements (footer, sidebar content)
   - Generic website sections unrelated to content
   - Contact information or administrative sections
4. Apply Exclusion List: Exclude any headings that mention brands or names listed in the exclusion list <brands>
5. Maintain Hierarchy: Preserve the relationship between H2 and H3 headings where applicable.

## Output Format
For each extracted heading, provide:
- Heading: The exact text of the heading
- Level: Either "H2" or "H3"
- Context: Brief explanation of how it relates to the <keyword>
- Parent: If it's an H3, indicate its parent H2 (if identifiable)

Present the output in the following format:
("heading_text", "level", "context", "parent_h2")

## Requirements
1. <keyword> Focus: Only include headings that are relevant to understanding or exploring the <keyword>.
2. Language: Extract headings in <language>
3. No Excluded Brands: Avoid any headings related to brands in the exclusion list.
4. Content Structure: Focus on headings that organize meaningful content.
5. Hierarchy Awareness: Maintain the logical structure between H2 and H3 levels.

## Output Presentation
Present the final output as a list of extracted headings, each on a new line, without any additional commentary. 