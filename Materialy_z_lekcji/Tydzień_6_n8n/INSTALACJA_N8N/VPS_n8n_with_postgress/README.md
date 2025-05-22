# Instalacja N8N z Postgress i Caddy

Na podstawie https://github.com/n8n-io/n8n-hosting/tree/main/docker-compose/withPostgresAndWorker + dodany Caddy jako reverse proxy.

## Wymagania wstępne

- Zainstalowany Docker i Docker Compose
- Domena i subdomena skonfigurowana do wskazywania na serwer
- Otwarty port 80 i 443 na serwerze

## Przygotowanie struktury katalogów

```bash
# Utwórz główny katalog
mkdir -p /home/$USER/n8n
cd /home/$USER/n8n

# Utwórz podkatalogi
mkdir -p local_files
mkdir -p caddy_config
```

## Utworzenie plików konfiguracyjnych

Utwórz plik `Caddyfile` w katalogu caddy_config:

```bash
nano caddy_config/Caddyfile
```

Wstaw następującą treść (zastąp n8n.twoja.domena swoją domeną):

```bash
n8n.twoja.domena {
    reverse_proxy n8n:5678
}
```

## Utworzenie wolumenów Docker

```bash
docker volume create n8n_storage
docker volume create caddy_data
```

## Przygotowanie plików Docker

Skopiuj zawartość plików do odpowiednich lokalizacji:

- `.env` - do katalogu głównego
- `compose.yml` - do katalogu głównego
- `init-data.sh` - do katalogu głównego

Upewnij się, że plik `init-data.sh` ma odpowiednie uprawnienia:

```
chmod +x init-data.sh
```

## Sprawdzenie i dostosowanie pliku .env

Plik `.env` zawiera następujące konfiguracje:

- Dane dostępowe do bazy danych PostgreSQL
- Klucz szyfrowania dla N8N
- Ścieżki do katalogów
- Konfiguracja domeny i subdomeny
- Ustawienia czasowe
- Adres email do certyfikatu SSL

Sprawdź i dostosuj te ustawienia według potrzeb, szczególnie:

- `DATA_FOLDER` - ścieżka do katalogów
- `DOMAIN_NAME` i `SUBDOMAIN` - nazwa domeny i subdomeny
- `SSL_EMAIL` - adres email do generowania certyfikatu SSL

### 6\. Uruchomienie kontenerów

```bash
docker compose up -d
```

Pierwsze uruchomienie może trwać dłużej, ponieważ Docker musi pobrać wszystkie obrazy.

### 7\. Weryfikacja działania

Po uruchomieniu, N8N powinien być dostępny pod adresem:

```php
https://adres.twojej.domeny
```

## Omówienie konfiguracji

### Struktura usług

- **postgres** - baza danych
- **redis** - usługa kolejkowania
- **caddy** - serwer proxy obsługujący certyfikaty SSL
- **n8n** - główny serwer N8N
- **n8n-worker** - pracownik obsługujący zadania
- **n8n-webhook** - obsługa webhooków

### Ustawienia N8N

- N8N używa bazy PostgreSQL z oddzielnym użytkownikiem
- Dane przechowywane są maksymalnie przez 7 dni (168 godzin)
- Maksymalna liczba przechowywanych wykonań: 10000
- Limit jednoczesnych zadań: 20
- Skonfigurowany serwer SMTP

### Bezpieczeństwo

- Wszystkie hasła i klucze są przechowywane w pliku .env
- Serwis używa HTTPS przez Caddy
- Baza danych używa oddzielnego użytkownika z ograniczonymi uprawnieniami

## Rozwiązywanie problemów

Jeśli N8N nie działa poprawnie:

```bash
# Sprawdź status kontenerów
docker compose ps

# Sprawdź logi
docker compose logs

# Logi konkretnego kontenera
docker compose logs n8n
docker compose logs postgres
docker compose logs caddy
```

## Aktualizacja N8N

```bash
# Zatrzymaj kontenery
docker compose down

# Pobierz najnowsze obrazy
docker compose pull

# Uruchom ponownie
docker compose up -d
```

Ta instrukcja powinna pomóc Ci zainstalować i skonfigurować N8N przy użyciu przesłanych plików Docker.

# Lista plików

[.env](/api/files/01969f33-4e01-73be-a2fc-07e39340316a/.env)

[compose.yml](/api/files/01969f32-b83b-714e-b5d1-1d2d8c8c0343/compose.yml)

[init-data.sh](/api/files/01969f33-257b-7141-9e47-e9d012a14978/init-data.sh)

**compose.yml**

```dockerfile
services:
  n8n:
    image: docker.n8n.io/n8nio/n8n
    restart: always
    environment:
      - N8N_HOST=${SUBDOMAIN}.${DOMAIN_NAME}
      - N8N_PORT=5678
      - N8N_PROTOCOL=https
      - NODE_ENV=production
      - WEBHOOK_URL=https://${SUBDOMAIN}.${DOMAIN_NAME}/
      - GENERIC_TIMEZONE=${GENERIC_TIMEZONE}
      - DB_TYPE=postgresdb
      - DB_POSTGRESDB_HOST=postgres
      - DB_POSTGRESDB_PORT=5432
      - DB_POSTGRESDB_DATABASE=${POSTGRES_DB}
      - DB_POSTGRESDB_USER=${POSTGRES_NON_ROOT_USER}
      - DB_POSTGRESDB_PASSWORD=${POSTGRES_NON_ROOT_PASSWORD}
      - EXECUTIONS_MODE=queue
      - QUEUE_BULL_REDIS_HOST=redis
      - QUEUE_HEALTH_CHECK_ACTIVE=true
      - N8N_ENCRYPTION_KEY=${ENCRYPTION_KEY}
      - EXECUTIONS_DATA_PRUNE=true
      - EXECUTIONS_DATA_MAX_AGE=168 # 168 - 7 dni
      - EXECUTIONS_DATA_PRUNE_MAX_COUNT=10000
      - NODE_FUNCTION_ALLOW_EXTERNAL=cheerio
      - N8N_EMAIL_MODE=smtp
      - N8N_SMTP_HOST=
      - N8N_SMTP_PORT=
      - N8N_SMTP_USER=
      - N8N_SMTP_PASS=
      - N8N_SMTP_SENDER=${SSL_EMAIL}
      - N8N_SMTP_SSL=false
      - N8N_CONCURRENCY_PRODUCTION_LIMIT=20
    links:
      - postgres
      - redis
      - caddy
    ports:
      - 5678:5678
    volumes:
      - n8n_storage:/home/node/.n8n
      - ${DATA_FOLDER}/local_files:/files
    depends_on:
      redis:
        condition: service_healthy
      postgres:
        condition: service_healthy

  postgres:
    image: postgres:16
    restart: always
    environment:
      - POSTGRES_USER
      - POSTGRES_PASSWORD
      - POSTGRES_DB
      - POSTGRES_NON_ROOT_USER
      - POSTGRES_NON_ROOT_PASSWORD
    volumes:
      - db_storage:/var/lib/postgresql/data
      - ./init-data.sh:/docker-entrypoint-initdb.d/init-data.sh
    healthcheck:
      test: ['CMD-SHELL', 'pg_isready -h localhost -U ${POSTGRES_USER} -d ${POSTGRES_DB}']
      interval: 5s
      timeout: 5s
      retries: 10


  redis:
    image: redis:6-alpine
    restart: always
    volumes:
      - redis_storage:/data
    healthcheck:
      test: ['CMD', 'redis-cli', 'ping']
      interval: 5s
      timeout: 5s
      retries: 10


  caddy:
    image: caddy:latest
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - caddy_data:/data
      - ${DATA_FOLDER}/caddy_config:/config
      - ${DATA_FOLDER}/caddy_config/Caddyfile:/etc/caddy/Caddyfile

volumes:
  db_storage:
  redis_storage:
  n8n_storage:
    external: true
  caddy_data:
    external: true
```

Plik **.env**

```
POSTGRES_USER=root_user_name
POSTGRES_PASSWORD=StrongPassword123!@@@
POSTGRES_DB=n8n

POSTGRES_NON_ROOT_USER=non_root_user_name
POSTGRES_NON_ROOT_PASSWORD=SuperTajneHaslo123@@@

ENCRYPTION_KEY=SOME_RANDOM_STRING


# Replace <directory-path> with the path where you created folders earlier
DATA_FOLDER=/home/$USER/n8n

# The top level domain to serve from, this should be the same as the subdomain you created above
DOMAIN_NAME=YourDomainName 

# The subdomain to serve from
SUBDOMAIN=n8n

# DOMAIN_NAME and SUBDOMAIN combined decide where n8n will be reachable from
# above example would result in: https://n8n.example.com

# Optional timezone to set which gets used by Cron-Node by default
# If not set New York time will be used
GENERIC_TIMEZONE=Europe/Berlin

# The email address to use for the SSL certificate creation
SSL_EMAIL=noreply@your.domain
SSL_EMAIL_PASS=Stron_Password
```

Skrypt inicjujący **init-data.sh**

```
#!/bin/bash
set -e;


if [ -n "${POSTGRES_NON_ROOT_USER:-}" ] && [ -n "${POSTGRES_NON_ROOT_PASSWORD:-}" ]; then
	psql -v ON_ERROR_STOP=1 --username "$POSTGRES_USER" --dbname "$POSTGRES_DB" <<-EOSQL
		CREATE USER ${POSTGRES_NON_ROOT_USER} WITH PASSWORD '${POSTGRES_NON_ROOT_PASSWORD}';
		GRANT ALL PRIVILEGES ON DATABASE ${POSTGRES_DB} TO ${POSTGRES_NON_ROOT_USER};
		GRANT CREATE ON SCHEMA public TO ${POSTGRES_NON_ROOT_USER};
	EOSQL
else
	echo "SETUP INFO: No Environment variables given!"
fi
```