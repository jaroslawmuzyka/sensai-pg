# Bezpieczeństwo

> ## <mark><strong>Security is not a feature, it's a requirement.</strong></mark>

![image](image%206.png)

<details>
<summary>⚠️ ZŁOTA ZASADA</summary>

```markdown
⚠️ ZŁOTA ZASADA: Klucze API to jak hasła!
- NIGDY nie wrzucaj ich do GitHub
- Używaj pliku .env (pokażemy jak)
- Testuj najpierw na małych danych

Przykład co może pójść źle:
- Wrzucisz klucz API na GitHub = ktoś go ukradnie
- Zapętlisz skrypt = 10000 requestów do API = rachunek 💸
```

</details>

---

## Skanery bezpieczeństwa

<details>
<summary>🔍 PIP AUDIT - Skaner bezpieczeństwa bibliotek Pythona</summary>

`pip audit` to narzędzie do skanowania zależności Pythona pod kątem znanych podatności bezpieczeństwa. Jak antywirus, ale dla twoich bibliotek!

**Instalacja:**

```shell
bash
pip install pip-audit
```

**Użycie:**

```shell
bash
# Skanuj obecne środowisko
pip-audit

# Skanuj requirements.txt
pip-audit -r requirements.txt

# Automatyczna naprawa (jeśli możliwa)
pip-audit --fix

# Szczegółowy raport
pip-audit --desc
```

**Przykładowy output:**

```text
Found 2 known vulnerabilities in 2 packages
Name       Version  ID             Fix Versions
---------- -------- -------------- ------------
flask      1.0.2    PYSEC-2019-179 >=1.0.3
requests   2.6.0    PYSEC-2021-101 >=2.26.0
```

</details>

<details>
<summary>🔍 NPM AUDIT - Skaner bezpieczeństwa bibliotek Node</summary>

`npm audit` to wbudowane narzędzie do skanowania zależności Node.js pod kątem znanych podatności bezpieczeństwa. Jak antywirus, ale dla twoich pakietów npm!

**Instalacja:**

```shell
# Wbudowane w npm (6.0+) - nie wymaga instalacji
npm --version
```

**Użycie:**

```shell
# Skanuj projekt
npm audit

# Automatyczna naprawa (jeśli możliwa)
npm audit fix

# Wymuszenie naprawy (może wprowadzić breaking changes)
npm audit fix --force

# Tylko podatności o wysokim/krytycznym poziomie
npm audit --audit-level high

# Format JSON dla dalszego przetwarzania
npm audit --json

# Szczegółowy raport
npm audit --parseable
```

**Kiedy używać npm audit:**

*   **Regularnie:** Co tydzień/miesiąc w aktywnych projektach, przed każdym deploymentem produkcyjnym, po dodaniu nowych zależności.
*   **Natychmiast:** Gdy otrzymasz alert o nowej podatności, przed rozpoczęciem pracy nad starszym projektem, po klonowaniu repozytorium.
*   **W procesie CI/CD:** Dodaj do pipeline'u jako gate przed deploymentem, zautomatyzuj sprawdzanie w pull requestach.
*   **Pilnie:** Gdy twoja aplikacja obsługuje wrażliwe dane, w aplikacjach bankowych/finansowych.

**Przykładowy output:**

```text
# npm audit report

lodash  <=4.17.10
Severity: high
Prototype Pollution - https://npmjs.com/advisories/782
fix available via `npm audit fix`
node_modules/lodash

2 high severity vulnerabilities

To address all issues, run:
  npm audit fix
```

**Bonus:** Dla większych projektów można użyć `yarn audit` (Yarn) lub `pnpm audit` (pnpm) - działają podobnie!

</details>

---

## ✅ Security Rules (wklej to do .cursora)

<details>
<summary>Skopiuj to do cursorrules i waliduj kod przed deployem</summary>

**authentication:**
- ZAWSZE weryfikuj tokeny przed użyciem - nigdy nie ufaj inputowi użytkownika
- NIGDY nie wysyłaj tokenów w URL/query params - używaj Authorization headers
- NIGDY nie loguj pełnych tokenów - maksymalnie pierwsze/ostatnie 4 znaki
- Używaj krótkich czasów wygaśnięcia tokenów (30 min dla access, 7 dni dla refresh)
- Implementuj token rotation i refresh token flow
- Hashuj hasła używając bcrypt/argon2 z odpowiednim salt

**database_security:**
- ZAWSZE używaj Row Level Security (RLS) w Supabase/PostgreSQL
- NIGDY nie używaj service/admin keys w kodzie klienckim
- ZAWSZE używaj parametryzowanych zapytań - nigdy string concatenation
- Szyfruj wrażliwe dane przed zapisem do bazy (PII, tokeny, klucze API)
- Regularnie rotuj klucze dostępowe do bazy danych
- Ogranicz uprawnienia użytkowników bazy do minimum (principle of least privilege)

**input_validation:**
- ZAWSZE waliduj i sanityzuj wszystkie inputy użytkownika
- Sprawdzaj typy danych, długość, format, dozwolone znaki
- Odrzucaj podejrzane wzorce (Path Traversal: ../, SQL: '; DROP TABLE)
- Używaj whitelist zamiast blacklist dla dozwolonych wartości
- Escapuj specjalne znaki przed wyświetleniem (XSS prevention)
- Waliduj zarówno po stronie klienta jak i serwera

**Przykłady:**

```
# Autoryzacja
- |
  // ✅ DOBRZE - z headerem
  fetch('/api/endpoint', {
    headers: { 'Authorization': `Bearer ${token}` }
  })

  // ❌ ŹLE - token w URL
  fetch(`/api/endpoint?token=${token}`)

# Walidacja
- |
  // ✅ DOBRZE - właściwa walidacja
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  if (!emailRegex.test(email)) throw new Error('Invalid email');

  // ❌ ŹLE - brak walidacji
  const email = req.body.email; // używane bez sprawdzenia

# Logowanie
- |
  // ✅ DOBRZE - bez wrażliwych danych
  logger.info(`User ${userId} logged in`);

  // ❌ ŹLE - logowanie tokenów
  logger.info(`Token: ${accessToken}`);

# Błędy
- |
  // ✅ DOBRZE - generyczny błąd
  res.status(500).json({ error: 'Internal server error' });

  // ❌ ŹLE - szczegóły implementacji
  res.status(500).json({ error: err.stack });

# Zapytania DB
- |
  // ✅ DOBRZE - parametryzowane
  db.query('SELECT * FROM users WHERE id = $1', [userId]);

  // ❌ ŹLE - konkatenacja
  db.query(`SELECT * FROM users WHERE id = ${userId}`);
```

**supabase_specific:**
- ZAWSZE włączaj RLS na wszystkich tabelach
- Używaj auth.uid() w politykach RLS
- Preferuj anon key nad service key w aplikacji
- Implementuj polityki dla SELECT, INSERT, UPDATE, DELETE osobno
- Testuj polityki RLS przed deploymentem
- Używaj Supabase Edge Functions dla wrażliwych operacji

**deployment_security:**
- Skanuj dependencies pod kątem vulnerabilities (npm audit)
- Używaj najnowszych wersji bibliotek z patchami bezpieczeństwa
- Implementuj CSP (Content Security Policy) headers
- Używaj HSTS dla wymuszenia HTTPS
- Regularnie przeprowadzaj pentesty
- Monitoruj logi pod kątem anomalii

**monitoring:**
- Loguj wszystkie nieudane próby logowania
- Monitoruj nietypowe wzorce dostępu
- Alertuj przy podejrzanych aktywnościach
- Regularnie przeglądaj logi bezpieczeństwa
- Implementuj audit trail dla krytycznych operacji

**compliance:**
- Przestrzegaj GDPR/RODO dla danych osobowych
- Implementuj right to be forgotten
- Szyfruj dane PII (Personally Identifiable Information)
- Dokumentuj przepływ danych osobowych
- Regularnie audytuj zgodność z przepisami

</details>

---

## KRYTYCZNE - NAPRAW NATYCHMIAST:

<details>
<summary>critical_vulnerabilities</summary>

- Service key używany zamiast anon key w Supabase
- Brak weryfikacji tokenów OAuth przed użyciem
- Brak RLS na tabelach z wrażliwymi danymi
- SQL injection przez konkatenację stringów
- Logowanie haseł, tokenów lub kluczy API
- Hardkodowane klucze API w kodzie klienckim

</details>
