# Modele AI

![image](image%2011.png)

![image](image%2012.png)

![image](image%2013.png)

---

## Czy najinteligentniejszy model jest najlepszy?

Wybierając model musimy przede wszystkim wziąć pod uwagę w jakim środowisku go używamy - jeśli potrzebujemy skryptu bez zależności od większej liczby elementów systemy to spokojnie możemy go napisać z modelem w czacie, ale jeśli chcemy wykorzystać model jako agenta (np. w Cursorze) to jego skuteczność korzystania z narzędzi jest moim zdaniem istotniejsza niż jego wyniki w testach programistycznych.

![image](image%2014.png)

<details>
<summary>Więcej informacji</summary>

[https://artificialanalysis.ai](https://artificialanalysis.ai)

</details>

---

## Testy programistyczne dla modeli

<details>
<summary>HumanEval</summary>

*   **Najstarszy i najczęściej używany** benchmark do oceny generowania kodu
*   Składa się z **164 prostych zadań programistycznych** w Pythonie
*   Zadania to głównie **pojedyncze funkcje** z jasno określonymi specyfikacjami
*   **Relatywnie łatwy** - dlatego najlepsze modele osiągają tu wyniki 95%+
*   Przykład: "Napisz funkcję, która zwraca n-ty element ciągu Fibonacciego"

</details>

<details>
<summary>SciCode</summary>

*   Koncentruje się na **programowaniu naukowym i badawczym**
*   Zadania wymagają **głębokiej wiedzy domenowej** z matematyki, fizyki, chemii itp.
*   Często wymaga użycia **specjalistycznych bibliotek** (NumPy, SciPy)
*   **Trudniejszy niż HumanEval** - testuje zdolność modelu do rozumienia i stosowania złożonych algorytmów
*   Przykład: "Zaimplementuj metodę Monte Carlo do oszacowania wartości liczby Pi"

</details>

<details>
<summary>LiveCodeBench</summary>

*   **Najbardziej realistyczny i wymagający** benchmark
*   Zadania pochodzą z **prawdziwych konkursów programistycznych** (LeetCode, Codeforces)
*   Ocena opiera się na **przechodzeniu ukrytych testów**, tak jak w prawdziwym konkursie
*   Testuje **zdolność do rozwiązywania problemów**, a nie tylko generowania kodu
*   **Najtrudniejszy** - nawet najlepsze modele mają tu problemy
*   Przykład: "Znajdź najkrótszą ścieżkę w grafie z uwzględnieniem wag krawędzi"

</details>
