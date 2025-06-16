## Scenariusze n8n

Tutaj znajdziesz gotową listę scenariuszy n8n z opisami i linkami do pobrania. Każdy scenariusz jest powiązany z konkretną lekcją z kursu.

Na podstawie przesłanych dokumentów stworzę tabelę zachowując kolejność lekcji. Oto połączona tabela:

| LEKCJA (nazwa i link do lekcji) | Scenariusz (nazwa i link) | Opis Scenariusza |
|---|---|---|
| [Przegląd dostępnych metod instalacji n8n (01:04)](https://learn.sensai.academy/next/public/lesson/315) | - | - |
| [n8n w wersji cloud (05:09)](https://learn.sensai.academy/next/public/lesson/321) | - | - |
| [Instalacja n8n na własnym komputerze (08:00)](https://learn.sensai.academy/next/public/lesson/317) | [Instrukcja instalacji na localhost](./LOKALNY_LOCALHOST_N8N) | Instrukcja instalacji na localhost |
| [Instalacja n8n na Railway (04:57)](https://learn.sensai.academy/next/public/lesson/318) | - | - |
| [Instalacja n8n na Elestio (08:08)](https://learn.sensai.academy/next/public/lesson/319) | - | - |
| [Instalacja n8n na Hetznerze (lub dowolnym VPS) (40:49)](https://learn.sensai.academy/next/public/lesson/316) | [Instrukcja instalacji na VPS](./INSTALACJA_N8N/VPS_n8n_with_workers) | Instrukcja instalacji na VPS |
| [Przegląd interfejsu n8n i omówienie wyzwalaczy (14:42)](https://learn.sensai.academy/next/public/lesson/320) | - | - |
| [Import i eksport gotowych scenariuszy automatyzacji (04:48)](https://learn.sensai.academy/next/public/lesson/322) | - | - |
| [Wprowadzenie do tworzenia workflow w n8n (21:30)](https://learn.sensai.academy/next/public/lesson/325) | [Proste formularze](./proste_formularze.json) | Scenariusz tworzy prosty formularz do wprowadzania słów kluczowych z walidacją - sprawdza czy wprowadzone słowo nie zawiera przecinka i wyświetla odpowiedni komunikat sukcesu lub błędu |
| [Pobieranie i przetwarzanie danych ze stron internetowych (27:44)](https://learn.sensai.academy/next/public/lesson/310) | [Pobieranie i przetwarzanie danych ze stron internetowych](./pobieranie_i_przetwarzanie_danych_ze_stron_internetowych.json) | Scenariusz pobiera nagłówki (h1-h6) i treść strony internetowej (konwertowaną na Markdown) na podstawie podanego URL i zwraca je w odpowiedzi |
| [Korzystanie z zewnętrznych usług przez API (Perplexity) (17:10)](https://learn.sensai.academy/next/public/lesson/312) | [Korzystanie z zewnętrznych API - Perplexity](./korzystanie_z_zewnetrznych_api_perplexity.json) | Scenariusz integruje się z API Perplexity do przeprowadzania research'u na zadany temat, zwracając szczegółowe informacje wraz z cytowaniami źródeł |
| [Automatyczne odświeżanie tokena API w n8n (Senuto) (10:03)](https://learn.sensai.academy/next/public/lesson/313) | [Automatyczne odświeżanie tokena API - Senuto](./automatyczne_odswiezanie_tokena_api_senuto.json) | Scenariusz automatycznie odświeża token API Senuto co 29 dni, zapisuje go na dysku i udostępnia przez webhook dla innych workflow |
| [Korzystanie z zewnętrznych API - widoczność domeny w Senuto (07:43)](https://learn.sensai.academy/next/public/lesson/314) | [Narzędzie widoczności domeny - Senuto](./tool_senuto_domain_visibility.json) | Scenariusz pobiera dane o widoczności domeny w wynikach wyszukiwania z API Senuto, może być używany jako narzędzie w innych workflow |
| [Połączenie usług Google z n8n (16:09)](https://learn.sensai.academy/next/public/lesson/307) | -  | - |
| [Pobieranie danych z Google Trends (14:13)](https://learn.sensai.academy/next/public/lesson/308) | [Pobieranie danych z Google Trends](./google_pobranie_danych_z_trends.json) | Scenariusz automatycznie pobiera trending keywords z Google Trends dla Polski, przetwarza dane XML i zapisuje je do Google Sheets z harmonogramem co 2 godziny |
| [Eksport tekstu do Google Docs (12:57)](https://learn.sensai.academy/next/public/lesson/309) | [Export HTML do Google Docs](./export_html_do_google_docs.json) | Scenariusz konwertuje treść w formacie Markdown na HTML, a następnie eksportuje ją do nowego dokumentu w Google Docs z automatycznym formatowaniem |
| [Integracja n8n z Wordpressem](https://learn.sensai.academy/next/public/lesson/330) | [Integracja z WordPress](./wordpress_create_post.json) | Scenariusz pobiera dane z Google Sheets, importuje treść z Google Docs, a następnie tworzy nowy wpis w WordPressie i aktualizuje status w arkuszu |
| [Integracja n8n z Wordpressem (cz. 2) - grafika wyróżniająca](https://learn.sensai.academy/next/public/lesson/331) | [WordPress z grafiką wyróżniającą](./wordpress_grafika_wyrozniajaca.json) | Rozszerzony scenariusz WordPress, który dodatkowo generuje grafikę wyróżniającą za pomocą AI (OpenAI DALL-E) i dodaje ją do wpisu |
| [Korzystanie z wektorowej bazy danych w n8n](https://learn.sensai.academy/next/public/lesson/329) | [Qdrant - Drive - Docs](./qdrant_drive_docs.json) | Kompleksowy scenariusz RAG (Retrieval Augmented Generation) - automatycznie indeksuje dokumenty z Google Drive do bazy wektorowej Qdrant i umożliwia zadawanie pytań o zawartość dokumentów |
| [Blok agenta w n8n](https://learn.sensai.academy/next/public/lesson/328) | [Blok agenta](./blok_agenta.json) | Scenariusz demonstruje użycie bloku "AI Agent" w n8n z modelem językowym, pamięcią konwersacji i narzędziem kalkulatora do odpowiedzi na zapytania z czatu |
| [Agent AI korzystający z zewnętrznych API](https://learn.sensai.academy/next/public/lesson/327) | [Agent SEO - MASTER](./agent_seo_master.json) | Zaawansowany agent AI z narzędziami SEO: pobieranie stron, sprawdzanie widoczności domeny i research przez Perplexity. Kompleksowy asystent SEO |
| [Rozmowa ze stroną w n8n (20:02)](https://learn.sensai.academy/next/public/lesson/326) | [Rozmowa ze stroną](./rozmawiaj_ze_strona.json) | Scenariusz umożliwia prowadzenie konwersacji o zawartości stron internetowych - agent pobiera treść strony i odpowiada na pytania na jej podstawie |
| [Łączenie n8n z Telegramem (24:20)](https://learn.sensai.academy/next/public/lesson/324) | [SensaiBot Telegram](./sensai_bot_telegram.json) | Bot Telegram z integracją AI, pamięcią konwersacji, dostępem do bazy wiedzy Qdrant i możliwością pobierania treści stron internetowych |
| [Łączenie n8n ze Slackiem (28:19)](https://learn.sensai.academy/next/public/lesson/323) | [SensaiBot Slack](./sensai_bot_slack.json) | Bot Slack z podobną funkcjonalnością jak wersja Telegram - AI agent z pamięcią, bazą wiedzy i narzędziami do analizy stron i domen |
| [Praca domowa do tygodnia 5 i 6](https://learn.sensai.academy/next/public/lesson/332) | - | - |

Tabela zachowuje kolejność lekcji zgodnie z przesłanymi dokumentami i łączy informacje o scenariuszach z ich opisami.
