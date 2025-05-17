### Wprowadzenie do Google Colab

Google Colab (Google Colaboratory) to usługa oparta na Jupiter Notebook, umożliwiająca pisanie i uruchamianie kodu Python w przeglądarce. Jest to notatnik do tworzenia komórek z kodem i tekstem opisującym.

**Dlaczego warto korzystać z Google Colab?**

*   **Brak konfiguracji:** Działa w chmurze Google, nie wymaga instalacji Pythona na komputerze. Alternatywą lokalną jest Anaconda.
*   **Moc obliczeniowa:** Dostęp do zasobów Google (GPU, TPU) przydatnych przy wymagających zadaniach.
*   **Dokumentowanie kodu:** Łatwe tworzenie czytelnej dokumentacji dzięki przeplataniu kodu i tekstu (Markdown).
*   **Wersja darmowa:** Podstawowa wersja jest darmowa i wystarczająca do wielu zadań.
*   **Integracja ze środowiskiem Google:** Działa podobnie do Google Docs, ułatwia udostępnianie i współpracę. Integracja z Google Drive.

**Wymagania:**

*   Przeglądarka internetowa.
*   Konto Google.

Aby rozpocząć, wejdź na `colab.research.google.com`.

### Podstawowe elementy i funkcje Google Colab

Notatnik składa się z komórek tekstowych i kodowych.

**Komórki tekstowe**
Służą do opisów, wyjaśnień, nagłówków.

*   **Formatowanie:** Użycie języka Markdown lub wbudowanego edytora wizualnego.
*   **Opcje komórki:** Przesuwanie, linkowanie, komentowanie, kopiowanie, usuwanie, dostosowywanie wyglądu.

**Komórki kodowe**
Miejsce na kod do wykonania.

*   **Obsługiwane języki:** Głównie Python, także R.
*   **Uruchamianie kodu:** Kliknięcie ikony "play" lub skrót klawiszowy. Wynik pod komórką.

Przykład prostego skryptu:
```python
print("Automatyzacja i analiza danych to klucz do SEO 3.0 Sense AI")
```

**Praca ze zmiennymi**

Przechowywanie wartości do późniejszego wykorzystania.

Definiowanie zmiennej:
```python
glowne_slowo_kluczowe = "sztuczna inteligencja w SEO"
```
Odwoływanie się do zmiennej:
```python
print(f"Pracujemy nad słowem kluczowym: {glowne_slowo_kluczowe}")
```

**Formatowanie tekstu za pomocą Markdown**

*   Nagłówki: `# Nagłówek H1`, `## Nagłówek H2`.
*   Pogrubienie: `**tekst**`.
*   Kursywa: `*tekst*`.
*   Wstawianie fragmentów kodu (jako tekst): Użycie odwrotnych apostrofów \`kod\`.

**Interaktywne formularze**

Umożliwiają wprowadzanie danych bez edycji kodu, za pomocą komentarza `#@param`.

*Cel:* Ułatwienie korzystania z notatnika osobom nietechnicznym.

Przykład tworzenia formularza:
```python
nazwa_uzytkownika = "seo sensei" #@param {type:"string"}
```

*Typy formularzy:*

*   Pola tekstowe (string): `typ: "string"`
*   Pola liczbowe (integer, number): `typ: "integer"`
*   Suwaki (slider): `typ: "slider", min:0, max:1, step:0.01`
*   Listy rozwijane (dropdown): `["Polska", "Niemcy"]`
*   Pola wyboru (checkbox): `typ: "boolean"`
*   Kalendarze (date): `typ: "date"`

**Zarządzanie bibliotekami w Pythonie**

Biblioteki to zbiory gotowych funkcji.

*Preinstalowane biblioteki:* Wiele popularnych bibliotek (np. Pandas) jest już dostępnych. Wystarczy je zaimportować.
```python
import pandas as pd
```
*Instalowanie dodatkowych bibliotek:* Za pomocą menedżera pip.
```python
!pip install requests
!pip install beautifulsoup4
```
*Ważna uwaga:* W nowej sesji Colab (np. po ponownym otwarciu notatnika) biblioteki trzeba zainstalować/zaimportować ponownie.

**Środowisko wykonawcze (Runtime)**

Maszyna wirtualna w chmurze Google, która wykonuje kod.

*   *Zmiana typu środowiska:* Menu "Środowisko wykonawcze" -> "Zmień typ środowiska wykonawczego".
*   *Język programowania:* Python 3 (domyślnie) lub R.
*   *Akcelerator sprzętowy:*
    *   CPU: Standardowy procesor.
    *   GPU: Układ graficzny do złożonych obliczeń.
    *   TPU: Specjalistyczny układ Google do uczenia maszynowego.
*   *Zasoby:* Informacje o RAM i dysku widoczne w interfejsie.

**Integracja z Google Drive**

Praca na plikach przechowywanych na Dysku Google.

*Podłączanie Google Drive:* Wykonanie komórki z kodem do montowania Dysku.
```python
from google.colab import drive
drive.mount('/content/drive')
```
*Dostęp do plików:* Ścieżka `/content/drive/MyDrive/`.

Przykład listowania katalogu:
```bash
!ls "/content/drive/MyDrive/nazwa_twojego_folderu"
```
*Połączenie może wymagać ponownej autoryzacji w nowej sesji.*

**Praca zespołowa i udostępnianie**

Udostępnianie notatników podobnie jak Google Docs.

*   *Opcje udostępniania:* Przycisk "Udostępnij" - nadawanie uprawnień (przeglądanie, komentowanie, edytowanie).
*   *Kopiowanie notatnika:* Aby edytować notatnik tylko do odczytu, stwórz kopię ("Plik" -> "Zapisz kopię na Dysku").

**Dodatkowe funkcje i możliwości**

*Sekretne klucze (Obiekty tajne)*
Bezpieczne przechowywanie danych, np. kluczy API, w panelu po lewej stronie (ikona klucza).

*Zarządzanie aktywnymi sesjami*
Menu "Środowisko wykonawcze" -> "Zarządzaj sesjami". Kontrola nad aktywnymi notatnikami, możliwość zakończenia sesji.

**Płatne wersje Google Colab**

*   *Pay As You Go:* Płatność za zużycie.
*   *Colab Pro:* Więcej zasobów, szybsze GPU, więcej pamięci.
*   *Colab Pro+:* Jeszcze więcej zasobów, uruchamianie w tle (do 24h, nawet po zamknięciu przeglądarki).
*   *Colab Enterprise:* Dla firm, zaawansowane zarządzanie, planowanie uruchomień.

**Integracja z Google Gemini**

Modele językowe Gemini w Colab.

*   *Wyjaśnianie kodu:* Zaznacz kod i poproś Gemini o wyjaśnienie.
*   *Analiza plików z Gemini (Agent AI):* Wgraj plik i zleć Gemini analizę danych za pomocą promptu. Agent wygeneruje i wykona kod (np. w Pythonie z Pandas) do analizy statystycznej i wizualizacji.

**Podsumowanie**

Google Colab to wszechstronne narzędzie do pracy z Pythonem, analizą danych i automatyzacją. Zachęcamy do samodzielnego eksperymentowania. 