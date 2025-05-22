# Utworzenie użytkownika (Debian / Ubuntu)

Po zalogowaniu się na serwerze na konto root przystąp do stworzenie użytkownika. Działanie poprzez użytkownika ma za zadanie zwiększyć bezpieczeństwo na twoim serwerze.

## Zaloguj się do swojego VPS

Zaloguj się do swojego VPS

```shell
ssh root@your_server_ip_address
```

Jeżeli to Twoje pierwsze logowanie, to musisz po zalogowaniu się ustawić nowe hasło dla użytkownika root. **Zapisz nowo utworzone hasło, ponieważ nie będzie można go zmienić!**

## Utworzenie użytkownika

Użyj komendy `adduser`, aby dodać nowego użytkownika do systemu:

```bash
user
```

Komenda poprosi o:

1.  Hasło
2.  Pełne imię i nazwisko
3.  Numer pokoju
4.  Telefon służbowy
5.  Telefon domowy
6.  Inne informacje

Tylko hasło jest wymagane; pozostałe pola można pominąć naciskając Enter.

## Dodawanie użytkownika do grupy **sudo**

Aby utworzyć użytkownika z uprawnieniami administracyjnymi, dodaj go do grupy sudo:

```bash
usermod -aG sudo nazwa_użytkownika
```

## Testowanie użytkownika z dostępem do `sudo`

Aby sprawdzić, czy nowe uprawnienia `sudo` działają, najpierw użyj komendy `su`, żeby przełączyć się na nowe konto użytkownika:

```bash
su nazwa_uzytkownika
```

Jako nowy użytkownik, sprawdź czy możesz korzystać z `sudo` dodając przedrostek `sudo` do komendy, którą chcesz uruchomić z uprawnieniami superużytkownika:

```bash
sudo komenda_do_uruchomienia
```

Przykładowo, możesz wyświetlić zawartość katalogu `/root`, który normalnie jest dostępny tylko dla użytkownika root:

```bash
sudo ls -la /root
```

Przy pierwszym użyciu `sudo` w sesji, zostaniesz poproszony o hasło dla konta tego użytkownika. Wprowadź hasło, aby kontynuować:

```bash
Output:
[sudo] password for nazwa_uzytkownika:
```

:::warning
**Uwaga:** Nie jest to prośba o hasło **root**! Wprowadź hasło użytkownika z uprawnieniami sudo, którego właśnie utworzyłeś. Jeśli twój użytkownik jest w odpowiedniej grupie i podałeś poprawne hasło, komenda wydana z `sudo` zostanie uruchomiona z uprawnieniami **root**.
:::

## Logowanie do serwera jako użytkownik

Teraz możesz wylogować się ze swojego serwera. Żeby to zrobić wywołaj dwa razy komendę `exit` . Potem żeby zalogować się do serwera wydaj komendę:

```bash
ssh nazwa_uzytkownika@adres_ip_serwera
```

Logujesz się wprowadzając swoje hasło użytkownika.