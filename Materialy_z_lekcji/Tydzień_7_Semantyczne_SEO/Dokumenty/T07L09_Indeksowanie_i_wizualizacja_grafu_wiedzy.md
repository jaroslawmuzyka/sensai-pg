# Indeksowanie i wizualizacja grafu wiedzy w bazie danych

**Opis:**
Ta lekcja pokazuje, jak zaindeksować przygotowany wcześniej graf wiedzy w grafowej bazie danych Neo4j i zwizualizować go w formie interaktywnych "bąbelków". Pozwala to na graficzną eksplorację połączeń między encjami i lepsze zrozumienie struktury wiedzy.

---

## Krok 1: Przygotowanie środowiska i konfiguracja
- **Instalacja biblioteki:** W Google Colab zainstaluj wymaganą bibliotekę (pojawia się komunikat `successful`).
- **Dane dostępowe:** Wprowadź swoje dane do połączenia z bazą (Forj Pass, Forj ID).
- **Liczba wątków:** Skrypt pozwala ustawić liczbę wątków (np. 5) dla szybszego przetwarzania.

---

## Krok 2: Uruchomienie skryptu indeksującego
- Skrypt automatycznie czyści i optymalizuje dane.
- **Deduplikacja węzłów i relacji:** Zapobiega powielaniu tych samych encji i relacji.
- **Walidacja danych:** Użycie polecenia `MERGE` zapewnia spójność i brak duplikatów.
- Po uruchomieniu pojawiają się komunikaty potwierdzające deduplikację.

---

## Krok 3: Eksploracja zwizualizowanego grafu wiedzy
- Po zakończeniu indeksowania (np. 3891 węzłów i relacji) można przejść do wizualnej eksploracji w interfejsie Neo4j.
- **Interaktywna analiza:** Klikaj na węzły, by zobaczyć ich sąsiadów i relacje.
- **Przykłady:**
  - Węzeł "samochód" – sąsiedzi: "Renault Clio", "Honda Civic", "Skoda Octavia", "kredyt samochodowy".
  - Relacje są opisane i skierowane (np. "Renault Clio" → "samochód" z opisem `instance of`).
  - Wyszukiwarka pozwala znaleźć konkretne węzły (np. "hatchback", "samochód elektryczny").

---

## Krok 4: Analiza przykładów i outliery
- Graf pokazuje wiedzę wyciągniętą z treści.
- **Przykłady:**
  - "Hatchback" – powiązania z "Ford Focus" i "Hyundai i20".
  - "Samochód elektryczny" – powiązania z "Tesla", "Dacia Spring", "Nissan Leaf", "BMW i3".
  - "Rejestracja samochodu zza granicy" – relacja `wymaga` z "przetłumaczone dokumenty" i "potwierdzenie opłacenia akcyzy".
- **Outliery:** Węzły niepowiązane (np. "historia samochodu") wynikają z ograniczonej głębokości analizy.

---

## Podsumowanie i następne kroki
Stworzony graf to żywa, interaktywna reprezentacja wiedzy, którą można przeszukiwać i analizować. Będzie się rozwijał wraz z dodawaniem nowych danych. Następny krok to analityka grafu i budowa mapy tematycznej.

---

## Ważne linki
- Link do lekcji na platformie: [SensAI Academy](https://learn.sensai.academy/next/public/lesson/341) 