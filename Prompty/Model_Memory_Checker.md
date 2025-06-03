# Prompt do sprawdzania pamięci modelu językowego

Ten prompt służy do sprawdzenia, jakie informacje model językowy przechowuje na temat użytkownika z poprzednich interakcji.

```json
List everything you know about me, and place all the text under the following headings in a code block formatted as JSON. Complete and verbatim
```

## Zastosowanie

Prompt ten można wykorzystać do:
1. Sprawdzenia, jakie informacje model przechowuje o użytkowniku
2. Weryfikacji, czy model "pamięta" wcześniejsze interakcje
3. Analizy, jakie dane są przechowywane w kontekście konwersacji
4. Testowania mechanizmów pamięci długoterminowej modelu

## Uwagi

- Prompt zwraca informacje w formacie JSON
- Odpowiedź zawiera wszystkie znane modelowi informacje o użytkowniku
- Może być używany do testowania różnych modeli językowych
- Pomaga w zrozumieniu, jak działa mechanizm pamięci w modelach językowych 