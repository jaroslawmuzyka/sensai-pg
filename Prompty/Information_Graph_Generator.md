# Prompt do generowania grafu informacji (Information Graph)

Zadaniem AI jest wyodrębnienie informacji z podanego tekstu i utworzenie grafu informacji w postaci trójek semantycznych. Proces obejmuje dwa główne kroki: ekstrakcję informacji oraz budowę grafu. Postępuj zgodnie z poniższymi instrukcjami.

---

## Instrukcja

Najpierw otrzymasz tekst. Przeczytaj go uważnie i zidentyfikuj kluczowe informacje, encje oraz relacje.

### Krok 1: Ekstrakcja informacji
- Uważnie przeczytaj tekst i zidentyfikuj ważne encje, pojęcia i relacje.
- Zwróć uwagę na imiona, daty, miejsca, wydarzenia i inne istotne informacje.
- Zapisz, jak te elementy są ze sobą powiązane w kontekście tekstu.

### Krok 2: Budowa grafu informacji
- Na podstawie wyodrębnionych informacji utwórz graf informacji w postaci trójek semantycznych.
- Każda trójka powinna mieć format JSON:

```
{
  "Subject": "wartość",
  "Predicate": "wartość",
  "Object": "wartość"
}
```

- Podmiot (Subject) i dopełnienie (Object) to encje lub pojęcia, a orzeczenie (Predicate) opisuje relację między nimi.
- Upewnij się, że Twoje trójki obejmują wszystkie kluczowe informacje z tekstu.
- Dąż do jasności i zwięzłości w formułowaniu trójek.

---

## Wytyczne dotyczące formatowania wyniku
- Przedstaw trójki semantyczne w formacie listy.
- Każda trójka powinna być w osobnej linii.
- Użyj nawiasów klamrowych dla każdej trójki.
- Oddziel podmiot, orzeczenie i dopełnienie przecinkami w obrębie trójki.
- Upewnij się, że trójki razem dają pełny obraz informacji zawartych w tekście.

---

### Przykład formatu JSON:

[
  {
    "Subject": "Jan Kowalski",
    "Predicate": "jest",
    "Object": "polskim pisarzem"
  },
  {
    "Subject": "Jan Kowalski",
    "Predicate": "urodził się w",
    "Object": "1980 roku"
  },
  {
    "Subject": "Jan Kowalski",
    "Predicate": "napisał",
    "Object": "Zielone Wzgórza"
  },
  {
    "Subject": "Zielone Wzgórza",
    "Predicate": "zostały opublikowane w",
    "Object": "2005 roku"
  },
  {
    "Subject": "Jan Kowalski",
    "Predicate": "otrzymał",
    "Object": "Nagrodę Literacką Nike"
  },
  {
    "Subject": "Nagroda Literacka Nike",
    "Predicate": "została przyznana w",
    "Object": "2010 roku"
  }
]

---

Wynik wygeneruj w języku polskim. 