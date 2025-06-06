# Praktyczne zastosowanie modeli rerankingowych w procesie RAG

Ta lekcja demonstruje w praktyce, jak modele rerankingowe wpływają na wyniki wyszukiwania semantycznego w porównaniu do samych modeli embeddingowych. Zrozumiesz ich rolę w procesie Retrieval Augmented Generation (RAG) oraz w kontekście działania wyszukiwarek takich jak Google. Ćwiczenie pokaże, jak modele rerankingowe zwiększają dokładność, uszeregowując wstępnie wyselekcjonowaną grupę dokumentów.

## Wprowadzenie do modeli rerankingowych

Modele rerankingowe odgrywają kluczową rolę zarówno w zaawansowanych procesach RAG, jak i w mechanizmach rankingowych wyszukiwarki Google. Ich głównym zadaniem jest precyzyjne uszeregowanie wyników, które zostały wstępnie wybrane przez szybsze, ale mniej dokładne metody, takie jak wyszukiwanie oparte na embeddingach. W procesie RAG, embeddingi pomagają wybrać grupę najbardziej zbliżonych dokumentów, a model rerankingowy tworzy z nich ostateczny, bardziej trafny ranking.

## Cel ćwiczenia i wykorzystywane narzędzia

Celem tego ćwiczenia jest praktyczne zademonstrowanie, jak modele rerankingowe mogą zmienić i poprawić wyniki wyszukiwania w stosunku do wyników uzyskanych wyłącznie za pomocą modeli embeddingowych.

**Wykorzystywane narzędzia:**

**Model rerankingowy:** Wielojęzyczny model od Giny. Działa poprzez przesłanie zapytania oraz treści dokumentów, a następnie zwraca `read advance score` dla każdego dokumentu, szeregując je.

**Model embeddingowy:** Model od Google, konkretnie `text embedding 0307`.

**Inne wspomniane narzędzia i modele:**

**Dostawcy modeli rerankingowych:** Cohere, ColBERT (dystrybucja łącząca embeddingi z rerankingiem).

**Crawlery:** Jina Reader (użyty w ćwiczeniu), Crow4AI, FireCrawl.

**Platforma:** Google Colab.

*Uwaga:* Google oficjalnie nie udostępnia modeli rerankingowych, ale istnieje możliwość rerankingu w oparciu o modele Gemini (informacje będą podlinkowane w GitHubie).

## Przebieg ćwiczenia w Google Colab krok po kroku

Proces realizowany w notebooku Google Colab będzie przebiegał następująco:

1. **Pobranie treści z adresów URL:**
   - **Dane wejściowe:** Sitemap.xml wskazanej strony (w przykładzie: sitemapa seomarketing.com, plik `sitemaps_2.xml`, zawierająca 253 adresy URL).
   - **Proces:** Skrypt pobiera listę URL-i z sitemapy, a następnie za pomocą Jina Reader pobiera treść oraz znaczniki `<title>` dla każdego adresu. Pobranie danych może zająć kilka minut (w przykładzie ok. 7 minut).
   - **Wskazówka dotycząca embeddingów:** W ćwiczeniu do generowania embeddingów i porównań wykorzystywane są wyłącznie znaczniki `<title>` stron. Jest to często wystarczające dla operacji na embeddingach dla stron internetowych. Rzadziej wykorzystuje się cały content, ponieważ nawet po oczyszczeniu jest on zazwyczaj zbyt długi, co prowadzi do uśrednienia wektora przez model embeddingowy i zmniejszenia jego dokładności. Alternatywy to łączenie `<title>` i `<description>` lub wykorzystanie podsumowań treści generowanych przez model językowy. Chunkowanie (dzielenie treści na mniejsze kawałki) również stosuje się dla poprawy skuteczności dopasowania embeddingowego.
   - **Ostrzeżenie:** Nie podawaj zbyt dużej sitemapy, aby uniknąć potencjalnie wysokich kosztów i długiego czasu przetwarzania. Skrypty nie są zoptymalizowane pod kątem bardzo dużych zbiorów danych.

2. **Generowanie embeddingów:**
   - **Proces:** Pobrane tytuły stron są zamieniane na embeddingi za pomocą modelu Google `text embedding 0307`.
   - **Parametr:** Używany jest `task_type='SEMANTIC_SIMILARITY'`, odpowiedni dla celu porównywania podobieństwa semantycznego.
   - **Przechowywanie embeddingów:** W tym ćwiczeniu embeddingi są przetwarzane w pamięci maszyny, bez zapisywania do bazy wektorowej, ponieważ jest to operacja jednorazowa. Baza wektorowa jest przydatna przy budowie procesów RAG działających w trybie ciągłym lub gdy potrzebny jest wielokrotny dostęp do informacji.
   - **Wynik:** Powstaje plik zawierający URL, tytuł, wygenerowany embedding oraz status operacji.

3. **Wyszukiwanie najbliższych sąsiadów na podstawie embeddingów:**
   - **Proces:** Obliczane jest podobieństwo kosinusowe pomiędzy embeddingami tytułów wszystkich URL-i. Dla każdego URL-a wyznaczanych jest 10 jego najbliższych sąsiadów (najbardziej podobnych semantycznie tytułów).
   - **Wynik:** Lista sąsiadów wraz z ich wynikami podobieństwa (np. 0.87, 0.83). Zauważalna jest często mała rozpiętość wyników podobieństwa (np. między 0.89 a 0.86 dla różnych artykułów).

4. **Reranking wybranych sąsiadów:**
   - **Proces:** Dla każdego URL-a, 10 najbliższych sąsiadów (wybranych na podstawie embeddingów) jest przesyłanych do modelu rerankingowego od Giny w celu ich ponownego uszeregowania. Model rerankingowy ma dostęp do większego kontekstu i jest bardziej dokładny.
   - **Czas:** Ten etap może zająć kilka minut (w przykładzie ok. 5 minut).

## Analiza i porównanie wyników rerankingu

Po zakończeniu procesu rerankingu, porównujemy wyniki uzyskane z samego embeddingu z wynikami po zastosowaniu modelu rerankingowego.

**Kluczowe obserwacje:**

**Rozpiętość ocen:** Model rerankingowy zazwyczaj wykazuje znacznie większą rozpiętość ocen (np. od 0.36 do 0.71) w porównaniu do modelu embeddingowego (np. od 0.84 do 0.88). Oznacza to, że model rerankingowy lepiej różnicuje relewantność dokumentów.

**Odchylenie standardowe:** Odchylenie standardowe ocen jest większe dla modelu rerankingowego (np. 0.1) niż dla embeddingowego (np. 0.013), co potwierdza jego większą precyzję w ocenie.

**Zmiany w rankingu:** Chociaż dla niektórych zapytań (tytułów) wyniki mogą być podobne, dla wielu innych kolejność sąsiadów znacząco się zmienia po rerankingu, ukazując bardziej trafne dopasowania. Różnice te są szczególnie widoczne przy dużych domenach z różnorodnymi tematami.

**Praktyczne zastosowanie:** W przypadku budowy np. struktury linkowania wewnętrznego dla dużego serwisu z tysiącami podobnych do siebie podstron, można najpierw wybrać np. 100 najbardziej podobnych artykułów za pomocą embeddingów, a następnie za pomocą modelu rerankingowego zredukować tę listę do 10 najbardziej relevantnych.

## Podsumowanie i zachęta do eksploracji

Lekcja pokazała, że modele rerankingowe są cennym uzupełnieniem modeli embeddingowych, dostarczając bardziej precyzyjnego uszeregowania wyników. Chociaż embeddingi są skuteczne w szybkim filtrowaniu dużej liczby dokumentów, reranking pozwala na dokładniejszą ocenę i wybór najbardziej relevantnych pozycji.

Zachęcam do własnej eksploracji tego procesu:

**Testowanie na własnej domenie:** Przetestuj skrypt na własnej domenie (pamiętając o jej rozmiarze).

**Inne modele rerankingowe:** Zapoznaj się z innymi modelami rerankingowymi (np. od Cohere, ColBERT, czy możliwościami Gemini), które zostaną podlinkowane na GitHubie.

**Eksperymenty z embeddingami:** Eksperymentuj z różnymi danymi wejściowymi do embeddingu (np. łączenie tytułu i opisu, podsumowania treści, chunkowanie).

W kolejnych lekcjach będziemy dalej składać poszczególne elementy procesu RAG, omawiając działanie AI Overviews i AI Mode w Google. 