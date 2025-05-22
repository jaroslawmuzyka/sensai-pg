# Podstawowe komendy Linux

## Nawigacja

`pwd` - wyświetla bieżący katalog

`ls` - lista plików i katalogów (`ls -la` dla szczegółów)

`cd [katalog]` - zmiana katalogu

`cd ..` - przejście do katalogu nadrzędnego

`cd ~` - przejście do katalogu domowego

`cd -` - powrót do poprzedniego katalogu

## Zarządzanie plikami

`touch [plik]` - tworzy pusty plik

`mkdir [katalog]` - tworzy katalog

`mkdir -p [ścieżka]` - tworzy całą strukturę katalogów

`cp [źródło] [cel]` - kopiuje pliki/katalogi

`cp -r [źródło] [cel]` - kopiuje katalogi rekurencyjnie

`mv [źródło] [cel]` - przenosi/zmienia nazwę

`rm [plik]` - usuwa plik (`rm -r` dla katalogów)

`rm -rf [katalog]` - usuwa katalog bez pytania (ostrożnie!)

## Wyświetlanie zawartości

`cat [plik]` - wyświetla całą zawartość

`less [plik]` - wyświetla zawartość z przewijaniem

`head/tail [plik]` - pokazuje początek/koniec pliku

`head -n [liczba] [plik]` - pokazuje pierwsze \[liczba\] linii

`tail -n [liczba] [plik]` - pokazuje ostatnie \[liczba\] linii

`tail -f [plik]` - śledzi na żywo zmiany w pliku

`more [plik]` - pokazuje zawartość strona po stronie

## Wyszukiwanie

`find [ścieżka] -name "[wzorzec]"` - szuka plików

`find [ścieżka] -type f -size +100M` - szuka plików większych niż 100MB

`grep [wzorzec] [plik]` - szuka tekstu w pliku

`grep -r "[wzorzec]" [katalog]` - szuka rekurencyjnie w katalogu

`locate [nazwa]` - szybkie wyszukiwanie plików (wymaga updatedb)

## Zarządzanie pakietami

`apt update` - aktualizacja listy pakietów (Debian/Ubuntu)

`apt upgrade` - aktualizacja zainstalowanych pakietów

`apt install [pakiet]` - instalacja pakietu (Debian/Ubuntu)

`apt remove [pakiet]` - usunięcie pakietu

`apt-get install [pakiet]` - starsze Debian/Ubuntu

`dnf install [pakiet]` - Fedora/RHEL 8+

`yum install [pakiet]` - CentOS/RHEL 7

`rpm -i [plik.rpm]` - instalacja z pliku RPM

`dpkg -i [plik.deb]` - instalacja z pliku DEB

`pacman -S [pakiet]` - Arch Linux

`zypper install [pakiet]` - openSUSE

## Użytkownicy i grupy

`useradd [nazwa]` - tworzy użytkownika

`userdel [nazwa]` - usuwa użytkownika

`usermod [opcje] [nazwa]` - modyfikuje użytkownika

`passwd [nazwa]` - zmienia hasło użytkownika

`groupadd [nazwa]` - tworzy grupę

`groupdel [nazwa]` - usuwa grupę

`groups [użytkownik]` - pokazuje grupy użytkownika

`id [użytkownik]` - informacje o użytkowniku/grupach

## Edytory tekstu

`vi/vim [plik]` - zaawansowany edytor (tryby: Insert-i, Command-Esc, :wq - zapisz i wyjdź, :q! - wyjdź bez zapisu)

`nano [plik]` - prosty edytor (^O - zapisz, ^X - wyjdź)

`emacs [plik]` - zaawansowany edytor (C-x C-s - zapisz, C-x C-c - wyjdź)

## Uprawnienia

`chmod [uprawnienia] [plik]` - zmienia uprawnienia

`chmod +x [plik]` - nadaje uprawnienia do wykonywania

`chown [użytkownik]:[grupa] [plik]` - zmienia właściciela

`sudo [komenda]` - wykonuje komendę jako administrator

`su - [użytkownik]` - przełącza na innego użytkownika

`sudo -s` - uruchamia powłokę jako root

## System

`ps` - lista procesów (`ps aux` dla wszystkich)

`kill [PID]` - kończy proces

`killall [nazwa]` - kończy wszystkie procesy o nazwie

`top/htop` - monitorowanie zasobów systemu

`free -h` - pokazuje wykorzystanie pamięci

`df -h` - pokazuje wykorzystanie dysków

`du -sh [katalog]` - pokazuje rozmiar katalogu

`reboot` - uruchamia ponownie system

`shutdown -h now` - wyłącza system natychmiast

`history` - pokazuje historię wykonanych komend

## Kompresja i archiwizacja

`tar -czvf [archiwum.tar.gz] [pliki/katalogi]` - tworzy archiwum

`tar -xzvf [archiwum.tar.gz]` - rozpakowuje archiwum

`zip -r [archiwum.zip] [pliki/katalogi]` - tworzy archiwum ZIP

`unzip [archiwum.zip]` - rozpakowuje archiwum ZIP

## Sieć

`ping [host]` - sprawdza połączenie

`ifconfig/ip a` - konfiguracja interfejsów sieciowych

`ip r` - pokazuje tablicę routingu

`ss -tuln` - pokazuje otwarte porty

`netstat -tuln` - pokazuje otwarte porty (starsze systemy)

`wget [URL]` - pobiera plik z internetu

`curl [URL]` - pobiera plik lub wyświetla zawartość strony

`ssh [użytkownik]@[host]` - zdalne połączenie

`scp [plik] [użytkownik]@[host]:[ścieżka]` - kopiuje pliki przez SSH

`sftp [użytkownik]@[host]` - transfer plików przez SSH

## Sterowanie przepływem

`|` (pipe) - przekierowuje wyjście jednej komendy na wejście drugiej

`>` - przekierowuje wyjście do pliku (nadpisuje)

`>>` - dopisuje wyjście do pliku

`<` - przekierowuje zawartość pliku na wejście komendy

`&&` - wykonuje następną komendę tylko gdy poprzednia się powiedzie

`||` - wykonuje następną komendę tylko gdy poprzednia się nie powiedzie

`;` - wykonuje komendy sekwencyjnie

## Uzyskanie pomocy

`man [komenda]` - wyświetla instrukcję (manual)

`info [komenda]` - wyświetla dokumentację info

`[komenda] --help` - pokazuje opcje komendy

`whatis [komenda]` - krótki opis komendy

`apropos [słowo kluczowe]` - szuka komend według słowa kluczowego

## Zmienne systemowe

`echo $PATH` - wyświetla zmienną PATH

`export VAR=wartość` - ustawia zmienną środowiskową

`printenv` - wyświetla wszystkie zmienne środowiskowe

## Zapora sieciowa (Firewall)

### Debian/Ubuntu

`ufw status` - sprawdza status zapory

`sudo ufw enable/disable` - włącza/wyłącza zaporę

`sudo ufw allow [port/usługa]` - zezwala na ruch na danym porcie

`sudo ufw deny [port/usługa]` - blokuje ruch na danym porcie

`sudo ufw delete [reguła]` - usuwa regułę

`sudo ufw app list` - wyświetla dostępne profile aplikacji

`sudo ufw allow from [ip-address]` - zezwala na ruch z danego adresu IP

`sudo ufw status numbered` - pokazuje numerowane reguły

### Fedora/RHEL:

`firewall-cmd --state` - sprawdza status zapory

`firewall-cmd --add-port=[port]/tcp` - otwiera port TCP

`firewall-cmd --reload` - przeładowuje konfigurację