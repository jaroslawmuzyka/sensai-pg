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

### 1. Wprowadzenie i podstawy
- Wstęp do tygodnia
- Lekcja wstępna do instalacji
- Jakie instalacje wybrać

### 2. Instalacja n8n
- Instalacja n8n na localhost
- Instalacja n8n na Hetznerze
- Instalacja n8n na Mikrusie
- Instalacja n8n na Railway
- Instalacja n8n na Elestio

### 3. Podstawy pracy z n8n
- Interfejs n8n
- Łączenie bloków
- Blok agenta
- Import szablonów

### 4. Integracje z narzędziami Google
- Połączenie n8n z narzędziami Google
- Google Trends to Google Sheets
- Eksport do GDocs

### 5. Integracje z CMS i bazami danych
- WordPress - część 1
- WordPress - część 2
- Podstawy pracy z Qdrant
- Zaawansowana praca z Qdrant

### 6. Praca z API i danymi
- Pobieranie danych ze strony
- Korzystanie z zewnętrznych API
- Integracja z Senuto
- Senuto - Widoczność Domeny
- Agent korzystający z zewnętrznych API
- Połączenie n8n z rownowaznikiem

### 7. Integracje z komunikatorami
- Łączenie ze Slackiem
- Integracja z Telegramem

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

## Struktura katalogu

Ten katalog zawiera następujące podkatalogi z materiałami dodatkowymi:

*   [`DOCKER/`](./DOCKER/) - Materiały dotyczące instalacji i konfiguracji środowiska Docker.
*   [`INSTALACJA_N8N/`](./INSTALACJA_N8N/) - Instrukcje dotyczące różnych metod instalacji n8n (na localhost, na VPS z PostgreSQL, na VPS z PostgreSQL i workerami).
*   [`LINUX/`](./LINUX/) - Podstawowe informacje i komendy związane z systemem operacyjnym Linux, przydatne przy pracy z serwerami VPS.
*   [`SCENARIUSZE/`](./SCENARIUSZE/) - Przykładowe scenariusze (workflowy) n8n gotowe do wykorzystania.

*W tym katalogu pojawią się materiały do poszczególnych lekcji z Tygodnia 6, w tym notatki, transkrypcje, przykładowe przepływy pracy i inne zasoby związane z n8n.*
