### Notatka:

Ta lekcja łączy dotychczasowe koncepcje, aby wyjaśnić, jak Google modeluje tematy i buduje mapy tematyczne. Zrozumiesz fundamentalną różnicę między grafem wiedzy a grafem informacji – dwoma kluczowymi narzędziami, których Google używa do porządkowania i rozumienia treści w internecie.

---

### Dwa typy grafów

Aby efektywnie zarządzać ogromem danych w internecie, Google stosuje podział na dwa rodzaje grafów. Utrzymywanie jednej, gigantycznej struktury dla całej sieci byłoby niewydajne. Dlatego wiedza jest organizowana na dwóch poziomach:

**Graf Wiedzy (Knowledge Graph):** Jego celem jest przedstawienie szerokiego obrazu tematu ("big picture", "helicopter view"). Łączy ze sobą główne pojęcia (encje) i pokazuje ich wzajemne relacje, np. jak "samochód" łączy się z "motocyklem" w ramach szerszej dziedziny motoryzacji. Jest to graf reprezentujący **szerokość** wiedzy. Używamy go do budowania struktury serwisu i map tematycznych.

**Graf Informacji (Information Graph):** Skupia się na szczegółach dotyczących jednego, konkretnego pojęcia. Zawiera listę suchych faktów i danych, np. "samochód ma cztery koła", "samochód ma silnik". Reprezentuje **głębokość** wiedzy. Jest idealną podstawą do tworzenia wyczerpujących i bogatych w fakty treści.

---

### Anatomia grafu wiedzy

Graf wiedzy, który będziemy tworzyć, składa się z trzech podstawowych elementów, które pozwalają na zaawansowane modelowanie tematu i budowanie kontekstowego linkowania wewnętrznego.

- **Encje (Węzły / Nodes):** Są to główne pojęcia lub obiekty w analizowanym temacie, np. "samochód", "silnik", "napęd hybrydowy". W SEO semantycznym myślimy w kategoriach encji, a nie słów kluczowych.
- **Relacje (Krawędzie / Edges):** To połączenia, które określają, w jaki sposób encje są ze sobą powiązane. Używamy standardowego słownika relacji (np. `is a` – jest rodzajem, `has part` – ma część), aby utrzymać spójność danych.
- **Etykiety (Właściwości / Labels):** To dodatkowe informacje opisujące relację. W naszym modelu wprowadzamy dwie etykiety: opis słowny relacji (np. "oba są pojazdami kołowymi, ale różnią się liczbą kół") oraz siłę powiązania (jak blisko powiązane są ze sobą dwie encje).

---

### Ćwiczenie: Tworzenie prostego grafu wiedzy

Korzystając z przygotowanego promptu i treści (np. z artykułu na Wikipedii o samochodach), tworzymy pierwszy graf wiedzy. Wprowadzamy do modelu AI treść oraz określamy centralną encję analizy (np. "samochód").

Wynikiem jest struktura w formacie JSON, która pokazuje powiązania między encjami. Na przykład:

- Encja źródłowa: `samochód` | Relacja: `is a` | Encja docelowa: `kołowy pojazd silnikowy`
- Encja źródłowa: `samochód` | Relacja: `has part` | Encja docelowa: `silnik`

Nawet z małej ilości tekstu uzyskujemy mapę kluczowych połączeń, która stanowi szkielet tematu.

---

### Anatomia grafu informacji

Graf informacji ma inną, prostszą strukturę, opartą na tzw. trójnikach semantycznych: **Podmiot – Orzeczenie – Dopełnienie (Subject – Predicate – Object)**. Jego celem jest ekstrakcja jak największej liczby konkretnych faktów z tekstu.

Każdy fakt jest rozbijany na ten trójkowy format, np.: "jabłko (podmiot) jest (orzeczenie) owocem (dopełnienie)". Na tej zasadzie zbudowana jest cała Wikidata, czyli bazodanowy odpowiednik Wikipedii.

---

### Ćwiczenie: Tworzenie grafu informacji

Używając drugiego promptu, przeprowadzamy ekstrakcję informacji z tego samego tekstu. W tym przypadku nie definiujemy centralnej encji, ponieważ celem jest wyciągnięcie wszystkich dostępnych faktów.

Wynikiem jest długa lista trójników w formacie JSON. Na przykład:

- Podmiot: `silnik spalinowy` | Orzeczenie: `wykorzystuje` | Dopełnienie: `benzynę lub olej napędowy`
- Podmiot: `emisja CO2 na osobę na kilometr dla samochodu` | Orzeczenie: `wynosi` | Dopełnienie: `271 gramów`

Taka lista jest bezcenna przy tworzeniu szczegółowego i wyczerpującego contentu.

---

### Podsumowanie i praktyczne zastosowanie

Zapamiętaj kluczową zasadę: **struktura Twojej strony internetowej to graf wiedzy, a jej treść to graf informacji**. Google analizuje Twoją witrynę w obu tych wymiarach, porównując ją do swojego globalnego rozumienia tematu.

Im bogatszy i dokładniejszy graf informacji dostarczysz w swoich treściach, tym Twoja strona będzie bardziej atrakcyjna dla mechanizmów AI Search i AI Overview. Jeśli chcesz zgłębić temat, zapoznaj się z koncepcją **Microsoft Graph RAG**, która potwierdza opisane tu podejście.

---

#### Prompt do stworzenia grafu wiedzy:

Pełny, aktualny prompt do generowania grafu wiedzy znajdziesz w katalogu promptów:

[Prompty/Knowledge_Graph_Generator.md](../../../Prompty/Knowledge_Graph_Generator.md)

---

#### Prompt do stworzenia grafu informacji (trójki semantyczne):

Pełny, aktualny prompt do generowania grafu informacji znajdziesz w katalogu promptów:

[Prompty/Information_Graph_Generator.md](../../../Prompty/Information_Graph_Generator.md)

--- 