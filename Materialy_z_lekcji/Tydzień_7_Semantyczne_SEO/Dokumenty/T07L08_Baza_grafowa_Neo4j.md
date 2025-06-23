# Baza grafowa Neo4j

**Streszczenie:**
Ta lekcja wprowadza rozwiązanie problemu skali, który pojawił się po wygenerowaniu setek grafów wiedzy. Aby efektywnie zarządzać dużą ilością połączonych danych, korzystamy z Neo4j – jednej z najpopularniejszych grafowych baz danych na świecie.

---

## Czym jest Neo4j i dlaczego go używamy?
Neo4j to lider na rynku baz grafowych, używany przez firmy takie jak Adobe, BMW czy Cisco. Pozwala przechowywać, zarządzać i analizować dane w formie grafów – dokładnie tak, jak modelujemy połączenia między encjami w tym kursie. Oferuje zaawansowane opcje eksploracji, wizualizacji i zadawania zapytań do grafu (np. „pokaż najsilniejsze powiązania”), co jest niemożliwe w prostym pliku tekstowym czy czacie.

---

## Rejestracja i tworzenie darmowej instancji (AuraDB)
Na potrzeby kursu korzystamy z darmowej, chmurowej wersji Neo4j – AuraDB. Proces konfiguracji jest prosty i nie wymaga instalacji na własnym komputerze.

**Krok 1: Rejestracja**
- Wejdź na [neo4j.com](https://neo4j.com) i załóż darmowe konto.

**Krok 2: Tworzenie instancji**
- Po zalogowaniu do panelu Aura, kliknij „Create instance”. Wybierz darmowy pakiet (Free).

**Krok 3: Zapisanie hasła**
- Podczas tworzenia instancji zostanie wygenerowane hasło dostępowe. Skopiuj je i zapisz w bezpiecznym miejscu – nie będzie ponownie wyświetlone.

**Krok 4: Oczekiwanie**
- Poczekaj, aż instancja bazy danych zostanie utworzona i uruchomiona.

---

## Pierwsze spojrzenie na interfejs Aury
Po utworzeniu instancji zobaczysz panel zarządzania. Baza jest na razie pusta (0 węzłów, 0 relacji). Kluczowe obszary interfejsu:
- **Query:** miejsce do pisania zapytań do bazy.
- **Explore:** narzędzie do interaktywnej wizualizacji grafów.
- **Connect:** dane do połączenia z bazą z poziomu kodu (np. w Pythonie).

---

## Podsumowanie i następne kroki
Pomyślnie utworzyliśmy i skonfigurowaliśmy własną, darmową instancję profesjonalnej bazy grafowej Neo4j. Mamy gotowe środowisko do pracy z danymi. W kolejnej lekcji zajmiemy się załadowaniem (indeksacją) 166 grafów wiedzy z pliku JSON do bazy.

---

## Ważne linki
- Link do lekcji na platformie: [SensAI Academy](https://learn.sensai.academy/next/public/lesson/340)
- Strona Neo4j: [https://neo4j.com](https://neo4j.com) 