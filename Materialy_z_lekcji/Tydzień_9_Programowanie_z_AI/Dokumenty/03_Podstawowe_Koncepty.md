# Podstawowe Koncepty w Kodzie

Ucząc się jednego języka programowania dużo łatwiej nauczyć nam się kolejnych. Podobnie jak poznamy język włoski łatwiej nam nauczyć się hiszpańskiego. Jest tak dlatego, że języki te operują na podobnych konceptach, mają zbliżoną składnię. Tu użyjemy Pythona, ale te same koncepty stosowane są w innych językach.

---

<details>
<summary>1. Zmienne - Pojemniki na dane</summary>

Zmienna to jak komórka w Excelu - miejsce gdzie przechowujesz informację.

```python
# Zmienne tekstowe (string)
keyword = "buty nike"
url = "https://example.com/buty"

# Zmienne liczbowe
pozycja = 11
liczba_wyswietlen = 15420
ctr = 2.5  # procent

# Zmienne logiczne (True/False)
czy_w_top10 = False
czy_zindeksowana = True

# Używanie zmiennych
print(f"Keyword '{keyword}' jest na pozycji {pozycja}")
# Wynik: Keyword 'buty nike' jest na pozycji 11
```

**Analogia SEO**: Zmienna to jak parametr w Google Analytics - przechowuje konkretną wartość którą możesz później wykorzystać.

</details>

---

<details>
<summary>2. Funkcje - Gotowe przepisy</summary>

Funkcja to zestaw instrukcji które możesz używać wielokrotnie. Jak makro w Excelu!

```python
# Definicja funkcji
def sprawdz_pozycje(keyword, pozycja):
    """Sprawdza czy keyword jest w TOP10"""
    if pozycja <= 10:
        return f"✅ '{keyword}' jest w TOP10 (poz. {pozycja})"
    else:
        return f"❌ '{keyword}' poza TOP10 (poz. {pozycja})"

# Użycie funkcji
wynik1 = sprawdz_pozycje("buty nike", 5)
wynik2 = sprawdz_pozycje("adidas sneakers", 15)

print(wynik1)  # ✅ 'buty nike' jest w TOP10 (poz. 5)
print(wynik2)  # ❌ 'adidas sneakers' poza TOP10 (poz. 15)
```

**Praktyczny przykład SEO**:

```python
def oblicz_potencjal_ruchu(impressions, pozycja_obecna, pozycja_docelowa=3):
    """Oblicza potencjalny wzrost ruchu po awansie"""
    ctr_obecny = get_ctr_dla_pozycji(pozycja_obecna)
    ctr_docelowy = get_ctr_dla_pozycji(pozycja_docelowa)

    ruch_obecny = impressions * ctr_obecny / 100
    ruch_potencjalny = impressions * ctr_docelowy / 100

    wzrost = ruch_potencjalny - ruch_obecny
    return round(wzrost)

# Użycie
potencjal = oblicz_potencjal_ruchu(10000, 11, 3)
print(f"Możesz zyskać {potencjal} dodatkowych kliknięć miesięcznie!")
```

</details>

---

<details>
<summary>3. Listy - Kolekcje danych</summary>

Lista to jak kolumna w Excelu - przechowuje wiele wartości.

```python
# Lista keywords
keywords = ["buty nike", "adidas sneakers", "puma buty", "reebok classic"]

# Dodawanie do listy
keywords.append("new balance")

# Dostęp do elementów (numeracja od 0!)
pierwszy_keyword = keywords[0]  # "buty nike"
ostatni_keyword = keywords[-1]  # "new balance"

# Przetwarzanie całej listy
for keyword in keywords:
    print(f"Analizuję: {keyword}")
```

**Słowniki - dane z etykietami**:

```python
# Słownik to jak wiersz w Excelu z nazwanymi kolumnami
dane_keyword = {
    "keyword": "buty nike",
    "pozycja": 11,
    "impressions": 15420,
    "clicks": 234,
    "url": "https://example.com/buty-nike"
}

# Dostęp do danych
print(dane_keyword["keyword"])  # "buty nike"
print(dane_keyword["pozycja"])  # 11

# Lista słowników (jak tabela w Excelu)
wyniki_seo = [
    {"keyword": "buty nike", "pozycja": 11, "impressions": 15420},
    {"keyword": "adidas sneakers", "pozycja": 5, "impressions": 8900},
    {"keyword": "puma buty", "pozycja": 23, "impressions": 3200}
]
```

</details>

---

<details>
<summary>4. Warunki - Podejmowanie decyzji</summary>

Instrukcje warunkowe pozwalają programowi reagować różnie w zależności od sytuacji.

```python
pozycja = 11

# Prosty warunek
if pozycja <= 10:
    print("Świetnie! Jesteś w TOP10")
else:
    print("Trzeba popracować nad pozycją")

# Złożone warunki
if pozycja <= 3:
    status = "🥇 TOP3 - Excellent!"
elif pozycja <= 10:
    status = "✅ TOP10 - Dobra robota"
elif pozycja <= 20:
    status = "📈 TOP20 - Jest potencjał"
else:
    status = "💪 Wymaga pracy"

# Operatory logiczne
if pozycja > 10 and impressions > 1000:
    print("Duży potencjał - warto zoptymalizować!")

if ctr < 1 or pozycja > 50:
    print("Pilna interwencja potrzebna!")
```

</details>

---

<details>
<summary>5. Pętle - Automatyzacja powtórzeń</summary>

Pętle pozwalają wykonać te same operacje dla wielu elementów.

```python
# Pętla for - gdy znasz ilość powtórzeń
keywords = ["buty nike", "adidas sneakers", "puma buty"]

for keyword in keywords:
    print(f"Sprawdzam pozycję dla: {keyword}")
    # Tu normalnie byłoby wywołanie API

# Pętla while - gdy nie wiesz ile razy
strona = 1
while strona <= 10:
    print(f"Pobieram wyniki ze strony {strona}")
    strona = strona + 1
    # Przerwij jeśli nie ma więcej wyników
    if brak_wynikow:
        break
```

**Praktyczny przykład - analiza wielu URL**:

```python
urls_do_sprawdzenia = [
    "https://example.com/kategoria-1",
    "https://example.com/kategoria-2",
    "https://example.com/produkt-1"
]

for url in urls_do_sprawdzenia:
    status_code = sprawdz_status(url)  # funkcja sprawdzająca
    if status_code == 404:
        print(f"❌ BŁĄD 404: {url}")
    elif status_code == 200:
        print(f"✅ OK: {url}")
```

</details>

---

<details>
<summary>6. Klasy - Szablony obiektów</summary>

Klasa to jak formularz - definiuje strukturę danych i co można z nimi zrobić.

```python
class AnalizaKeyword:
    def __init__(self, keyword, url):
        self.keyword = keyword
        self.url = url
        self.pozycja = None
        self.impressions = 0
        self.clicks = 0

    def oblicz_ctr(self):
        if self.impressions > 0:
            return (self.clicks / self.impressions) * 100
        return 0

    def czy_wymaga_optymalizacji(self):
        return self.pozycja > 10 and self.impressions > 1000

# Użycie klasy
analiza1 = AnalizaKeyword("buty nike", "/buty-nike")
analiza1.pozycja = 15
analiza1.impressions = 5000
analiza1.clicks = 50

print(f"CTR: {analiza1.oblicz_ctr():.2f}%")
if analiza1.czy_wymaga_optymalizacji():
    print("🎯 Ten keyword ma duży potencjał!")
```

</details>

---

<details>
<summary>7. Import bibliotek - Korzystanie z gotowych narzędzi</summary>

Biblioteki to gotowe zestawy funkcji które możesz używać.

```python
# Import całej biblioteki
import pandas as pd
import requests

# Import konkretnej funkcji
from datetime import datetime
from collections import Counter

# Przykład użycia
# Pandas - jak Excel w Pythonie
df = pd.read_csv('keywords.csv')
top10 = df[df['pozycja'] <= 10]

# Requests - pobieranie danych z internetu
response = requests.get('https://api.example.com/data')

# Counter - liczenie wystąpień
keywords = ["nike", "adidas", "nike", "puma", "nike"]
licznik = Counter(keywords)
print(licznik)  # {'nike': 3, 'adidas': 1, 'puma': 1}
```

</details>

---

<details>
<summary>8. Obsługa błędów - Gdy coś pójdzie nie tak</summary>

```python
try:
    # Próbuj wykonać kod
    response = requests.get(api_url)
    data = response.json()
except requests.exceptions.Timeout:
    print("❌ API nie odpowiada - timeout")
except Exception as e:
    print(f"❌ Wystąpił błąd: {e}")
else:
    # Wykonaj jeśli nie było błędu
    print("✅ Dane pobrane pomyślnie")
finally:
    # Wykonaj zawsze (np. zamknij połączenie)
    print("Zakończono operację")
```

</details>
