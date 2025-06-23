# Proces budowy map tematycznych

Ta lekcja jest wprowadzeniem do zaawansowanego procesu budowania mapy tematycznej (topical map). Poznasz poszczególne etapy, które pozwolą Ci tworzyć kompleksowe strategie contentowe w oparciu o dogłębną analizę działania wyszukiwarki Google.

---

## Schemat procesu budowy mapy tematycznej

```
START
  |
  v
[1] Rozbudowa zapytań (query expansion)
  |
  v
[2] Głęboka analiza SERP (deep SERP analysis)
  |
  v
[3] Dekompozycja i rekompozycja do grafu wiedzy
  |
  v
[4] Wykorzystanie grafowej bazy danych (Neo4j)
  |
  v
[5] Wnioskowanie i budowa fraz kluczowych
  |
  v
STOP
```

---

## Krok 1: Rozbudowa zapytań (query expansion)
Proces rozpoczyna się od rozszerzenia początkowego słowa kluczowego. Celem jest odtworzenie sposobu, w jaki Google interpretuje i rozwija zapytania użytkowników. Zamiast skupiać się na pojedynczej frazie, jak „samochód”, generujemy zestaw powiązanych zapytań, np. „czym jest samochód”, „jakie są rodzaje samochodów” czy „samochód nowy a używany”. Stanowi to fundament do dalszej, głębszej analizy.

## Krok 2: Głęboka analiza SERP (deep SERP analysis)
Ten etap polega na dogłębnej analizie wyników wyszukiwania (SERP) dla rozbudowanych wcześniej zapytań. W przeciwieństwie do narzędzi SEO, których bazy danych mogą być aktualizowane co kilka miesięcy, analiza bieżących wyników Google daje wgląd w aktualny „konsensus” na dany temat. To pozwala zrozumieć, jakie informacje i jakie konteksty wyszukiwarka uważa za najważniejsze tu i teraz, co daje przewagę nad konkurencją opierającą się wyłącznie na danych z narzędzi.

## Krok 3: Dekompozycja i rekompozycja do grafu wiedzy
Na tym etapie analizujemy setki stron internetowych z wyników wyszukiwania, aby dokonać ich "dekompozycji" – czyli rozłożenia na czynniki pierwsze. Następnie składamy te elementy na nowo (rekompozycja) w postaci grafów wiedzy. Celem jest zrozumienie, jak Google strukturyzuje i łączy informacje w danej niszy. Ten proces można porównać do rekompozycji na siłowni: zamiast budować pustą „masę” (stare, nieefektywne treści) lub tylko „redukować” (usuwać content), jednocześnie spalamy tłuszcz i budujemy masę mięśniową, tworząc skuteczną i wartościową strukturę tematyczną.

## Krok 4: Wykorzystanie grafowej bazy danych Neo4j
Ponieważ w wyniku analizy powstaną setki grafów, których nie da się efektywnie przetworzyć w standardowym oknie czatu, wprowadzimy dedykowane narzędzie: **Neo4j**. Jest to darmowa grafowa baza danych, która służy do przechowywania, zarządzania i wizualizacji skomplikowanych relacji między danymi. Pozwoli to na logiczne połączenie wszystkich informacji i cykliczne odświeżanie grafu w oparciu o nowe dane z wyszukiwarki.

## Krok 5: Wnioskowanie i budowa fraz kluczowych
Ostatnim etapem będzie nauka pobierania informacji z utworzonej bazy grafowej. Na podstawie zgromadzonych danych i ich wzajemnych powiązań przeprowadzimy ćwiczenie polegające na zbudowaniu nowej, precyzyjnej frazy kluczowej. To pokaże, jak ogromna jest różnica w jakości i głębokości tematów w porównaniu do prostego grafu, od którego zaczęliśmy. 