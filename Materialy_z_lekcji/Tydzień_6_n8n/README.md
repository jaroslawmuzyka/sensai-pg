# Materiały do Tygodnia 6: n8n - Automatyzacja przepływów pracy

Ten katalog zawiera materiały dodatkowe do lekcji z szóstego tygodnia kursu SEO 3.0, poświęconego platformie n8n do automatyzacji przepływów pracy.

**Uwaga:** Wszystkie datasety używane w kursie są dostępne w centralnym katalogu [`../../Datasety`](../../Datasety).

---

## Wprowadzenie do n8n

N8n to potężne narzędzie do automatyzacji przepływów pracy (workflow automation), które pozwala łączyć, przetwarzać i automatyzować zadania między różnymi aplikacjami i usługami. W przeciwieństwie do wielu innych narzędzi tego typu, n8n jest open-source i można je hostować lokalnie, co daje większą kontrolę nad danymi i procesami.

### Kluczowe cechy n8n:

* **Elastyczność** - możliwość tworzenia złożonych przepływów pracy z wieloma warunkami i rozgałęzieniami
* **Bogata biblioteka integracji** - gotowe węzły (nodes) do połączenia z popularnymi usługami i API
* **Możliwość hostowania lokalnie** - pełna kontrola nad danymi i procesami
* **Interfejs wizualny** - intuicyjny edytor przepływów typu "przeciągnij i upuść"
* **Możliwość tworzenia własnych węzłów** - rozszerzanie funkcjonalności według własnych potrzeb
* **Wsparcie dla JavaScript** - możliwość dodawania niestandardowej logiki za pomocą kodu

---

# Tematy omawiane w tygodniu 6

## Wprowadzenie i podstawy
- Wstęp do tygodnia

## Instalacja n8n
- Lekcja wstępna do instalacji
- Jakie instalacje wybrać
- Instalacja n8n na localhost
- Instalacja n8n na Hetznerze (lub dowolnym VPS)
- Instalacja n8n na Railway
- Instalacja n8n na Elestio

## Podstawy pracy z n8n
- Interfejs n8n
- Łączenie bloków
- Import szablonów

## Praca z API i danymi
- Pobieranie danych ze strony
- Korzystanie z zewnętrznych API
- Korzystanie z zewnętrznych API - Senuto
- Korzystanie z zewnętrznych API - Senuto Widocznosc Domeny
- Połączenie n8n z rownowaznikiem @mat

## Integracje z narzędziami Google
- Połączenie n8n z narzędziami Google
- Google Trends to Google Sheets
- Eksport treści do Google Docs

## Integracje z CMS i bazami danych
- WordPress - część 1
- WordPress - część 2 (grafika wyróżniająca)

## Praca z Qdrant
- Podstawy pracy z Qdrant
- Zaawansowana praca z Qdrant

## Blok Agenta
- Blok agenta
- Agent korzystający z zewnętrznych API
- Rozmowa ze strona w n8n

## Integracje z komunikatorami
- Łączenie ze Slackiem
- Integracja z Telegramem

---

# Oczekiwane rezultaty

Po ukończeniu tygodnia 6 kursu SEO 3.0 będziesz potrafił:

* Zainstalować n8n za pomocą Dockera i skonfigurować dostęp przez subdomenę
* Tworzyć konta i zarządzać dostępem do instancji n8n
* Projektować i implementować złożone workflow automatyzujące zadania
* Łączyć n8n z różnymi zewnętrznymi API i serwisami
* Tworzyć własne endpointy API do wykorzystania przez inne systemy
* Konfigurować i wykorzystywać bloki agentów AI w workflow
* Tworzyć narzędzia dla agentów AI i integrować je z workflow
* Automatyzować zadania SEO z wykorzystaniem n8n i zewnętrznych narzędzi
* Implementować systemy monitoringu i alertów dla procesów SEO
* Integrować n8n z systemami CMS (WordPress)
* Projektować workflow zgodnie z najlepszymi praktykami
* Efektywnie debugować i rozwiązywać problemy w workflow

---

# Źródła wiedzy

W tej sekcji znajdziesz dodatkowe materiały i źródła, które mogą być pomocne w zgłębianiu tematów związanych z n8n i automatyzacją przepływów pracy.

* [Oficjalna dokumentacja n8n](https://docs.n8n.io/)
* [Repozytorium GitHub n8n](https://github.com/n8n-io/n8n)
* [Biblioteka natywnych integracji n8n](https://n8n.io/integrations)
* [Przykłady przepływów pracy n8n](https://n8n.io/workflows)
* [Blog n8n z poradnikami i przykładami](https://blog.n8n.io/)
* [Dokumentacja Docker dla n8n](https://hub.docker.com/r/n8nio/n8n)
* [Przewodnik po API WordPress](https://developer.wordpress.org/rest-api/)
* [Dokumentacja API WooCommerce](https://woocommerce.github.io/woocommerce-rest-api-docs/)
* [Dokumentacja Google API](https://developers.google.com/docs/api)
* [Dokumentacja QDRANT](https://qdrant.tech/documentation/)

---

# Struktura katalogu

Ten katalog zawiera następujące podkatalogi z materiałami dodatkowymi:

*   [`DOCKER/`](./DOCKER/) - Materiały dotyczące instalacji i konfiguracji środowiska Docker.
*   [`INSTALACJA_N8N/`](./INSTALACJA_N8N/) - Instrukcje dotyczące różnych metod instalacji n8n (na localhost, na VPS z PostgreSQL, na VPS z PostgreSQL i workerami).
*   [`LINUX/`](./LINUX/) - Podstawowe informacje i komendy związane z systemem operacyjnym Linux, przydatne przy pracy z serwerami VPS.
*   [`PRZYKLADOWE_ZGLOSZENIE_DO_CREATORS/`](./PRZYKLADOWE_ZGLOSZENIE_DO_CREATORS/) - Przykład zgłoszenia szablonu workflow do społeczności n8n Creators zgodnie z wytycznymi.
*   [`SCENARIUSZE/`](./SCENARIUSZE/) - Przykładowe scenariusze (workflowy) n8n gotowe do wykorzystania.

*W tym katalogu pojawią się materiały do poszczególnych lekcji z Tygodnia 6, w tym notatki, transkrypcje, przykładowe przepływy pracy i inne zasoby związane z n8n.*

# Zadanie domowe

Zadanie domowe jest bardzo proste. Chciałbym żebyś przygotowała / przygotowała jakąś prostę automatyzację związaną z Twoją pracą. Jeden bardzo prosty workflow, który oszczędzi Ci parę minut na operacji.

Może to być np.
- Bot na telegramie, który po przesłaniu linka znajdzie na stronie nagłówki,
- Bot, który będzie ułatwiał Ci tworzenie raportu na podstawie danych z SENUTO
- Zapisywanie AI Overviews do Google Sheets (tu masz wtyczkę:  obsługującą webhook https://github.com/romek-rozen/ai-overview-extractor ) 
- Listowanie słów zależnych
- ...


## Co zrobić żeby zaliczyć? 
- Przygotuj Google Docs:
  - Jaki proces realizuje?
  - Jaki problem rozwiązuje?
  - Dlaczego trzeba było to zautomatyzować?
  - Jakie miałaś, miałeś największe problemy i jak sobie poradziłaś, poradziłeś?
  - Masz maksymalnie jedną stronę A4 z marginesami 1.5 z każdej strony.

- Przygotuj (wyeksportuj) swój główny workflow:
  - Workflow powinien być tak skonstruowany, żeby osoba bez znajomości Twojego problemu będzie umiała go użyć,
  - Tutaj masz wytyczne dla "creatorów" szablonów z N8n : https://github.com/romek-rozen/ai-overview-extractor/blob/main/n8n-template-submission/template-submission-guidelines.md 
  - Tutaj możesz zobaczyć jak wygląda proces przygotowywania takiego "zgłoszenia" : https://github.com/romek-rozen/ai-overview-extractor/tree/main/n8n-template-submission
  - Wytyczna dotycząca nazewnictwa węzłów: Aby zwiększyć przejrzystość i ułatwić użytkownikom zrozumienie przebiegu pracy, zaleca się nadawanie kluczowym węzłom opisowych, jednoznacznych nazw. 
  - Unikaj ogólnych lub technicznych terminów, które mogą być niezrozumiałe dla osób spoza zespołu. 
  - Opisowe nazwy pomagają szybko zidentyfikować funkcję każdego elementu i usprawniają nawigację w procesie.
  - Przykład: Zamiast nazwy „data” użyj nazwy „Pobieranie danych wejściowych”, zamiast „Basic LLM Chain” – „Analiza tekstu przez model językowy”, zamiast „Markdown” – „Formatowanie tekstu do Markdown”.


### Podpowiedzi
- Korzystaj aktywnie z jakiegoś LLM przy projektowaniu workflow.
- Korzystaj aktywnie z cursora / cline / kilo code przy przygotowywaniu dokumentacji .
- Staraj się naprawdę nie utrudniać i zacznij od prostych operacji.
