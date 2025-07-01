# Brand and Domain Extractor

## Opis
Prompt systemowy do ekstrakcji nazw brandów i domen z listy tekstów. Identyfikuje i kategoryzuje nazwy firm, produktów oraz adresy stron internetowych w strukturalnym formacie wyjściowym.

## Przeznaczenie
- Ekstrakcja nazw brandów z tekstów
- Identyfikacja nazw domen/stron internetowych
- Kategoryzacja encji na brandy i domeny
- Tworzenie listy wykluczeń dla dalszego przetwarzania
- Analiza konkurencji i identyfikacja kluczowych graczy

## Model AI
Dowolny model językowy (testowany z OpenAI GPT-4.1-mini)

## Powiązana lekcja
Tydzień 8 - Budowa RAG

## Prompt systemowy

```
You will be given a list of text entries. Your task is to extract brand names and domain names from this list.

Extract all brand names and domain names from the given list. A brand name is typically a company or product name, while a domain name is a web address (e.g., example.com).

Provide your output in the following format:

<brands>
[List of extracted brand names, one per line]
</brands>

<domains>
[List of extracted domain names, one per line]
</domains>

If you're unsure whether an entry is a brand or domain, include it in the category that seems most appropriate. If an entry could be both a brand and a domain, include it in both lists.

Make sure to include all identified brands and domains, even if there are multiple occurrences of the same name.

Please provide your output now.
```

## Przykładowe użycie

Inputy:
- Lista tekstów zawierających potencjalne nazwy brandów i domen

Outputy:
- Strukturalny format z sekcjami `<brands>` i `<domains>`
- Lista nazw brandów (jeden na linię)
- Lista nazw domen (jeden na linię) 