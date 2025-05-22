# Instalacja n8n na localhost przy użyciu Docker Compose

Ta instrukcja opisuje kroki niezbędne do zainstalowania i uruchomienia n8n na Twoim lokalnym komputerze przy użyciu Docker i Docker Compose.

**Wymagania wstępne:**

Upewnij się, że masz zainstalowane:
*   Docker
*   Docker Compose

Jeśli ich nie masz, znajdziesz instrukcje instalacji w materiałach kursu (np. w sekcji o Dockerze).

**Kroki instalacji:**

1.  **Utwórz katalog konfiguracji Docker:**
    Utwórz nowy katalog na swoim komputerze, w którym będziesz przechowywać pliki konfiguracyjne Docker dla n8n (np. `Dokumenty > Docker > n8n-localhost`).

2.  **Umieść pliki konfiguracyjne:**
    W utworzonym katalogu umieść dwa pliki:
    *   `.env` - zawiera zmienne środowiskowe dla konfiguracji bazy danych i n8n.
    *   `docker-compose.yml` - definiuje usługi (kontenery) n8n, bazy danych, Redis i Qdrant oraz ich konfigurację.

3.  **Utwórz wolumeny Docker:**
    Wolumeny Docker służą do trwałego przechowywania danych generowanych przez kontenery. Utwórz następujące wolumeny:

    ```bash
    docker volume create n8n_storage
    docker volume create postgres_storage
    docker volume create redis_storage
    docker volume create qdrant_storage
    ```
    *   `n8n_storage`: Przechowuje dane konfiguracyjne i workflowy n8n.
    *   `postgres_storage`: Przechowuje dane bazy danych PostgreSQL używanej przez n8n.
    *   `redis_storage`: Przechowuje dane Redis, używanego przez n8n do cache'owania i kolejek.
    *   `qdrant_storage`: Przechowuje dane bazy wektorowej Qdrant, używanej przez n8n do pracy z wektorami.

4.  **Utwórz katalog `files` (opcjonalnie):**
    Utwórz katalog o nazwie `files` w tym samym miejscu co pliki `.env` i `docker-compose.yml`. Ten katalog będzie zamapowany do kontenera n8n i pozwoli na dostęp do lokalnych plików z poziomu workflowów n8n.

5.  **Uruchom kontenery:**
    Otwórz terminal, przejdź do katalogu, w którym umieściłeś pliki `.env` i `docker-compose.yml`, a następnie uruchom kontenery za pomocą polecenia:

    ```bash
    docker compose up -d
    ```
    Opcja `-d` uruchamia kontenery w tle.

    Pierwsze uruchomienie może trwać dłużej, ponieważ Docker musi pobrać wszystkie niezbędne obrazy kontenerów.

**Dostęp do n8n:**

Po pomyślnym uruchomieniu kontenerów, interfejs n8n będzie dostępny w przeglądarce pod adresem: `http://localhost:5678`.

**Aktualizacja n8n:**

Aby zaktualizować n8n do najnowszej wersji, wykonaj następujące kroki w katalogu z plikiem `docker-compose.yml`:

1.  Zatrzymaj działające kontenery:
    ```bash
    docker compose down
    ```
2.  Pobierz najnowszy obraz n8n:
    ```bash
    docker compose pull
    ```
3.  Uruchom kontenery ponownie:
    ```bash
    docker compose up -d
    ```

**Zatrzymywanie i usuwanie:**

Aby zatrzymać kontenery, użyj polecenia w katalogu z plikiem `docker-compose.yml`:

```bash
docker compose down
```

Aby zatrzymać i usunąć kontenery oraz sieci (ale zachować wolumeny z danymi), użyj:

```bash
docker compose down
```

Aby zatrzymać i usunąć kontenery, sieci ORAZ wolumeny (co spowoduje utratę danych n8n, bazy danych itp.), użyj:

```bash
docker compose down -v
