# Automatyczny prompt engineering

Ta lekcja przeprowadzi Cię przez proces automatycznego prompt engineeringu. Dowiesz się, jak wykorzystać modele językowe nie tylko do generowania odpowiedzi, ale również do tworzenia, testowania i optymalizowania samych promptów. W tym celu skorzystamy ze specjalnie przygotowanego notatnika Google Colab.

---

## Idea automatycznego prompt engineeringu

Modele językowe doskonale radzą sobie z tworzeniem promptów. Proces automatycznego prompt engineeringu polega na wykorzystaniu jednych modeli do generowania kandydatów na prompty, a innych do ich oceny i wyboru najlepszego z nich. Kluczowe etapy to:

1. **Generowanie kandydatów na prompty:** Na podstawie opisu zadania (co chcemy osiągnąć za pomocą docelowego promptu), pierwszy model językowy tworzy kilka propozycji (kandydatów) promptów.
2. **Ewaluacja i ranking:** Drugi model językowy ocenia wygenerowanych kandydatów, porównując ich skuteczność na podstawie predefiniowanych przypadków testowych (test case'ów).
3. **Wybór najlepszego promptu:** Do wyboru najlepszego promptu wykorzystywany jest system rankingu, np. ranking ELO, pierwotnie stworzony dla szachistów.

---

## Praktyczne zastosowanie: Notatnik Google Colab

Do przeprowadzenia procesu automatycznego prompt engineeringu wykorzystamy dedykowany notatnik Google Colab.

**Link do notatnika:** [https://colab.research.google.com/drive/1HCzAn1J5PgPPU9DtbcpwDUPDwY9sSwiM?usp=sharing](https://colab.research.google.com/drive/1HCzAn1J5PgPPU9DtbcpwDUPDwY9sSwiM?usp=sharing)

*Pamiętaj, aby przed rozpoczęciem pracy skopiować notatnik na swój dysk Google. Oryginalny notatnik został stworzony przez Matthew Hammera, a następnie dostosowany przez Damiana do aktualnych modeli językowych.*

---

### Krok 1: Przygotowanie środowiska

- **Instalacja bibliotek:** Pierwsza komórka notatnika instaluje niezbędne biblioteki, w tym OpenAI oraz inne biblioteki wspomagające.
- **Klucz API OpenAI:** Do korzystania z notatnika (w jego obecnej formie) potrzebny będzie klucz API OpenAI. Należy go wprowadzić w odpowiednim polu. Notatnik można dostosować do innych dostawców modeli (np. Gemini), modyfikując odpowiednio kod.

---

### Krok 2: Konfiguracja meta-promptów

Notatnik wykorzystuje dwa główne prompty sterujące procesem:

- **Prompt do generowania promptów (meta-prompt):** Instrukcja dla pierwszego modelu, jak ma tworzyć kandydatów na docelowy prompt. Wykorzystuje on metodologie zoptymalizowane dla modelu GPT-4.1.
- **Prompt do rankingu promptów:** Instrukcja dla drugiego modelu, jak ma oceniać i porównywać (np. prompt A vs prompt B) wygenerowanych kandydatów na podstawie wyników z test case'ów.

*Te prompty można modyfikować i dostosowywać do własnych potrzeb i celów.*

---

### Krok 3: Konfiguracja parametrów generowania

W tej sekcji ustawiamy kluczowe parametry procesu:

- **Plik z przypadkami testowymi (test case'y):** Należy wczytać plik (np. z GitHub, folder "Datasety") zawierający dane testowe. W przykładzie używane są pliki JSON zawierające "main keyword" i "keywordy towarzyszące" do generowania konspektów artykułów. Można ograniczyć liczbę używanych test case'ów (np. 20 z dostępnych 245).
- **Wybór modeli językowych:**
  - **Model do generowania kandydatów:** Np. GPT-4.1, który generuje kilka wstępnych wersji promptu.
  - **Model do generowania odpowiedzi:** Model, który będzie używany z testowanymi promptami do generowania faktycznych odpowiedzi na podstawie test case'ów.
  - **Model do rankingu:** Model oceniający, który prompt jest lepszy (np. GPT-4.1).
  *Pamiętaj, że różne modele (np. reasoningowe, GPT-4.0, GPT-4.1) mogą wymagać nieco innej specyfiki promptowania.*
- **Parametry temperatury:** Zazwyczaj nieco wyższa dla generowania promptów i odpowiedzi (większa kreatywność), a niższa dla rankingu (bardziej deterministyczna ocena).
- **Liczba kandydatów na prompt:** Ile startowych wersji promptu ma wygenerować model (np. 5 lub 7).
- **Maksymalna liczba plików do testu:** Ile przypadków testowych z wczytanego pliku zostanie użytych.
- **Maksymalna liczba tokenów odpowiedzi:** Jak długa może być odpowiedź generowana przez testowany prompt.
- **Liczba prób ponowienia:** Ile razy model ma próbować połączyć się z API w razie niepowodzenia.
- **Współczynnik K (dla rankingu ELO):** Parametr algorytmu rankingowego.

---

### Krok 4: Definicja funkcji i zadania głównego

- **Definicje głównych procesów/funkcji:** Komórka zawierająca kod funkcji realizujących poszczególne etapy – nie wymaga konfiguracji.
- **Definicja zadania głównego:** Tutaj opisujesz, co ma realizować docelowy prompt. Np. `"generate a detailed, so-optimized article outline based on the provide keywords, focusing on creating in a comprehensive logic"`. Im więcej szczegółów i precyzji w opisie, tym lepiej model generujący prompty zrozumie zadanie. Ten opis trafi jako instrukcja do modelu generującego kandydatów na prompty.

---

### Krok 5: Uruchomienie procesu głównego

Po skonfigurowaniu wszystkich powyższych elementów uruchamiamy główny proces:

1. Model generuje zadaną liczbę kandydatów na prompty na podstawie Twojego opisu i przykładowych test case'ów.
2. Następnie każdy z wygenerowanych promptów jest testowany na określonej liczbie przypadków testowych. Model rankingujący porównuje wyniki (np. dla 7 promptów i 20 test case'ów może to oznaczać dużą liczbę porównań i zapytań do API – np. 420, co wiąże się z kosztami).
3. Po zakończeniu obliczeń otrzymujemy ranking promptów wraz z ich punktacją ELO.

---

### Krok 6: Analiza wyników

- Notatnik prezentuje listę wygenerowanych i przetestowanych promptów, uszeregowanych według ich skuteczności (punktacji ELO). Prompt z najwyższą punktacją jest uznawany za najlepszy dla danego zadania i zestawu testowego.
- Wyniki są również dostępne w formie pliku HTML, który można pobrać i udostępnić.

---

## Zalety automatycznego prompt engineeringu

Takie podejście pozwala na:

- Systematyczne i obiektywne tworzenie oraz testowanie promptów.
- Szybką optymalizację i iterację nad promptami.
- Znalezienie najlepiej działającego promptu dla konkretnego zadania w oparciu o dane.

Jest to potężna technika pozwalająca na efektywniejsze wykorzystanie modeli językowych. 