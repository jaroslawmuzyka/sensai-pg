# Docker Compose

Docker Compose to narzędzie do definiowania i uruchamiania aplikacji wielokontenerowych. Jest kluczem do usprawnienia procesu rozwoju i wdrażania.

Compose upraszcza kontrolę nad całym stosem aplikacji, ułatwiając zarządzanie usługami, sieciami i woluminami w jednym pliku konfiguracyjnym YAML. Następnie za pomocą jednego polecenia tworzysz i uruchamiasz wszystkie usługi z pliku konfiguracyjnego.

Compose działa we wszystkich środowiskach: produkcyjnym, stagingowym, deweloperskim, testowym, a także w przepływach pracy CI. Posiada również polecenia do zarządzania całym cyklem życia aplikacji:

- Uruchamianie, zatrzymywanie i przebudowywanie usług
- Przeglądanie statusu działających usług
- Strumieniowanie logów z działających usług
- Uruchamianie jednorazowych poleceń w usłudze

## Instalacja Docker Compose

Zaktualizuj indeks pakietów i zainstaluj najnowszą wersję Docker Compose

```bash
sudo apt-get update
sudo apt-get install docker-compose-plugin
```

Sprawdź, czy Docker Compose jest poprawnie zainstalowany, sprawdzając wersję.

```bash
docker compose version
```

## Aktualizacja Docker Compose

Aby zaktualizować wtyczkę Docker Compose, wykonaj następujące polecenia:

```bash
sudo apt-get update
sudo apt-get install docker-compose-plugin
```