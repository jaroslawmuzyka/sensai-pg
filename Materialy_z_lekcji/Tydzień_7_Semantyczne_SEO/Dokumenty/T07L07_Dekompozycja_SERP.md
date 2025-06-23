# Dekompozycja SERP

**Streszczenie:**
W tej lekcji przechodzimy do kluczowego etapu procesu – dekompozycji. Po zebraniu ponad 500 unikalnych adresów URL, przekształcamy surową treść tych stron w ustrukturyzowaną wiedzę w postaci grafów. To krok naśladujący proces Information Retrieval stosowany przez Google.

---

## Konfiguracja skryptu do budowy grafów
Do automatyzacji zadania wykorzystujemy kolejny skrypt w Google Colab. Kluczowe elementy konfiguracji:
- **Narzędzie do scrapingu (Jina API):** Pobiera treści ze stron. W kursie korzystamy z gotowego rozwiązania, ale w praktyce warto rozważyć własnego scrapera.
- **Model AI (Flash):** Szybki i tani model, idealny do tysięcy operacji. Droższe modele (np. Pro) są nieekonomiczne.
- **Liczba wątków:** Wysoka liczba równoległych wątków (np. 10) dla Jina API i modelu AI.
- **Centralna encja:** W naszym przypadku to „samochód”. Jej podanie jest niezbędne do prawidłowego budowania grafów.

---

## Kluczowa koncepcja: Dwie perspektywy w jednym grafie
Dla każdego analizowanego tematu (np. „akcesoria do samochodu”) skrypt generuje **dwa grafy wiedzy**:
- **Graf zapytania (Query Response):** Opisuje temat z jego własnej perspektywy (np. rodzaje akcesoriów, funkcje).
- **Graf encji (Entity Response):** Pokazuje relację tematu do centralnej encji („samochód posiada akcesoria”).

Dzięki temu uzyskujemy pełny, wielowymiarowy obraz – niezbędny do wizualizacji i budowy spójnej mapy tematycznej.

---

## Wyniki procesu: Od stron do surowych danych
- Proces jest czasochłonny, ale wyniki stanowią fundament mapy tematycznej.
- Skrypt posiada mechanizmy walidacji i ponawiania prób.
- **Liczba wygenerowanych grafów:** 166 (83 grupy fraz x 2 perspektywy).
- **Format danych:** Wszystkie grafy zapisane w jednym dużym pliku JSON – surowa, ustrukturyzowana wiedza na temat samochodów.

---

## Podsumowanie i kolejny krok: Problem skali
Zreplikowaliśmy zaawansowany proces ekstrakcji wiedzy, podobny do tego, który realizuje Google. Mamy 166 precyzyjnie zbudowanych grafów. Pojawia się jednak problem skali – taką ilość danych trudno analizować bez specjalistycznych narzędzi. W kolejnej lekcji poznamy grafową bazę danych Neo4j.

---

## Ważne linki
- Link do lekcji na platformie: [SensAI Academy](https://learn.sensai.academy/next/public/lesson/339) 