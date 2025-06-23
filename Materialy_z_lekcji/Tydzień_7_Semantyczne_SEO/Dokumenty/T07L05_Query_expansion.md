# Query expansion (rozszerzanie zapytań)

**Streszczenie:**
Ta lekcja koncentruje się na technice *query expansion* (rozszerzania zapytań) – kluczowym pierwszym kroku w budowaniu mapy tematycznej. Pozwala ona wyjść poza analizę pojedynczego słowa kluczowego i zbudować szeroki zestaw powiązanych fraz i pytań, które lepiej oddają intencje użytkowników i strukturę tematu.

---

## Narzędzie: Google Colab do automatyzacji procesu
Do przeprowadzenia procesu query expansion wykorzystaj przygotowany skrypt w [Google Colab](https://colab.research.google.com/drive/1kTx9_TbA43a0hmoOnWI_FhFeoXBZsz6q?usp=sharing). Pozwala on automatycznie wygenerować listę rozszerzonych fraz i pytań na podstawie jednego słowa kluczowego.

**Konfiguracja skryptu:**
- **Keyword:** Wprowadź centralne pojęcie (np. `samochód`).
- **Język:** Określ język operacji (np. `polski`).
- **Model AI:** Zalecany Gemini 1.5 Pro (Open Router), można też użyć modeli OpenAI (unikać modelu Flash).

---

## Jak działa proces rozszerzania zapytań?
Skrypt naśladuje proces, który zachodzi w wyszukiwarce Google – tzw. *keyword-to-query transformation*. Google rzadko traktuje jednowyrazowe zapytanie dosłownie, lecz przepisuje je na bardziej szczegółowe frazy na podstawie intencji i kontekstu.

**Zasady rozszerzania:**
- **Synonimy i warianty:** samochód → auto, pojazd
- **Szersze i węższe koncepcje:** samochód → samochód sportowy, samochód elektryczny
- **Powiązane pojęcia techniczne:** samochód → auto, bus
- **Pytania i intencje:** kto, co, gdzie, kiedy, dlaczego, jak
- **Porównania:** samochód elektryczny versus samochód hybrydowy

---

## Przykładowe wyniki dla słowa „samochód”

**Wygenerowane frazy:**
- auto, pojazd
- samochód sportowy, samochód elektryczny, samochód hybrydowy

**Wygenerowane pytania:**
- Jaki samochód kupić?
- Co to jest samochód?
- Gdzie kupić samochód?
- Jak działa samochód elektryczny?
- Jak przygotować samochód do sprzedaży?
- Koszt utrzymania samochodu.

Dzięki tej liście można badać aktualny konsensus w Google na temat szeroko pojętej kategorii samochodów, a nie tylko jednego hasła.

---

## Dodatkowe zasoby
- Artykuł o query expansion: [Query Expansion with LLMs – Searching Better by Saying More (Jina AI)](https://jina.ai/news/query-expansion-with-llms-searching-better-by-saying-more/)
- [Google Colab: Automatyzacja query expansion](https://colab.research.google.com/drive/1kTx9_TbA43a0hmoOnWI_FhFeoXBZsz6q?usp=sharing)

---

## Podsumowanie
Wykonaliśmy pierwszy, fundamentalny krok – query expansion. Zamiast jednej frazy, mamy bogaty zestaw zapytań, które posłużą w kolejnym etapie: głębokiej analizie wyników wyszukiwania (SERP analysis). 