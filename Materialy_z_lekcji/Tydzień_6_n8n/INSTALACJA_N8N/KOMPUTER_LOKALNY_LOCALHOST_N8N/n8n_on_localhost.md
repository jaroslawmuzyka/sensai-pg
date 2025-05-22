# Instalacja na localhost

Utwórz katalog w którym będziesz przechowywać konfigurację Docker (np. Dokumenty > Docker > n8n-localhost)

Utwórz wolumen w Docker

```bash
docker volume create n8n_storage
```

Utwórz plik .env i wgraj jego zawartość

Utwórz plik docker-compose.yml i wgraj jego zawartość

Utwórz katalog files. Będzie to katalog do korzystania z lokalnych plików w n8n.


### Uruchomienie kontenerów

```bash
docker compose up -d
```

Pierwsze uruchomienie może trwać dłużej, ponieważ Docker musi pobrać wszystkie obrazy.