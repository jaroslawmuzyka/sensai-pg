# Instalacja Docker - systemy oparte na Debian

## Zainstaluj używając repozytorium `apt`

Przed pierwszą instalacją Docker Engine na nowej maszynie hosta, musisz skonfigurować repozytorium `apt` dla Dockera. Następnie możesz zainstalować i aktualizować Dockera z tego repozytorium.

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

## Zainstaluj pakiety Dockera

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
# Zarządzaj Dockerem jako użytkownik bez uprawnień roota

# Zarządzaj Dockerem jako użytkownik bez uprawnień rootasud

Demon Docker jest powiązany z gniazdem Unix, a nie portem TCP. Domyślnie użytkownik `root` jest właścicielem gniazda Unix, a inni użytkownicy mogą uzyskać do niego dostęp tylko używając `sudo`. Demon Docker zawsze działa jako użytkownik `root`.

Jeśli nie chcesz poprzedzać polecenia `docker` słowem `sudo`, utwórz grupę Unix o nazwie `docker` i dodaj do niej użytkowników. Gdy demon Docker uruchamia się, tworzy gniazdo Unix dostępne dla członków grupy `docker`. W niektórych dystrybucjach Linux system automatycznie tworzy tę grupę podczas instalacji Docker Engine za pomocą menedżera pakietów. W takim przypadku nie musisz ręcznie tworzyć grupy.

:::danger
**OSTRZEŻENIE**

Grupa `docker` przyznaje uprawnienia poziomu root użytkownikowi. Szczegóły dotyczące wpływu na bezpieczeństwo systemu znajdziesz w sekcji Docker Daemon Attack Surface.
:::

:::info
**Uwaga** Aby uruchomić Docker bez uprawnień roota, zobacz Uruchamianie demona Docker jako użytkownik bez uprawnień roota ([Tryb Rootless](https://docs.docker.com/engine/security/rootless/) \*źródło z oficjalnej dokumentacji Dockera).
:::

**Aby utworzyć grupę** `docker` **i dodać swojego użytkownika:**

Utwórz grupę `docker` , najprawdopodobniej już istnieje.

```console
sudo groupadd docker
```

Dodaj swojego użytkownika do grupy `docker`.

```console
sudo usermod -aG docker $USER
```

Wyloguj się i zaloguj ponownie, aby członkostwo w grupie zostało ponownie ocenione. Jeśli używasz Linuxa w maszynie wirtualnej, może być konieczne ponowne uruchomienie maszyny wirtualnej, aby zmiany weszły w życie. Możesz również uruchomić następujące polecenie, aby aktywować zmiany w grupach:

```console
newgrp docker
```

4.  Sprawdź, czy możesz uruchamiać polecenia `docker` bez `sudo`.

```bash
docker ps


CONTAINER ID   IMAGE                    COMMAND                  CREATED       STATUS                 PORTS                                                                                         NAMES
71b8a82ddcfc   docmost/docmost:latest   "docker-entrypoint.s…"   2 hours ago   Up 2 hours             3000/tcp                                                                                      docmost-docmost-1
cd1b537fe23d   caddy:2-alpine           "caddy run --config …"   2 hours ago   Up 2 hours             0.0.0.0:80->80/tcp, :::80->80/tcp, 0.0.0.0:443->443/tcp, :::443->443/tcp, 443/udp, 2019/tcp   docmost-caddy-1
42b7419acd3c   redis:7.2-alpine         "docker-entrypoint.s…"   2 hours ago   Up 2 hours             6379/tcp                                                                                      docmost-redis-1
6201f01700d3   postgres:16-alpine       "docker-entrypoint.s…"   2 hours ago   Up 2 hours             5432/tcp                                                                                      docmost-db-1
b068c85ee882   containrrr/watchtower    "/watchtower --sched…"   2 hours ago   Up 2 hours (healthy)   8080/tcp                                                                                      docmost-watchover-1
```