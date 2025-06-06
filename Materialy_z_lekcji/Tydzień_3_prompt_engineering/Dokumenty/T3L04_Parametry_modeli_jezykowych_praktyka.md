# Parametry modeli językowych – praktyka

Niniejsza notatka przedstawia praktyczne aspekty konfiguracji parametrów modeli językowych. Skupimy się na demonstracji działania tych parametrów w popularnych narzędziach takich jak OpenAI Playground, Workbench od Anthropic (Claude) oraz Google AI Studio, a także na ich praktycznym wykorzystaniu w środowisku Google Colab.

**Link do omawianego Google Colab:**  
[https://colab.research.google.com/drive/1dfTAIF0gVNEfprf17u3ppZkDigI2yuOA?usp=sharing](https://colab.research.google.com/drive/1dfTAIF0gVNEfprf17u3ppZkDigI2yuOA?usp=sharing)

---

## Narzędzia do testowania i konfiguracji parametrów

Zanim zaczniemy korzystać z modeli językowych poprzez API, warto przetestować ustawienia i prompty w dedykowanych do tego narzędziach:

- **OpenAI Playground:** Pozwala na testowanie promptów i konfiguracji przed użyciem API. Umożliwia zdefiniowanie instrukcji systemowej i obserwację wpływu różnych parametrów na generowane treści.
- **Anthropic Workbench (Claude):** Służy do konfiguracji pola systemowego i promptu dla modeli Claude. Oferuje bardziej ograniczony zestaw parametrów w porównaniu do OpenAI.
- **Google AI Studio:** Jest odpowiednikiem Playgroundu OpenAI dla modeli Google, takich jak Gemini. Umożliwia wybór modelu i dostosowanie jego specyficznych parametrów.

---

## Kluczowe parametry modeli językowych i ich wpływ

### 1. Temperatura
- **Definicja:** Parametr kontrolujący losowość generowanych tokenów. Nie jest to bezpośrednio "kreatywność", a raczej stopień przypadkowości w wyborze kolejnych słów.
- **Skala:** Różni się w zależności od narzędzia (np. 0-2 w OpenAI, 0-1 w Claude). Niskie wartości (np. 0) prowadzą do bardziej powtarzalnych i przewidywalnych odpowiedzi, odpowiednich dla zadań klasyfikacyjnych czy analitycznych. Wyższe wartości (np. 1 w OpenAI) sprzyjają generowaniu bardziej zróżnicowanych i "kreatywnych" treści, ale zbyt wysoka wartość (np. 2 w OpenAI) może skutkować generowaniem bezsensownych, losowych ciągów tokenów.
- **Zastosowanie:** Niska temperatura dla zadań wymagających precyzji (np. klasyfikacja), wyższa dla zadań kreatywnych (np. pisanie treści).

### 2. Maximum Tokens (Maksymalna liczba tokenów)
- **Definicja:** Określa maksymalną liczbę tokenów, jaką model może wygenerować w odpowiedzi. Różne modele mają różne limity tokenów na wejściu i wyjściu.
- **Ważność:** Istotne jest przewidzenie potrzebnej długości odpowiedzi i ustawienie odpowiedniego limitu, aby uniknąć ucięcia treści lub, w przypadku API, generowania zbyt długich (i kosztownych) odpowiedzi, zwłaszcza gdy model mógłby się zapętlić. Przykładowo, model GPT-4O ma 128 tys. tokenów kontekstu, ale tylko 4095 na wyjściu w Playground.
- **Praktyka:** Należy dostosować ten parametr do zadania, np. generując strukturę JSON z HTML, trzeba przewidzieć rozsądną długość, aby uniknąć przetwarzania bardzo długich, niepotrzebnych ciągów znaków.

### 3. Top P
- **Definicja:** Alternatywny sposób kontrolowania losowości. Model wybiera tokeny z najbardziej prawdopodobnego zestawu, którego suma prawdopodobieństw przekracza wartość Top P. Np. Top P = 0.5 oznacza wybór z 50% najbardziej prawdopodobnych tokenów.
- **Wpływ:** Podobnie jak temperatura, niższe wartości prowadzą do bardziej przewidywalnych wyników. W praktyce często używa się głównie temperatury, ale warto znać działanie Top P.

### 4. Frequency Penalty (Kara za częstotliwość)
- **Definicja:** Penalizuje tokeny na podstawie ich dotychczasowej częstotliwości występowania w generowanym tekście.
- **Cel:** Zachęca model do używania bardziej zróżnicowanego słownictwa i unikania powtarzania tych samych słów.

### 5. Presence Penalty (Kara za obecność)
- **Definicja:** Penalizuje tokeny, które już pojawiły się w tekście, niezależnie od ich częstotliwości.
- **Cel:** Zwiększa skłonność modelu do podejmowania nowych tematów i unikania powielania informacji. W niektórych niszowych tematach może pomóc uniknąć powtarzania tych samych faktów.
- **Praktyka:** Te dwa parametry (Frequency i Presence Penalty) nie zawsze znajdują zastosowanie, szczególnie przy wieloetapowym tworzeniu treści, gdzie oczyszczanie i humanizacja tekstu odbywa się w późniejszych krokach.

### 6. Top K (w Google AI Studio)
- **Definicja:** Model rozważa 'K' najbardziej prawdopodobnych tokenów podczas generacji. Jeśli Top K ustawione jest na 3, model wybierze spośród trzech najbardziej prawdopodobnych następnych tokenów.

### 7. Format odpowiedzi
- **Opcje:** Modele mogą zwracać odpowiedzi w różnych formatach, np. czysty tekst, obiekt JSON. Ta funkcja jest przydatna do strukturyzowanych danych wyjściowych.

---

## Parametry specyficzne dla modeli "reasoningowych"

Modele "reasoningowe" (służące do rozumowania) różnią się od klasycznych modeli i posiadają inne parametry. Nie obsługują one np. temperatury czy limitu tokenów w ten sam sposób.

- **Reasoning Effort:** Określa "wysiłek", jaki model ma poświęcić na wewnętrzne rozumowanie przed wygenerowaniem odpowiedzi. W modelach OpenAI może przyjmować wartości np. "low", "medium", "high". Większy wysiłek oznacza więcej wewnętrznych kroków rozumowania, co może prowadzić do lepszych odpowiedzi, ale także większego zużycia tokenów i dłuższego czasu generacji.
- **Max Completion Tokens:** Kontroluje maksymalną długość samej odpowiedzi, ale nie obejmuje tokenów zużytych na wewnętrzne rozumowanie modelu.
- **Zastosowanie:** Modele te są używane np. do kodowania lub złożonych, pojedynczych zadań. Są jednak wolniejsze i dają mniejszą kontrolę nad outputem niż modele klasyczne, dlatego rzadziej stosuje się je w typowych zadaniach SEO czy automatyzacjach contentowych.

---

## Praktyczne ćwiczenia w Google Colab

W dostarczonym notatniku Google Colab można praktycznie przetestować wpływ parametrów (głównie na przykładzie API OpenAI):

1. **Instalacja bibliotek i konfiguracja kluczy API.**
2. **Testowanie Temperatury:** Uruchomienie tego samego promptu z różnymi ustawieniami temperatury (np. 0.1, 0.7, 1.4) w celu zaobserwowania różnic w losowości i jakości generowanego tekstu.
3. **Testowanie Top P:** Porównanie działania Top P z temperaturą.
4. **Testowanie Maximum Tokens:** Obserwacja, jak model przerywa generowanie po osiągnięciu zadanego limitu tokenów (powód zakończenia: "length").
5. **Testowanie Frequency i Presence Penalty:** Generowanie tekstów z różnymi ustawieniami tych kar, aby zobaczyć ich wpływ na powtórzenia i zróżnicowanie treści.
6. **Testowanie Reasoning Effort (dla modeli reasoningowych):** Porównanie wyników i zużycia tokenów (całkowitego i na rozumowanie) dla różnych poziomów "wysiłku" (low, medium, high).

---

## Podsumowanie i dobre praktyki

- Zawsze dostosowuj parametry do konkretnego zadania i używanego modelu.
- Skale parametrów (szczególnie temperatury) mogą się różnić między dostawcami modeli.
- Uważnie zarządzaj parametrem "Maximum Tokens", aby kontrolować długość odpowiedzi i potencjalne koszty.
- W przypadku modeli "reasoningowych" bądź świadomy znacznie większego potencjalnego zużycia tokenów i dłuższego czasu odpowiedzi. Zawsze ograniczaj maksymalną liczbę tokenów na wyjściu.
- Dokumentacja konkretnego modelu jest najlepszym źródłem informacji o obsługiwanych parametrach i ich specyfice. 