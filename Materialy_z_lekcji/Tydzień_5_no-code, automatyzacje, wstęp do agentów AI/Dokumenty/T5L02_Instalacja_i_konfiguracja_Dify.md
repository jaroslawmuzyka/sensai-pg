# Instalacja i wstępna konfiguracja Dify na własnym serwerze

Ta notatka przeprowadzi Cię krok po kroku przez proces instalacji narzędzia **Dify** na własnym serwerze. Jest to alternatywa dla płatnej wersji SaaS, pozwalająca na korzystanie z **Dify** za darmo (poza kosztem serwera). Wszystkie komendy użyte w tej lekcji będą również dostępne w formie tekstowej pod materiałem wideo, co ułatwi ich skopiowanie i wykonanie.

---

## Wymagania wstępne

Przed przystąpieniem do instalacji, upewnij się, że dysponujesz:

- **Serwerem VPS:** Dowolny dostawca chmury lub serwer VPS (np. Hetzner, OVH, CyberFolks). W tej lekcji wykorzystywany jest Hetzner.
- **Dostępem do terminala:** Będziesz potrzebować połączyć się z serwerem przez SSH. Użytkownicy Windows mogą użyć narzędzia PuTTY, natomiast użytkownicy macOS i Linux mogą skorzystać z wbudowanego terminala.
- **Podstawową wiedzą o Dockerze (opcjonalnie):** **Dify** jest uruchamiane w kontenerach Docker. Wybierzemy obraz systemu z preinstalowanym Dockerem, aby uprościć proces.

---

## Krok 1: Przygotowanie serwera (przykład na Hetzner Cloud)

Poniższe kroki opisują tworzenie i konfigurację serwera w panelu Hetzner Cloud. Proces może wyglądać podobnie u innych dostawców.

1. **Zaloguj się do panelu Hetzner Cloud.**
2. **Stwórz serwer:**
   - Kliknij **Create Resource** (lub podobny przycisk) i wybierz **Server**.
   - **Lokalizacja:** Wybierz preferowaną lokalizację (w lekcji wybrano Helsinki ze względu na ekologiczne aspekty, takie jak chłodzenie wodą morską).
   - **System operacyjny:** Przejdź do zakładki **Apps** i wybierz **Docker**. Spowoduje to instalację systemu Ubuntu z już zainstalowanym Dockerem, co upraszcza proces.
   - **Typ serwera:** Wybierz odpowiedni typ serwera. Na potrzeby tej lekcji i testów wystarczy najtańsza opcja (np. 2 CPU, 2GB RAM, 40GB dysku).
     - **Wskazówka:** Jeśli planujesz intensywnie korzystać z **Dify** i przetwarzać duże ilości danych, rozważ wybór serwera z większą przestrzenią dyskową (np. 80GB), ponieważ **Dify** generuje logi i pliki, które mogą zajmować miejsce.
   - **Sieć:** Wybierz IPv4. IPv6 jest opcjonalne.
   - **Klucz SSH:** Zalecane jest dodanie publicznego klucza SSH dla bezpiecznego logowania.
     - W systemie macOS klucz publiczny domyślnie znajduje się w pliku `~/.ssh/id_rsa.pub`.
     - Jeśli nie dodasz klucza SSH, hasło roota zostanie wysłane na Twój adres e-mail.
   - **Dodatkowe opcje:**
     - **Wolumeny:** Dodatkowe dyski (niepotrzebne na tym etapie).
     - **Firewall:** Można skonfigurować później (niepotrzebne na tym etapie).
     - **Backupy:** **Zalecane jest włączenie backupów!** Dzięki temu będziesz miał kopie zapasowe **Dify** (np. 7 dni wstecz), co pozwoli na odtworzenie systemu w razie problemów.
   - **Nazwa serwera:** Nadaj serwerowi nazwę (np. `dify-test`) i kliknij **Create & Buy now**.
3. **Oczekiwanie na serwer:** Poczekaj kilkadziesiąt sekund, aż serwer zostanie utworzony i zainicjowany. Następnie skopiuj jego adres IP – będzie potrzebny do połączenia.

---

## Krok 2: Połączenie z serwerem przez SSH

1. Otwórz terminal (na macOS/Linux) lub PuTTY (na Windows).
2. Użyj skopiowanego adresu IP, aby połączyć się z serwerem jako użytkownik `root`. Komenda wygląda następująco:
   ```bash
   ssh root@TWOJ_ADRES_IP_SERWERA
   ```
   (Zastąp `TWOJ_ADRES_IP_SERWERA` faktycznym adresem IP).
3. Przy pierwszym połączeniu możesz zostać poproszony o potwierdzenie autentyczności hosta. Wpisz `yes`.

---

## Krok 3: Aktualizacja systemu

Po zalogowaniu się na serwer, dobrą praktyką jest zaktualizowanie listy pakietów systemowych.

```bash
apt update
```

Ta komenda pobierze najnowsze informacje o dostępnych pakietach.

---

## Krok 4: Pobranie Dify z GitHub

1. Wyszukaj w Google "**Dify** GitHub" aby przejść do oficjalnego repozytorium **Dify**.
2. Na stronie repozytorium **Dify** na GitHubie, kliknij zielony przycisk **Code**, a następnie skopiuj adres URL podany w sekcji HTTPS.
3. W terminalu serwera wykonaj komendę `git clone`, wklejając skopiowany adres:
   ```bash
   git clone ADRES_URL_REPOZYTORIUM_DIFY
   ```
   (Np. `git clone https://github.com/langgenius/dify.git` - sprawdź aktualny adres na GitHubie!).
   Ta komenda pobierze pliki instalacyjne **Dify** na Twój serwer do katalogu o nazwie `dify`.
4. Sprawdź, czy katalog został pobrany, listując zawartość bieżącego katalogu:
   ```bash
   ls
   ```
   Powinieneś zobaczyć katalog `dify`.

---

## Krok 5: Instalacja Dify za pomocą Docker Compose

**Dify** wykorzystuje Docker Compose do zarządzania kontenerami. Wszystkie potrzebne komendy znajdują się zazwyczaj w dokumentacji **Dify** na GitHubie.

1. **Przejdź do odpowiedniego katalogu w sklonowanym repozytorium:**
   ```bash
   cd dify/docker
   ```
2. **Skopiuj przykładowy plik środowiskowy:**
   ```bash
   cp .env.example .env
   ```
   Ta komenda tworzy plik konfiguracyjny `.env` z domyślnymi wartościami.
3. **Uruchom Dify:**
   ```bash
   docker-compose up -d
   ```
   Ta komenda pobierze wszystkie niezbędne obrazy Docker (m.in. Nginx, API **Dify**, bazy danych, pluginy) i uruchomi kontenery w tle (`-d` oznacza tryb "detached").
4. **Oczekiwanie na pobranie i uruchomienie:** Proces ten może zająć kilka minut, w zależności od prędkości serwera i połączenia internetowego. W terminalu zobaczysz logi pobierania i tworzenia kontenerów.

---

## Krok 6: Sprawdzenie statusu i oczekiwanie na pełne uruchomienie

Po wykonaniu komendy `docker-compose up -d` kontenery zaczną się uruchamiać, ale pełna inicjalizacja **Dify** może jeszcze chwilę potrwać.

- **Ważna wskazówka:** Daj systemowi kilka minut na pełne uruchomienie wszystkich usług **Dify**. Bezpośrednio po starcie kontenerów, aplikacja może nie być od razu dostępna lub działać wolno.
- **Monitorowanie obciążenia (opcjonalnie):**
  - Możesz użyć komendy `w`, aby sprawdzić `load average` (średnie obciążenie systemu). Jeśli wartości są wysokie (np. wyższe niż liczba rdzeni procesora), oznacza to, że serwer jest intensywnie wykorzystywany, prawdopodobnie przez procesy instalacyjne **Dify**.
  - Komenda `htop` (jeśli nie jest zainstalowana, możesz ją zainstalować przez `apt install htop`) pokazuje szczegółową listę procesów. Możesz zaobserwować procesy związane z **Dify**, które zużywają zasoby. Poczekaj, aż obciążenie spadnie.

Gdy zobaczysz komunikaty typu `created`, `started`, `healthy` dla kontenerów, a obciążenie serwera wróci do normy, **Dify** powinno być gotowe.

---

## Krok 7: Dostęp do zainstalowanego Dify

1. Otwórz przeglądarkę internetową.
2. W pasku adresu wpisz adres IP swojego serwera, poprzedzony `http://` (bez `s`, ponieważ na tym etapie nie konfigurowaliśmy certyfikatu SSL):
   ```
   http://TWOJ_ADRES_IP_SERWERA
   ```
3. Powinieneś zobaczyć stronę powitalną **Dify**, gdzie zostaniesz poproszony o utworzenie konta administratora (podanie loginu i hasła).
4. Po utworzeniu konta, zaloguj się przy użyciu tych samych danych.

Gratulacje! Masz teraz działającą instancję **Dify** na własnym serwerze.

---

## Krok 8: Wstępna konfiguracja w Dify

Po zalogowaniu się do **Dify**:

- Zapoznaj się z interfejsem, który powinien być taki sam jak w wersji SaaS.
- Przejdź do sekcji **Ustawienia** (Settings) -> **Dostawcy Modeli** (Model Providers) lub **Narzędzia** (Tools) -> **Marketplace**, aby zainstalować potrzebne wtyczki, np. dla OpenAI. Kliknij przycisk instalacji przy wybranym modelu lub narzędziu.

---

## Co dalej?

Pomyślnie zainstalowałeś **Dify** na swoim serwerze. W kolejnej lekcji omówiony zostanie proces aktualizacji **Dify** do nowszych wersji.

---

**Platforma kursu:** [Instalacja i wstępna konfiguracja Dify na własnym serwerze](https://learn.sensai.academy/next/public/lesson/295) 