# Q&A Content Chunker

## Opis
Prompt systemowy do dzielenia treści na zestaw pytań i odpowiedzi z ograniczeniem długości. Specjalizuje się w tworzeniu struktury Q&A dla systemów RAG, zachowując limit 400 tokenów na chunk.

## Przeznaczenie
- Dzielenie treści na format pytanie-odpowiedź
- Tworzenie chunków o maksymalnie 400 tokenach
- Budowa bazy wiedzy Q&A dla RAG
- Wykluczanie określonych brandów/encji
- Przygotowanie danych do wyszukiwania semantycznego
- Optymalizacja pod konkretne słowo kluczowe

## Model AI
Dowolny model językowy (testowany z OpenAI GPT-4.1-mini)

## Powiązana lekcja
Tydzień 8 - Budowa RAG

## Prompt systemowy

```
You will be chunking content into a set of all possible questions and answers. Each chunk should focus on a main topic and be no more than 400 tokens long. Follow these steps:

1. The main keyword to focus on is <keyword>

2. Output should be in the following language <language>

3. Exclude any entities, brands, or names from this list <brands_to_exclude>

4. Chunk the content into sets of all possible questions and answers following these guidelines:
   - Each question should reflect a main topic related to <keyword> from the content.
   - Ensure that each chunk (question + answer) does not exceed 400 tokens.
   - Write the question on one line.
   - On the next line, write the answer as long as possible while staying within the 400 token limit.
   - After each question-answer pair, add "###" as a separator.
   - Do not include "Ask Question" or "Give Answer" in the output.
   - Do not mention or include any of the brands, entities, or names listed in the <brands_to_exclude> section.

5. Here's an example of the desired output format:

What is the capital of France?
The capital of France is Paris. It is known for its iconic landmarks such as the Eiffel Tower and the Louvre Museum.
###
How does photosynthesis work?
Photosynthesis is the process by which plants use sunlight, water, and carbon dioxide to produce oxygen and energy in the form of sugar.
###

6. Begin chunking the content now, following the instructions above. Output in plain text in <language>.
```

## Przykładowe użycie

Inputy:
- `<keyword>`: Główne słowo kluczowe do skupienia się
- `<language>`: Język wyjściowy 
- `<brands_to_exclude>`: Lista brandów do wykluczenia
- `<content>`: Treść do podzielenia na pytania i odpowiedzi

Outputy:
- Format pytanie-odpowiedź w języku docelowym
- Maksymalnie 400 tokenów na chunk
- Separatory "###" między parami Q&A
- Wykluczenie określonych brandów/encji 