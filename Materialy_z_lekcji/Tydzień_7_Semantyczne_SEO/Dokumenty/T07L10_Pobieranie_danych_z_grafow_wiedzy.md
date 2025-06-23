# Pobieranie danych z grafów wiedzy

**Opis:**
Ta lekcja pokazuje, jak przejść od wizualizacji grafu wiedzy do jego praktycznego wykorzystania. Nauczysz się eksportować dane o encjach i relacjach, a następnie użyć ich do stworzenia mapy tematycznej (Topical Map) za pomocą AI. Celem jest odwzorowanie struktury wiedzy Google na własnej stronie.

---

## Krok 1: Pobieranie danych z grafu wiedzy
- W Colabie znajduje się skrypt do eksportowania danych z bazy grafowej.
- **Wybierz centralną encję:** np. `samochód`.
- **Ustaw siłę powiązań (Strength):**
  - 90-100%: Core Unique (fundament rdzenia tematycznego)
  - 80-90%: Strong Direct (mocno powiązane tematy)
  - <80%: Relevant Contextual (zewnętrzna warstwa mapy)
- W ćwiczeniu ustawiono 80-100%. Skrypt wygeneruje listę encji połączonych z "samochodem" w tym zakresie.

---

## Krok 2: Generowanie mapy tematycznej za pomocą AI
- Skopiuj listę połączeń i wklej do czatu AI z promtem "knowledge graph i topical map".
- Model AI podzieli tematy na logiczne klastry i stworzy strukturę mapy tematycznej.
- **Uwaga:** Dla automatyzacji warto generować wyniki w formacie JSON.

---

## Krok 3: Analiza wyników i rola "Source Context"
- AI może wygenerować szeroką mapę, jeśli nie podasz "Source Context" (czym się zajmujesz, np. "sprzedajemy tylko samochody elektryczne").
- Dodanie kontekstu pozwala precyzyjnie dopasować mapę do Twoich potrzeb i intencji użytkowników.

---

## Krok 4: Zastosowanie grafu do planowania linkowania wewnętrznego
- Relacje w grafie to "mosty kontekstowe" (Contextual Bridges) – podstawa do linkowania wewnętrznego.
- Możesz zapytać AI o kontekst linkowania między dwiema encjami (np. "samochód" i "klimatyzacja").
- Odpowiedź AI wskaże, jak i dlaczego połączyć te tematy na stronie.

---

## Podsumowanie i co dalej?
Lekcja pokazuje inżynierskie podejście do budowania struktur treści na bazie danych. Klucz to koncentracja na encjach, nie słowach kluczowych, i odzwierciedlenie sposobu, w jaki Google postrzega świat. W kolejnym tygodniu tematem będzie content briefing.

---

## Ważne linki
- Link do lekcji na platformie: [SensAI Academy](https://learn.sensai.academy/next/public/lesson/342) 