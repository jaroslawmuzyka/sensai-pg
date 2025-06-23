# Deep SERP analysis (głęboka analiza wyników wyszukiwania)

**Streszczenie:**
Ta lekcja pokazuje, jak przejść od listy rozszerzonych słów kluczowych (query expansion) do głębokiej analizy wyników wyszukiwania (SERP). Celem jest zbudowanie "dużego obrazka" tematu – zrozumienie, jak Google łączy podtematy i jakie strony uznaje za autorytatywne. Proces ten polega na rekursywnym przechodzeniu przez powiązane zapytania i budowaniu rozległych map wiedzy.

---

## Zasada działania: od słowa kluczowego do mapy powiązań
Proces polega na symulowaniu zachowania użytkownika, który zagłębia się w temat. Wychodzimy od listy słów kluczowych z query expansion i "przeklikujemy się" przez powiązane wyszukiwania w Google (People also search for).

Przykładowa ścieżka:
`samochód` → `samochód osobowy` → `samochód używany osobowy` → `samochody używane z salonu`

Każdy krok odkrywa nowy kontekst i powiązane strony, budując kompleksowy obraz dziedziny. W zaawansowanych zastosowaniach analizę można rozszerzyć o autosuggest.

---

## Automatyzacja procesu: Google Colab
Ręczne przeklikiwanie byłoby nieefektywne, dlatego używamy skryptu [Deep Search Analysis w Google Colab](https://colab.research.google.com/drive/1kTx9_TbA43a0hmoOnWI_FhFeoXBZsz6q?usp=sharing), który automatyzuje pobieranie danych z Google za pomocą Serpdata.

**Kluczowe parametry:**
- **Głębokość analizy (Depth):** liczba "kroków" w głąb powiązanych zapytań (w ćwiczeniu: 1)
- **Lokalizacja i język:** ustawienia dla Polski (HL, GL)
- **Liczba wątków:** 5 (przyspiesza proces)

---

## Jak działa skrypt i jakie dane zbiera?
- Skrypt wielowątkowo odpytuje Google dla każdej frazy z listy (i nowo odkrytych).
- Pobiera 10 najlepszych wyników (URL) i analizuje powiązane wyszukiwania.
- Pomija już przeanalizowane zapytania, by uniknąć powtórzeń.
- Usuwa duplikaty URL i grupy z mniej niż 2 adresami (eliminuje szum/outliery).

---

## Wyniki analizy dla tematu "samochód"
- Z 44 fraz z query expansion powstało **192 unikalnych słów kluczowych**.
- Zebrano **586 unikalnych adresów URL** – to nasz korpus wiedzy do dalszej pracy.

---

## Podsumowanie i następny krok
Mamy precyzyjnie wyselekcjonowaną listę 586 stron, które według Google stanowią rdzeń wiedzy o samochodach. W kolejnej lekcji przeanalizujemy treści tych stron, by zbudować z nich grafy wiedzy.

---

## Ważne linki
- Google Colab: [Deep Search Analysis](https://colab.research.google.com/drive/1kTx9_TbA43a0hmoOnWI_FhFeoXBZsz6q?usp=sharing)
- Link do lekcji na platformie: [SensAI Academy](https://learn.sensai.academy/next/public/lesson/338) 