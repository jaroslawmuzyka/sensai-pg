# T8L04: Tworzenie treści z AI - Budowa struktury nagłówków

## Opis lekcji

Ta lekcja koncentruje się na drugim kluczowym etapie procesu generacji treści: tworzeniu struktury nagłówków. Jest to krok o fundamentalnym znaczeniu, ponieważ od jego jakości zależy spójność, długość i ostateczna wartość całego artykułu. Zobaczysz, jak wykorzystać nowoczesne modele reasoningowe do tworzenia zoptymalizowanych planów treści oraz jak zautomatyzować ten proces.

---

## 📂 Materiały do pobrania

**Plik workflow do Dify:**  
[Pobierz plik workflow do Dify](https://learn.sensai.academy/download.php?lfid=67)

**Plik automatyzacji do Make.com:**  
[Pobierz plik automatyzacji do Make.com](https://learn.sensai.academy/download.php?lfid=68)

**Automatyzacje z repozytorium:**
- **[SEO 3.0] Budowa nagłówków - blog.yml** - [główny workflow YAML](../../../Automatyzacje/[SEO%203.0]%20Budowa%20nagłówków%20-%20blog.yml)
- **SEO 3.0 [2] - Nagłówki.blueprint.json** - [szablon Blueprint Make.com](../../../Automatyzacje/SEO%203.0%20[2]%20-%20Nagłówki.blueprint.json)

---

## Trzy typy nagłówków do różnych zastosowań

Proces generuje trzy rodzaje struktur nagłówków, które można dopasować do konkretnego celu i miejsca publikacji treści. Wybór zależy od strategicznego znaczenia artykułu w ramach Twojej mapy tematycznej (Topical Map).

### 1. Nagłówki rozbudowane (H2 + H3)
Najbardziej szczegółowa i opasła struktura. Idealna dla artykułów stanowiących rdzeń tematyczny (*core section*) Twojej strony. Taka hierarchiczna budowa (H2 z podpunktami H3) ułatwia tworzenie rozbudowanego linkowania wewnętrznego do powiązanych tematów.

### 2. Nagłówki H2
Typowa, płaska struktura składająca się wyłącznie z nagłówków H2. To standardowy format, który można stosować zamiennie z nagłówkami w formie pytań.

### 3. Nagłówki jako pytania
W opinii prowadzącego, najbardziej przydatny format z perspektywy SEO. Użytkownicy często wpisują w wyszukiwarki pytania, a taka struktura bezpośrednio na nie odpowiada. Doskonale sprawdza się na blogach i w artykułach pomocniczych (*outer section*).

---

## Logika skutecznego promptu dla modeli reasoningowych

Skuteczność generowania nagłówków opiera się na zaawansowanym prompcie, który został zoptymalizowany pod kątem modeli wnioskujących (reasoning models). Dzięki nim cały proces można zamknąć w jednym kroku, w przeciwieństwie do starszych metod wymagających kilku etapów.

### Kluczowe instrukcje w prompcie:

#### 1. Optymalizacja i unikanie redundancji
Model ma za zadanie stworzyć logiczny i zoptymalizowany plan artykułu (*outline*), agresywnie usuwając i grupując zbędne lub powtarzające się tematy. Celem jest plan **"tak krótki, jak to możliwe, i tak długi, jak to wymagane"**.

#### 2. Logiczny przepływ i podróż użytkownika
Nagłówki muszą tworzyć naturalną progresję, gdzie każdy kolejny wynika z poprzedniego. Struktura powinna prowadzić użytkownika od zdefiniowania głównego pojęcia do tematów pomocniczych.

#### 3. Unikanie generycznych fraz
Prompt zawiera zakaz używania typowych, generowanych przez AI nagłówków, takich jak:
- "Wprowadzenie"
- "Podsumowanie" 
- "Conclusion"
- "Ultimate Guide"

#### 4. Wykorzystanie przykładów
Prompt jest zasilony dużą liczbą przykładów świetnie zoptymalizowanych planów artykułów, co pozwala modelowi lepiej zrozumieć pożądany rezultat.

---

## Automatyzacja generowania nagłówków

Proces jest w pełni zautomatyzowany przy użyciu arkusza Google Sheets oraz platformy Make.com. Poniżej przedstawiono kroki konfiguracji.

### Krok 1: Przygotowanie arkusza Google

Do arkusza z poprzedniej lekcji dodawane są nowe kolumny:

- `Nagłówki rozbudowane`
- `Nagłówki H2`
- `Nagłówki jako pytania`
- `Status - Nagłówki` (do sterowania automatyzacją tego etapu)

### Krok 2: Konfiguracja scenariusza w Make.com

Tworzony jest nowy scenariusz, który wykonuje następujące czynności:

#### 1. Wyzwalacz (Trigger)
Scenariusz uruchamia się, gdy w kolumnie `Status - Nagłówki` pojawi się wartość **"generuj"**.

#### 2. Filtr logiczny
Dodano warunek sprawdzający, czy komórka z frazą kluczową nie jest pusta (`exist`). To zabezpieczenie zapobiega błędom, gdy scenariusz próbuje uruchomić się dla już przetworzonego lub pustego wiersza.

#### 3. Pobranie danych i wywołanie API
Scenariusz pobiera dane wejściowe z wiersza (m.in. frazę kluczową i graf informacji z poprzedniego etapu), a następnie wysyła je do odpowiedniego workflow w Deefai poprzez API.

#### 4. Aktualizacja arkusza
Po otrzymaniu odpowiedzi z Deefai, scenariusz wkleja trzy wygenerowane zestawy nagłówków do odpowiednich kolumn w arkuszu i zmienia status w kolumnie `Status - Nagłówki` na **"gotowe"**.

### Krok 3: Wprowadzenie etapu weryfikacji

Na końcu prowadzący dodaje kolejną kolumnę statusu: `Status - Generacja`. Jej celem jest stworzenie manualnego punktu kontrolnego.

Po wygenerowaniu nagłówków i otrzymaniu statusu "gotowe", użytkownik może je przejrzeć, dokonać edycji lub usunąć niechciane elementy. Dopiero po tej weryfikacji ręcznie zmienia status w kolumnie `Status - Generacja` na "generuj", co uruchomi kolejny, ostatni etap procesu: pisanie treści artykułu.

---

## Strategiczne zastosowanie typów nagłówków

### Core Section (Rdzeń tematyczny)
- **Typ nagłówków:** Rozbudowane (H2 + H3)
- **Charakterystyka:** Główne tematy strony, wysokokonkurencyjne frazy
- **Cel:** Maksymalne pokrycie tematyczne, rozbudowane linkowanie wewnętrzne

### Outer Section (Sekcja pomocnicza)
- **Typ nagłówków:** Pytania lub H2
- **Charakterystyka:** Artykuły blogowe, long-tail keywords
- **Cel:** Odpowiedzi na konkretne pytania użytkowników, łatwiejsze pozycjonowanie

### Blog Content
- **Typ nagłówków:** Pytania
- **Charakterystyka:** Tematyka pomocnicza, praktyczne porady
- **Cel:** Wysokie engagement, naturalne wyszukiwania głosowe

---

## Kluczowe korzyści systemu

### 1. Wieloformatowość
Jeden proces generuje trzy różne struktury dopasowane do strategii content marketingowej.

### 2. Optymalizacja SEO
Nagłówki w formie pytań idealnie odpowiadają na zapytania użytkowników w wyszukiwarkach.

### 3. Kontrola jakości
Etap weryfikacji pozwala na manualne sprawdzenie i dostosowanie przed finalną generacją treści.

### 4. Skalowalność
Automatyzacja umożliwia przetwarzanie wielu artykułów równocześnie.

### 5. Spójność
Wykorzystanie reasoning models gwarantuje logiczny przepływ i eliminację redundancji.

---

## Przepływ procesu

```
Dane z etapu 1 (wiedza) 
    ↓
Status "generuj" w kolumnie Nagłówki
    ↓
Trigger Make.com + filtr bezpieczeństwa
    ↓
API call do Dify (reasoning model)
    ↓
Generacja 3 typów nagłówków
    ↓
Zapis do arkusza + status "gotowe"
    ↓
Manualna weryfikacja użytkownika
    ↓
Status "generuj" w kolumnie Generacja → Etap 3
```

---

**Link do lekcji na platformie:** [SensAI Academy - Lekcja T8L04](https://learn.sensai.academy/next/public/lesson/347) 