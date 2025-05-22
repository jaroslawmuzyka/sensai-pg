# Logowanie do serwera poprzez SSH

Aby zalogować się do swojego serwera zdalnie musisz skorzystać z SSH. Żeby to zrobić w zależności od systemu operacyjnego masz parę możliwości.

# Logowanie przez komendę ssh

## MacOS

MacOS ma wbudowany terminal z obsługą SSH. Aby zalogować się do serwera:

1.  Otwórz Terminal (znajdziesz go w Applications > Utilities lub użyj Spotlight)
2.  Wpisz polecenie: `ssh użytkownik@adres_serwera`
3.  Przy pierwszym połączeniu system poprosi o potwierdzenie certyfikatu - wpisz "yes"
4.  Wprowadź hasło gdy zostaniesz o nie poproszony

Możesz również użyć parametrów:

- Port niestandardowy: `ssh -p 2222 użytkownik@adres_serwera`
- Logowanie z kluczem SSH: `ssh -i /ścieżka/do/klucza użytkownik@adres_serwera`

## Windows

Aby zalogować się do serwera SSH w systemie Windows:

1.  Użyj wbudowanego klienta OpenSSH (Windows 10+):
    - Otwórz PowerShell lub Command Prompt
    - Wpisz: `ssh użytkownik@adres_serwera`
2.  Alternatywnie zainstaluj PuTTY:
    - Pobierz z [oficjalnej strony](https://www.putty.org/)
    - Wprowadź adres serwera w polu Host Name
    - Ustaw port (domyślnie 22)
    - Kliknij "Open"
    - Wpisz nazwę użytkownika i hasło
3.  Użyj Windows Terminal (najnowsze wersje Windows):
    - Zainstaluj z Microsoft Store
    - Otwórz i użyj składni: `ssh użytkownik@adres_serwera`

Parametry:

- Port niestandardowy: `ssh -p 2222 użytkownik@adres_serwera`
- Logowanie z kluczem SSH: `ssh -i C:\ścieżka\do\klucza użytkownik@adres_serwera`

## Linux

Logowanie do serwera SSH w systemie Linux:

1.  Otwórz Terminal (CTRL+ALT+T w wielu dystrybucjach)
2.  Wpisz: `ssh użytkownik@adres_serwera`
3.  Przy pierwszym połączeniu potwierdź certyfikat wpisując "yes"
4.  Wprowadź hasło

Parametry:

- Port niestandardowy: `ssh -p 2222 użytkownik@adres_serwera`
- Logowanie z kluczem: `ssh -i /ścieżka/do/klucza użytkownik@adres_serwera`
- Zapisywanie sesji: `ssh -v użytkownik@adres_serwera` (tryb verbose)
- Przekierowanie portów: `ssh -L 8080:localhost:80 użytkownik@adres_serwera`

Użyteczne aliasy można dodać do ~/.bashrc lub ~/.zshrc:

```bash
alias serwer='ssh użytkownik@adres_serwera'
```

## Rozwiązywanie problemów z połączeniem SSH

### Typowe problemy

1.  Odmowa połączenia
    - Sprawdź poprawność adresu serwera i portu
    - Upewnij się, że usługa SSH działa na serwerze
    - Sprawdź czy firewall nie blokuje portu SSH
2.  Problemy z autoryzacją
    - Zweryfikuj poprawność nazwy użytkownika
    - Sprawdź uprawnienia pliku klucza: `chmod 600 ~/.ssh/id_rsa`
    - Plik known_hosts może wymagać aktualizacji: `ssh-keygen -R adres_serwera`
3.  Timeouty
    - Dodaj parametr `-v` dla szczegółowych logów: `ssh -v użytkownik@adres_serwera`
    - Sprawdź stabilność sieci
    - Użyj opcji Keep-Alive: `ssh -o ServerAliveInterval=60 użytkownik@adres_serwera`
4.  Problemy z kluczami
    - Upewnij się, że klucz publiczny jest w `~/.ssh/authorized_keys` na serwerze
    - Sprawdź format klucza (OpenSSH vs PuTTY)
    - Zweryfikuj hasło klucza prywatnego

### Polecenia diagnostyczne

```bash
ssh -v użytkownik@adres_serwera  # Tryb verbose
ssh -vvv użytkownik@adres_serwera  # Bardzo szczegółowy debugging
```

## Dobre praktyki bezpieczeństwa SSH

- Używaj kluczy SSH zamiast haseł - generuj je poleceniem `ssh-keygen -t ed25519`
- Wyłącz logowanie jako root - edytuj `/etc/ssh/sshd_config`, ustaw `PermitRootLogin no`
- Zmień domyślny port SSH z 22 na nieużywany powyżej 1024
- Włącz uwierzytelnianie dwuskładnikowe
- Ustaw limity czasowe sesji - dodaj `ClientAliveInterval 300` i `ClientAliveCountMax 0`
- Ogranicz dostęp do określonych użytkowników przez `AllowUsers twój_użytkownik`
- Używaj zapory sieciowej (iptables/ufw)
- Regularnie aktualizuj zarówno klienta jak i serwer SSH
- Monitoruj logi pod kątem nieudanych prób logowania
- Rozważ fail2ban do automatycznej blokady po nieudanych próbach

# Instrukcja generowania i logowania przez klucze SSH

## macOS i Linux

### 1\. Generowanie pary kluczy

```bash
ssh-keygen -t ed25519 -C "twój_komentarz_np_twoj_adres_email"
```

- Przy pytaniu o lokalizację można zaakceptować domyślną (`~/.ssh/id_ed25519`)
- Opcjonalnie ustaw hasło dla dodatkowego zabezpieczenia

### 2\. Dodawanie klucza na serwer

Automatycznie:

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub użytkownik@serwer
```

Ręcznie:

- Wyświetl klucz publiczny:
    
    ```bash
    cat ~/.ssh/id_ed25519.pub
    ```
    
- Skopiuj wyświetloną zawartość
- Zaloguj się na serwer i dodaj do pliku `~/.ssh/authorized_keys`:
    
    ```bash
    mkdir -p ~/.sshchmod 700 ~/.sshecho "skopiowany_klucz_publiczny" >> ~/.ssh/authorized_keyschmod 600 ~/.ssh/authorized_keys
    ```
    

### 3\. Konfiguracja ssh-agent

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### 4\. Logowanie

```bash
ssh użytkownik@serwer
```

## Windows 10+

### 1\. Instalacja OpenSSH (jeśli nie jest zainstalowany)

- Otwórz Ustawienia → Aplikacje → Funkcje opcjonalne
- Sprawdź czy zainstalowany jest "Klient OpenSSH"
- Jeśli nie, kliknij "Dodaj funkcję" i wybierz "Klient OpenSSH"

### 2\. Generowanie pary kluczy

- Otwórz PowerShell jako administrator
- Wpisz:
    
    ```powershell
    ssh-keygen -t ed25519 -C "twój_komentarz"
    ```
    
- Domyślna lokalizacja: `C:\Users\TwójUżytkownik\.ssh\id_ed25519`

### 3\. Dodawanie klucza na serwer

Ręcznie:

- Wyświetl klucz publiczny:
    
    ```powershell
    type $env:USERPROFILE\.ssh\id_ed25519.pub
    ```
    
- Skopiuj wyświetloną zawartość
- Zaloguj się na serwer i dodaj do pliku `~/.ssh/authorized_keys`

Alternatywnie (z użyciem PowerShell):

```powershell
$publicKey = Get-Content "$env:USERPROFILE\.ssh\id_ed25519.pub"
ssh użytkownik@serwer "mkdir -p ~/.ssh && chmod 700 ~/.ssh && echo '$publicKey' >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys"
```

### 4\. Konfiguracja ssh-agent

- Włącz usługę ssh-agent w PowerShell jako administrator:
    
    ```powershell
    # Ustaw usługę na automatyczne uruchamianieSet-Service -Name ssh-agent -StartupType Automatic# Uruchom usługęStart-Service ssh-agent# Dodaj kluczssh-add $env:USERPROFILE\.ssh\id_ed25519
    ```
    

### 5\. Logowanie

```powershell
ssh użytkownik@serwer
```

## Dodatkowe ustawienia dla wszystkich systemów

### Użycie niestandardowego portu

```bash
ssh -p 2222 użytkownik@serwer
```

### Konfiguracja stałych ustawień w pliku config

Utwórz lub edytuj plik `~/.ssh/config` (Linux/macOS) lub `C:\Users\TwójUżytkownik\.ssh\config` (Windows):

```
Host nazwa_skrócona
    HostName serwer.domena.pl
    User użytkownik
    Port 2222
    IdentityFile ~/.ssh/id_ed25519
```

Potem możesz logować się używając:

```bash
ssh nazwa_skrócona
```