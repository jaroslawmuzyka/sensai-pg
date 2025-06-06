# Tworzenie własnego promptu – praktyka

Ta lekcja krok po kroku przedstawia proces tworzenia zaawansowanego promptu, którego celem jest generowanie grafów wiedzy. Wykorzystamy metody omówione wcześniej, w tym automatyczny prompt engineering, aby stworzyć narzędzie do syntezy informacji z tekstów w postaci encji i relacji między nimi. Zrozumienie tego procesu jest kluczowe, gdyż generowanie grafów wiedzy stanowi podstawę wielu zaawansowanych zadań związanych z przetwarzaniem i generowaniem tekstów.

Pamiętaj, że istnieje wiele sposobów na tworzenie, ewaluację i testowanie promptów. Przedstawiony tu proces i checklista to jeden z możliwych modeli pracy, który możesz dostosować do własnych potrzeb. Choć wysiłek włożony w stworzenie solidnego promptu może być znaczny, jest to inwestycja, która zapewni jego nieprzerwane i bezbłędne działanie w Twoich zautomatyzowanych procesach.

---

## Cel: Prompt do generowania grafów wiedzy

Naszym celem jest stworzenie promptu, który z grupy tekstów (np. pobranych z wyników wyszukiwania) wyekstrahuje kluczowe informacje i przedstawi je w formie grafu wiedzy. Graf ten będzie składał się z encji (ważnych pojęć, obiektów) oraz relacji między tymi encjami.

---

## Ustrukturyzowane podejście do projektowania promptu

Nawet korzystając z automatyzacji, praca nad promptem wymaga od nas zdefiniowania pewnych ram i warunków brzegowych. Poniżej znajduje się checklista kroków, które warto wykonać (opisana również w notatkach na GitHub do tej lekcji):

1. **Ustalenie fundamentów:** Zdefiniuj cel promptu. Odpowiedz na pytania: Dlaczego ten prompt jest potrzebny? Dla kogo jest przeznaczony? Co dokładnie chcę dzięki niemu osiągnąć?
2. **Zmapowanie danych wejściowych i ograniczeń:** Określ, jakie dane będziesz w stanie dostarczyć do promptu. W naszym przypadku będą to teksty z wyników wyszukiwania dla określonego słowa kluczowego.
3. **Definicja kluczowych pojęć:** Aby uniknąć dowolnej interpretacji przez model, precyzyjnie zdefiniuj w prompcie kluczowe terminy. Dla grafu wiedzy będą to:
   - **Encja:** Czym jest encja w kontekście zadania.
   - **Relacja:** Jak rozumiana jest relacja między encjami.
   - **Siła relacji:** Jeśli dotyczy, jak określać siłę tej relacji.
   Można też poprosić model o wstępne definicje, a następnie je zmodyfikować.
4. **Podział zadania na mniejsze kroki:** Zastanów się, jakie etapy powinien przejść model, aby zrealizować zadanie od początku do końca.
5. **Projektowanie struktury promptu:** Chociaż przy automatycznym generowaniu ten krok może być częściowo pominięty, warto pamiętać o stosowaniu czytelnej struktury (np. Markdown) i oddzielaniu istotnych sekcji znacznikami.
6. **Dodawanie przykładów (dobrych i złych):** Przykłady znacząco pomagają modelowi zrozumieć oczekiwania.

---

## Implementacja z wykorzystaniem automatycznego prompt engineeringu

Po przejściu powyższych kroków i przygotowaniu skróconego opisu działania promptu, możemy wykorzystać notatnik do automatycznego prompt engineeringu (omawiany w poprzednich lekcjach).

- **Przygotowanie opisu zadania:** Na podstawie odpowiedzi na pytania z checklisty, stwórz szczegółowy opis tego, jak prompt ma działać. Ten opis posłuży jako wejście do procesu automatycznego generowania.
- **Konfiguracja notatnika Google Colab:**
  - Zaimportuj swój klucz API OpenAI.
  - Sprawdź i ewentualnie dostosuj prompty systemowe (meta-prompty) odpowiedzialne za generowanie kandydatów na prompty oraz za ich ranking.
  - **Kluczowy element: Dane testowe.** Dla zadania generowania grafu wiedzy, jako dane testowe należy dostarczyć teksty z wyników wyszukiwania dla różnych słów kluczowych. Załaduj przygotowany plik z tymi danymi.
- **Uruchomienie procesu:** Skrypt w notatniku wygeneruje kilku kandydatów na prompty, a następnie przetestuje ich działanie na dostarczonych danych testowych, dokonując rankingu. Proces ten może chwilę potrwać i wiązać się z kosztami API.
- **Analiza wyników:** Otrzymasz listę promptów wraz z ich oceną (np. punktacją ELO). Prompt, który uzyskał najwięcej punktów, jest teoretycznie najlepszy, ale zawsze wymaga dalszego, manualnego testowania. W przykładzie z lekcji różnice między czołowymi promptami mogą nie być duże.

Gotowy, przetestowany i poprawiony prompt do generowania grafów wiedzy zostanie udostępniony w materiałach do kursu. Może on się nieznacznie różnić od wyników automatycznego generowania, ponieważ był poddawany dalszym iteracjom.

---

## Alternatywna metoda: Wykorzystanie Claude Workbench

Przygotowany opis zadania można również wykorzystać w narzędziach takich jak Claude Workbench do wygenerowania wstępnej wersji promptu.

- Wprowadź szczegółowy opis zadania do generatora promptów w Claude Workbench. Unikaj ogólnych instrukcji, szczególnie gdy celem jest stworzenie promptu do konkretnego, powtarzalnego zadania.
- Po wygenerowaniu promptu przez Claude, warto przeprowadzić weryfikację:
  - Skopiuj wygenerowany prompt.
  - Wklej go do modelu językowego, który docelowo będzie go używał.
  - Poproś model o dokładne wyjaśnienie, krok po kroku, jak rozumie podane instrukcje. Porównaj to ze swoimi intencjami.

Ta metoda nie umożliwia tak prostego testowania na realnych danych jak podejście z notatnikiem Colab.

---

## Kolejne kroki: Testowanie, testowanie, testowanie!

Niezależnie od metody generowania, uzyskany prompt to dopiero początek.

- Przetestuj prompt w praktycznych zastosowaniach – np. integrując go z Make, N8N, czy pisząc dedykowany skrypt w Pythonie.
- Analizuj wyniki pod kątem błędów i obszarów do poprawy.
- Iteruj, wprowadzaj poprawki i testuj ponownie, aż osiągniesz satysfakcjonującą jakość i niezawodność.

W kolejnych tygodniach kursu zostaniesz wyposażony w dalszą wiedzę dotyczącą testowania i wdrażania promptów. 