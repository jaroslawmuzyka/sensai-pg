# Materiały do Tygodnia 6: n8n - Automatyzacja przepływów pracy

Ten katalog zawiera materiały dodatkowe do lekcji z szóstego tygodnia kursu SEO 3.0, poświęconego platformie n8n do automatyzacji przepływów pracy.

**Uwaga:** Wszystkie datasety używane w kursie są dostępne w centralnym katalogu [`../../Datasety`](../../Datasety).

---

## Wprowadzenie do n8n

n8n to potężne narzędzie do automatyzacji przepływów pracy (workflow automation), które pozwala łączyć, przetwarzać i automatyzować zadania między różnymi aplikacjami i usługami. W przeciwieństwie do wielu innych narzędzi tego typu, n8n jest open-source i można je hostować lokalnie, co daje większą kontrolę nad danymi i procesami.

### Kluczowe cechy n8n:

* **Elastyczność** - możliwość tworzenia złożonych przepływów pracy z wieloma warunkami i rozgałęzieniami
* **Bogata biblioteka integracji** - gotowe węzły (nodes) do połączenia z popularnymi usługami i API
* **Możliwość hostowania lokalnie** - pełna kontrola nad danymi i procesami
* **Interfejs wizualny** - intuicyjny edytor przepływów typu "przeciągnij i upuść"
* **Możliwość tworzenia własnych węzłów** - rozszerzanie funkcjonalności według własnych potrzeb
* **Wsparcie dla JavaScript** - możliwość dodawania niestandardowej logiki za pomocą kodu

---

## Tematy omawiane w tygodniu 6

### Lekcja 1: Wprowadzenie do n8n
* Czym jest n8n i jakie są jego główne funkcje
* Porównanie z innymi narzędziami do automatyzacji
* Architektura i filozofia działania n8n
* Przegląd interfejsu użytkownika

### Lekcja 2: Instalacja i korzystanie z n8n
* Opcje instalacji: cloud, mikr.us, selfhosted, local
* Konfiguracja środowiska Docker
* Pierwsze uruchomienie i konfiguracja
* Zarządzanie instancją n8n

### Lekcja 3: Podstawy pracy z n8n
* Dane logowania i zarządzanie dostępem
* Podstawowe bloki do komunikacji
* Konfiguracja credentiali dla różnych serwisów
* Szczegółowa konfiguracja dla Google API

### Lekcja 4: Przetwarzanie danych w n8n
* Przetwarzanie różnych typów danych (JSON, CSV, XML)
* Transformacja i mapowanie danych
* Łączenie i dzielenie strumieni danych
* Filtrowanie i sortowanie danych

### Lekcja 5: Komunikacja z zewnętrznymi API
* Blok HTTP Request i jego możliwości
* Korzystanie z dokumentacji API
* Autoryzacja i uwierzytelnianie w zapytaniach
* Obsługa odpowiedzi i błędów

### Lekcja 6: Integracja z WordPress i WooCommerce
* Konfiguracja połączenia z WordPress
* Automatyzacja zadań w WordPress
* Integracja z WooCommerce
* Przykłady praktycznych workflow

### Lekcja 7: Tworzenie narzędzi dla agentów AI
* Projektowanie narzędzi do ponownego wykorzystania
* Tworzenie endpointów dla agentów AI
* Integracja narzędzi z innymi blokami
* Testowanie i debugowanie narzędzi

### Lekcja 8: Obsługa błędów i workflow design
* Strategie obsługi błędów w n8n
* Najlepsze praktyki projektowania workflow
* Optymalizacja wydajności
* Monitorowanie i debugowanie

### Lekcja 9: Bloki agentów i zewnętrzne wywołania
* Konfiguracja i wykorzystanie bloków agentów
* Wywoływanie workflow przez zewnętrzne systemy
* Integracja z komunikatorami (Slack, Discord, Telegram)
* Tworzenie webhooków i API endpoints

---

## Projekty praktyczne

W ramach tygodnia 6 zrealizujemy szereg praktycznych projektów, które pozwolą zastosować zdobytą wiedzę w praktyce:

### Projekt 1: Endpointy do konwersji formatów
* Przygotowanie endpointów do realizacji prostych zadań
* Konwersja HTML do Markdown
* Konwersja Markdown do HTML
* Tworzenie API dla tych funkcjonalności

### Projekt 2: Agent do tworzenia schema.org
* Budowa agenta analizującego strony internetowe
* Automatyczne generowanie znaczników schema.org
* Walidacja wygenerowanych schematów
* Integracja z systemami CMS

### Projekt 3: Integracja z SENUTO
* Konfiguracja połączenia z API SENUTO
* Automatyczne pobieranie danych o widoczności
* Analiza i przetwarzanie danych SEO
* Generowanie raportów i alertów

### Projekt 4: Monitoring trendów Google
* Pobieranie aktualnych trendów z Google Trends
* Analiza i filtrowanie danych
* Automatyczne powiadomienia o nowych trendach
* Integracja z narzędziami planowania treści

### Projekt 5: Automatyzacja pracy z Neuronwriter
* Automatyczne tworzenie zadań w Neuronwriter
* Pobieranie wytycznych i sugestii z Neuronwriter
* Integracja z procesem tworzenia treści
* Monitorowanie postępów i statusów zadań

### Projekt 6: Wektorowa baza danych QDRANT
* Konfiguracja i połączenie z QDRANT
* Przechowywanie i indeksowanie danych wektorowych
* Wyszukiwanie semantyczne w bazie danych
* Integracja z agentami AI

### Projekt 7: Automatyczna publikacja treści
* Pobieranie treści z Google Docs
* Przetwarzanie i formatowanie treści
* Automatyczna publikacja w WordPress
* Planowanie i zarządzanie harmonogramem publikacji

---

## Oczekiwane rezultaty

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
* Integrować n8n z systemami CMS (WordPress) i e-commerce (WooCommerce)
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

*W tym katalogu pojawią się materiały do poszczególnych lekcji z Tygodnia 6, w tym notatki, transkrypcje, przykładowe przepływy pracy i inne zasoby związane z n8n.*
