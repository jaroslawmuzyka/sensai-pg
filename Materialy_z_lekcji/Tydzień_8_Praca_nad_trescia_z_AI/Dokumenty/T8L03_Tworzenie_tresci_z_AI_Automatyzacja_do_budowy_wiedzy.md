# T8L03: Tworzenie treści z AI - Automatyzacja do budowy wiedzy

## Opis lekcji

Ta lekcja koncentruje się na automatyzacji procesu, który został omówiony w poprzedniej części. Krok po kroku zbudujemy w pełni zautomatyzowany przepływ pracy, wykorzystując Google Sheets jako panel sterowania, Make.com jako silnik automatyzacji oraz Dify do przetwarzania danych i generowania wiedzy.

---

## 📂 Materiały do pobrania

**Plik automatyzacji w Make.com:**  
[Pobierz plik automatyzacji w Make.com](https://learn.sensai.academy/download.php?lfid=66)

**Główny arkusz na którym pracowaliśmy:**  
[Google Sheets - Panel sterowania](https://docs.google.com/spreadsheets/d/1SdeOwR3uw0N3MQa3YFX-l66wZ6SO56AlKorQK600a14/edit?usp=sharing)

**Katalog w którym odkładały się pliki (brief, content, audyt):**  
[Google Drive - Katalog wyników](https://drive.google.com/drive/folders/11_ee_P405ThkaDgQj63QRiWRMRlQzH97?usp=sharing)

**Automatyzacje z repozytorium:**
- **[SEO3.0] Budowa bazy wiedzy.yml** - [główny workflow YAML](../../../Automatyzacje/[SEO3.0]%20Budowa%20bazy%20wiedzy.yml)
- **SEO 3.0 - [1] Budowa wiedzy.blueprint.json** - [szablon Blueprint](../../../Automatyzacje/SEO%203.0%20-%20[1]%20Budowa%20wiedzy.blueprint.json)

---

## Konfiguracja panelu sterowania w Google Sheets

Podstawą naszej automatyzacji jest arkusz kalkulacyjny Google Sheets, który będzie pełnił rolę interfejsu do zarządzania całym procesem. Musi on zawierać odpowiednio przygotowane kolumny.

### Dane wejściowe:

- **Słowo kluczowe:** Główna fraza, na podstawie której będziemy budować wiedzę.
- **Język:** Kolumna z listą rozwijaną (dropdown), aby uniknąć błędów literowych (np. "Polish", "English").
- **Zawartość AI Overview:** Miejsce na wklejenie treści z Google AI Overview.
- **Status:** Kluczowa kolumna z listą rozwijaną, która będzie sterować automatyzacją. Zalecane statusy to: "Wybierz status", "generuj", "gotowe".

### Kolumny na wyniki:
- Frazy z wyników wyszukiwania
- Graf informacji
- Nagłówki konkurencji
- Knowledge Graph

---

## Budowa scenariusza automatyzacji w Make.com

Po przygotowaniu arkusza przechodzimy do serca operacji – budowy scenariusza w Make.com, który połączy wszystkie elementy.

### Krok 1: Uruchomienie procesu (Trigger)

Pierwszym modułem w scenariuszu jest **Google Sheets > Search Rows**. Służy on jako wyzwalacz całego procesu.

**Konfiguracja:**
- **Połączenie:** Wskaż plik i arkusz, który przygotowałeś wcześniej.
- **Filtr:** Ustaw filtr, aby moduł wyszukiwał tylko te wiersze, w których kolumna **Status** ma wartość równą **"generuj"**. Dzięki temu automatyzacja będzie przetwarzać tylko zadania gotowe do uruchomienia.
- **Limit:** Ustaw limit na `1`, aby przy każdym uruchomieniu scenariusza przetwarzany był tylko jeden wiersz. Pozwoli to na łatwiejsze zarządzanie procesem.

### Krok 2: Przygotowanie i wysłanie danych do Dify

Zanim wyślemy dane do Dify, dobrą praktyką jest ich odpowiednie sformatowanie, a następnie skonfigurowanie modułu HTTP.

**Transformacja do JSON:** Dodaj moduł **JSON > Transform to JSON**. Przepuść przez niego dane z Google Sheets (słowo kluczowe, język, treść AI Overview). Zabezpieczy to dane przed błędami, które mogłyby powstać przez specjalne znaki lub formatowanie w arkuszu.

**Wysłanie żądania HTTP:** Dodaj moduł **HTTP > Make a request**.

**Konfiguracja modułu HTTP:**
- **URL:** Wklej adres URL punktu końcowego (endpoint) Twojego przepływu pracy w Dify. Znajdziesz go w dokumentacji API opublikowanej aplikacji.
- **Method:** Wybierz **POST**, ponieważ wysyłasz dane w celu rozpoczęcia procesu.
- **Headers:** Dodaj jeden nagłówek. Nazwa: `Authorization`, Wartość: `Bearer [Twój_Klucz_API_z_Dify]`.
- **Body type:** Wybierz `Raw` z typem zawartości `application/json`.
- **Request content:** Wklej tutaj strukturę JSON, której oczekuje Dify. Zmapuj w niej dane wyjściowe z modułu **Transform to JSON**.

**⚠️ Ważna wskazówka:** Mapując zmienne z modułu **Transform to JSON**, nie umieszczaj ich w cudzysłowach w ciele żądania. Te zmienne są już poprawnie sformatowanym JSON-em. Zawsze zaznaczaj opcję **Parse response**.

### Krok 3: Pierwsze uruchomienie i mapowanie wyników

Aby Make.com "nauczył się", jaką strukturę danych zwraca Dify, musisz uruchomić scenariusz jeden raz (klikając "Run once"). Proces zakończy się błędem przy module zapisu (jeśli już go dodałeś) lub po prostu się zatrzyma, ale co najważniejsze – Make pozna strukturę odpowiedzi.

### Krok 4: Zapisanie danych i aktualizacja statusu

Teraz możesz dodać ostatni moduł: **Google Sheets > Update a Row**.

**Konfiguracja:**
- **Row number:** Zmapuj numer wiersza z pierwszego modułu (triggera). To gwarantuje, że zaktualizujesz właściwy wiersz.
- **Mapowanie danych:** W odpowiednich kolumnach zmapuj dane wyjściowe z modułu HTTP (frazy, graf informacji, nagłówki, knowledge graph).
- **Aktualizacja statusu:** W kolumnie **Status** wpisz ręcznie wartość **"gotowe"**. To kluczowy krok, który zapobiegnie ponownemu przetworzeniu tego samego wiersza w przyszłości.

---

## Uruchomienie i planowanie automatyzacji

Po zapisaniu scenariusza możesz go uruchomić ponownie. Tym razem powinien przejść od początku do końca, pobierając dane z wiersza ze statusem "generuj" i zapisując w nim wyniki wraz ze statusem "gotowe".

Aby proces był w pełni autonomiczny, możesz ustawić harmonogram działania scenariusza (np. co 15 minut), dzięki czemu będzie on samoczynnie sprawdzał arkusz w poszukiwaniu nowych zadań.

---

## Kluczowe elementy systemu

### Panel sterowania (Google Sheets)
- **Funkcja:** Interfejs użytkownika do zarządzania procesem
- **Kolumny wejściowe:** Słowo kluczowe, język, AI Overview, status
- **Kolumny wynikowe:** Frazy, graf informacji, nagłówki, knowledge graph
- **Kontrola procesu:** Lista rozwijana ze statusami sterująca automatyzacją

### Silnik automatyzacji (Make.com)
- **Trigger:** Google Sheets Search Rows z filtrem statusu
- **Przetwarzanie:** JSON Transform + HTTP Request do Dify
- **Zapis wyników:** Update Row w Google Sheets z aktualizacją statusu
- **Harmonogram:** Automatyczne sprawdzanie co 15 minut

### System przetwarzania (Dify)
- **Endpoint API:** Przyjmuje dane z arkusza przez Make.com
- **Workflow:** Przetwarzanie słów kluczowych, AI Overview i języka
- **Zwracane dane:** Strukturalny JSON z wynikami analizy
- **Integracja:** Seamless connection z Make.com przez API

---

## Zalety automatyzacji

1. **Skalowalność:** Możliwość przetwarzania wielu fraz jednocześnie
2. **Spójność:** Jednolity proces dla wszystkich zadań
3. **Efektywność:** Eliminacja ręcznej pracy przy rutynowych zadaniach
4. **Kontrola:** Łatwe zarządzanie przez interfejs arkusza kalkulacyjnego
5. **Monitoring:** Przejrzysty system statusów i wyników

---

**Link do lekcji na platformie:** [SensAI Academy - Lekcja T8L03](https://learn.sensai.academy/next/public/lesson/353) 