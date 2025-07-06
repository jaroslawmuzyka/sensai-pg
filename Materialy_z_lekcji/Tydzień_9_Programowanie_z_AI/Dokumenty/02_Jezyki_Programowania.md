# Języki Programowania

Rozmawiając z modelami językowymi możemy pisać aplikacje nie tworząc samemu ani linijki kodu. Dlatego bardziej niż składnia języka powinny nas interesować jego inne cechy, do czego służy, jakie ma mocne strony i jakie są jego ograniczenia. To po prostu wybór odpowiedniego narzędzia do zadania.

W praktyce wystarczy nam Python do przetwarzania danych i jako język serwera, Javascript jako język obsługujący interakcje usera ze stroną napisaną w HTML/CSS.

![image](image%202.png)

<details>
<summary>Więcej o językach programowania</summary>

[https://benjdd.com/languages/](https://benjdd.com/languages/)

</details>

---

## 🐘 SQL

o tym mówił już Damian, w module o Supabase.

<details>
<summary>info o SQL</summary>

[ info o SQL]

</details>

Alternatywą jest NoSQL stosowany np. w Firebase

---

## 🐍 Python

Jest to najpopularniejszy język programowania. Na GitHub jeśli chodzi o projekty Open Source, wyprzedził w 2024 roku Javascript.

Nazwany na cześć grupy Monty Python ponad 30 lat temu.

Jest to język wysokopoziomowy (czyli łatwy dla człowieka, nie dla komputera), napisany w C.

![image](image%203.png)

Wszechstronny, mnogość zastosowań w AI

**Mocne strony:**

*   prosta składnia
*   Mnogość bibliotek do przetwarzania i analizy danych (pandas, BeautifulSoup) i sdk (google, supabase), Crawl4AI
*   Mało "ceremonii" w kodzie

<details>
<summary>Alternatywa to Node.js ALE:</summary>

### **Pełny przykład Node.js - to samo zadanie co Python:**

```javascript
// Najpierw instalacja pakietów:
// npm install csv-parser exceljs

const fs = require('fs');
const csv = require('csv-parser');
const ExcelJS = require('exceljs');

// Funkcja główna (bo Node.js wymaga async/await dla Excel)
async function analizujKeywords() {
  const results = [];

  // 1. Wczytanie CSV
  await new Promise((resolve, reject) => {
    fs.createReadStream('keywords.csv')
      .pipe(csv())
      .on('data', (data) => {
        // Konwersja pozycji na liczbę (csv-parser zwraca stringi)
        data.pozycja = parseInt(data.pozycja);
        results.push(data);
      })
      .on('end', resolve)
      .on('error', reject);
  });

  // 2. Filtrowanie top 10
  const top10 = results.filter(row => row.pozycja <= 10);

  // 3. Zapis do Excel
  const workbook = new ExcelJS.Workbook();
  const worksheet = workbook.addWorksheet('Top 10');

  // Dodanie nagłówków (zakładamy że CSV ma kolumny: keyword, pozycja, klikniecia)
  worksheet.columns = [
    { header: 'Keyword', key: 'keyword', width: 30 },
    { header: 'Pozycja', key: 'pozycja', width: 10 },
    { header: 'Kliknięcia', key: 'klikniecia', width: 15 }
  ];

  // Dodanie danych
  top10.forEach(row => {
    worksheet.addRow(row);
  });

  // Zapisanie pliku
  await workbook.xlsx.writeFile('raport.xlsx');

  console.log('Gotowe! Zapisano do raport.xlsx');
}

// Uruchomienie z obsługą błędów
analizujKeywords().catch(error => {
  console.error('Błąd:', error);
});
```

#### **Porównanie kodu:**

**Python (3 linie):**

```python
dane = pd.read_csv("keywords.csv")
top10 = dane[dane['pozycja'] <= 10]
top10.to_excel("raport.xlsx")
```

**Node.js (40+ linii):**

*   Instalacja 2 pakietów
*   Import 3 modułów
*   Async/await wrapper
*   Promise dla strumienia
*   Ręczna konwersja typów
*   Ręczne definiowanie kolumn
*   Obsługa błędów
*   Callback hell (częściowo)

#### **Dodatkowe komplikacje w Node.js:**

1.  **Typy danych:**

```javascript
data.pozycja = parseInt(data.pozycja);
// Python - pandas robi to automatycznie
```

2.  **Struktura danych:**

```javascript
// Node.js - musisz ręcznie definiować kolumny Excel
worksheet.columns = [
  { header: 'Keyword', key: 'keyword', width: 30 },
  // ...
];
// Python - pandas zachowuje strukturę automatycznie
```

3.  **Obsługa asynchroniczności:**

```javascript
// Node.js - wszystko musi być w async/await lub callbackach
async function analizujKeywords() {
  await new Promise((resolve, reject) => {
    // ...
  });
}
// Python - synchroniczny, prosty przepływ
```

#### **Realny czas developmentu:**

| Zadanie | Python | Node.js |
| --- | --- | --- |
| Napisanie kodu | 30 sekund | 5-10 minut |
| Debugowanie | Rzadko potrzebne | Często (typy, async) |
| Instalacja bibliotek | pip install pandas openpyxl | npm install csv-parser exceljs |
| Dokumentacja | Prosta, spójna | Różna dla każdej biblioteki |

To pokazuje dlaczego Python dominuje w analizie danych - robi więcej przy mniejszym nakładzie kodu i czasu.

</details>

---

## 📒 Javascript/ Typescript

Kluczowe dla aplikacji webowych. Pisze się w nim zarówno obsługę kliknięć w przyciski,

---

## 🏠 Html + CSS

Choć formalnie nie są to języki programowania, to są niezbędne do tworzenia interfejsów użytkownika.

HTML odpowiada za strukturę strony, a CSS za jej wygląd.

<details>
<summary>HTML vs HTML + CSS</summary>

HTML HTML + CSS

![image](image%204.png)

</details>
