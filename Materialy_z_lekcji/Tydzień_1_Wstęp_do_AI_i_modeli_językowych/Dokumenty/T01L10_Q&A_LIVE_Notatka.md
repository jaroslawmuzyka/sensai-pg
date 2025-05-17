### Pytania i odpowiedzi ze spotkania live

**Pytanie:** Czy DeepSeek (narzędzie zgłoszone przez Pawła Cengla) będzie omawiany w kursie?

**Odpowiedź:**
*DeepSeek nie był pierwotnie planowany w kursie, ale skoro pojawiła się taka potrzeba, będzie o nim mowa.*

---

**Pytanie:** Czy Manus, nowy agent do tworzenia aplikacji/stron, zostanie pokazany?

**Odpowiedź:**
*Tak, zostanie pokazany Manus i być może zostanie wygenerowane coś prostego w ramach ćwiczenia na live.*

---

**Pytanie:** Ile osób jest zapisanych na obecną edycję kursu?

**Odpowiedź:**
*Jest 200 nowych osób i 160 z poprzedniego kursu, łącznie 360 osób.*

---

**Pytanie:** Jak osoby, które brały udział w poprzednim kursie, powinny podchodzić do materiałów, które mogły się powtórzyć?

**Odpowiedź:**
*Osoby, które już były na kursie, mogą pomijać oczywiste dla nich treści. W każdym tygodniu jest sporo nowych rzeczy, więc można podchodzić selektywnie do materiałów.*

---

**Pytanie:** Jak pracować z repozytorium GitHub udostępnionym w ramach kursu?

**Odpowiedź:**
*Repozytorium na GitHub zawiera wszystkie materiały kursowe (kod, notatki, transkrypcje, prompty, narzędzia, datasety). Można z nim pracować przez przeglądarkę lub rekomendowane narzędzia typu IDE (np. Cursor, Cline, Windsurf).*
* * **Cursor:** Aby załadować repozytorium do Cursora, należy go zainstalować, kliknąć "New Window", "klon repo" i wkleić URL repozytorium.*
* * **Custom Rules:** W repozytorium znajdują się pliki "cursor rules" (repo rule dla mentorów i zasady użytkownika). Zasady użytkownika załadowane jako kontekst w czacie Cursora pozwalają rozmawiać z repozytorium i pytać o jego zawartość (np. jakie zagadnienia są w danym tygodniu, co znajduje się w folderach).*
* * **Struktura repozytorium:***
    * * **Datasety:** Pliki z danymi do ćwiczeń.*
    * * **Materiały z lekcji:** Foldery dla każdego tygodnia zawierające dokumenty, transkrypcje (w plikach `.md`).*
    * * **Plik readme:** Zawiera wszystkie notatki do każdej lekcji, linki, materiały dodatkowe.*
    * * **Prompty:** Wszystkie prompty używane w kursie w formie tabeli.*
    * * **Narzędzia:** Opis narzędzi używanych w kursie (który tydzień, do czego służy).*
    * * **Notatniki Colab:** Linki i opisy notatników Google Colab.*
    * * **Linki do notatek:** Centralny plik z linkami do notatek i transkrypcji ze wszystkich lekcji.*
* * **Inne interfejsy:** Planowane jest udostępnienie innych interfejsów czatowych (np. na Dify, Telegram), aby ułatwić komunikację z repozytorium bez narzędzi programistycznych.*

---

**Pytanie:** Co zrobić, jeśli ktoś nie ma dostępu do repozytorium GitHub?

**Odpowiedź:**
*Należy zgłosić się do Mateusza Wyszogrodzkiego.*

---

**Pytanie:** Jak uzyskać dostęp do repozytorium na GitHub?

**Odpowiedź:**
*Na platformie kursu, w dwóch pierwszych lekcjach wprowadzających, znajduje się formularz do uzupełnienia nicku na GitHubie. Po jego wypełnieniu otrzymuje się automatyczne zaproszenie do repozytorium.*

---

**Pytanie:** W materiałach na GitHubie zdublowały się foldery tygodnia 5 i 6. Czy zostaną usunięte?

**Odpowiedź:**
*Tak, zostaną usunięte, aby uporządkować materiały.*

---

**Pytanie:** Jakie są wrażenia z korzystania z DeepSeek?

**Odpowiedź:**
*DeepSeek to chińska produkcja. Na arenach ma wysoką pozycję (7-8 miejsce). Stosuje architekturę mixture of experts (zestaw ekspertów do różnych zadań), co było innowacyjne. Planowana jest druga wersja modelu reasoningowego.*
* * **Plusy:***
    * * Cennik – modele są tańsze niż konkurencyjne.*
    * * Możliwe generowanie kontentu (przykład strony Armia Art, gdzie wygenerowano dużo treści).*
    * * Możliwe, że zawiera elementy języka polskiego w korpusie treningowym.*
    * * Tańsze wnioskowanie (reasoning) niż u konkurencji.*
* * **Minusy:***
    * * Czat jest bardzo "goły", ma mało funkcji w porównaniu do konkurencji.*
    * * Brak funkcjonalności typu GPTs czy inne historie.*
    * * Funkcja search/źródła podawane przez DeepSeek często są nieaktualne lub zerwane (bzdury).*
    * * Modele topowe konkurencji (Gemini Flash 2.5, GPT-4) są obecnie lepsze.*
    * * Był skandal związany z trenowaniem DeepSeek na danych z OpenAI.*
* * **Podsumowanie:** Obecnie DeepSeek R1 jest w tyle za konkurencją. Warto czekać na wersję drugą, jeśli przyniesie rewolucyjne zmiany.*

---

**Pytanie:** Czy program Cursor (i jego alternatywy) jest konieczny do kursu? Co zmienia?

**Odpowiedź:**
*Nie jest konieczny.*
* * **Co zmienia:***
    * * Ułatwia przyswajanie materiałów z repozytorium GitHub, pozwalając "rozmawiać" z materiałami (przeszukanie, zadawanie pytań o zawartość).*
    * * W tygodniu 9 (programowanie z AI) Cursor będzie istotnym narzędziem.*
    * * Jest to narzędzie typu IDE do programowania, ale można go używać też do innych celów (pisanie artykułów, edytor tekstowy z funkcjami AI).*
    * * Obsługuje standard MCP, pozwalając na komunikację z innymi narzędziami i modelami językowymi.*
* * **Alternatywy:** Cline (darmowy), Windsurf.*
* * **Dostęp do repozytorium bez tych narzędzi:** Można korzystać z repozytorium przez przeglądarkę GitHub. Planowane są inne interfejsy czatowe do komunikacji z repozytorium.*

---

**Pytanie:** Czy planowane jest wcześniejsze udostępnianie materiałów na platformie kursu niż w poniedziałki?

**Odpowiedź:**
*Plan jest taki, aby materiały były udostępniane wcześniej, prawdopodobnie w niedzielę. Trwają prace nad nagrywaniem materiałów stosownie wcześniej.*

---

**Pytanie:** Czy płatne narzędzia są niezbędne w czasie kursu? Czy wystarczy dostęp do płatnego ChatGPT (z dostępem do API)?

**Odpowiedź:**
*Na obecnym etapie płatny ChatGPT jest wystarczający do funkcji chatowych. W kolejnych tygodniach być może będzie potrzebne minimalne wykupienie tokenów OpenAI do pracy po API oraz niewielkie koszty związane z serwerami/VPS (np. ok. 20 zł miesięcznie).*
* * **Ogólna zasada:** Każde pokazane narzędzie/model ma wersję darmową, open source lub tanie zastosowanie.*
*Przygotowane zostanie zestawienie potrzebnego oprogramowania i szacowanych kosztów.*

---

**Pytanie:** Jak dodać na LinkedIn informację o udziale w kursie/projekcie SensAI Akademii? Jest jakiś szablon?

**Odpowiedź:**
*Tak, jest narzędzie (baner), które pobiera zdjęcie profilowe i dodaje banner SensAI. Link i instrukcja zostaną podane.*

---

**Pytanie:** Czy i jak często trzeba aktualizować biblioteki wykorzystywane w aplikacjach webowych utworzonych w Manusie, w kontekście zabezpieczenia przed wirusami?

**Odpowiedź:**
*To dobre pytanie, temat będzie szerzej poruszany w tygodniu o programowaniu. Najlepszą praktyką jest, aby Manus/inne narzędzie wykonało pierwsze zadanie, a następnie zsynchronizować projekt z GitHubem lub pobrać go lokalnie. Aktualizacje i dalsze prace powinny odbywać się lokalnie (np. w Cursorze). Nie wiadomo, jak często Manus operuje na nowych wersjach bibliotek. Generalnie aktualizacje nie odbywają się bardzo często.*

---

**Pytanie:** Jeśli Cursor działa poprawnie, czy GitHub mimo wszystko jest konieczny? Czy Cursor wystarczy na potrzeby kursu?

**Odpowiedź:**
*GitHub to nie program, lecz repozytorium kodu. Jeśli programujesz z AI, GitHub jest bardzo polecany, ponieważ AI może generować błędy i repozytorium pozwala łatwo cofnąć się do wcześniejszej wersji kodu. W kontekście kursu GitHub to platforma do przechowywania materiałów, a Cursor to narzędzie na komputerze, które łączy się z tym repozytorium. Bez repozytorium kodu (jak GitHub) programowanie z AI może być problematyczne.*

---

**Pytanie:** Jeśli dane z GitHuba zostaną zaciągnięte do Cursora, czy nowe materiały dodane na GitHuba pobiorą się automatycznie do Cursora, czy trzeba odświeżać?

**Odpowiedź:**
*Nie pobierają się automatycznie. Należy ręcznie zainicjować pobranie najnowszych zmian. Można to zrobić w terminalu Cursora komendą `git pull origin main`. Zaleca się robić to raz w tygodniu po udostępnieniu materiałów.*

---

**Pytanie:** Jak wysterować LLM, aby generował treści w określonym przedziale długości (np. 6000 znaków)?

**Odpowiedź:**
*LLM-y mają trudność w precyzyjnym szacowaniu długości.*
* * **Metody:***
    * * **Sterowanie przez outline:** Poprosić LLM o stworzenie outline'u o określonej liczbie sekcji (np. "tak długi, jak potrzeba i tak krótki, jak to możliwe"). Długość tekstu jest bardziej przewidywalna dla każdej sekcji.*
    * * **Opisowe określenie długości:** W prompcie określić długość tekstu opisowo (np. "krótki" = 300-500 wyrazów) na etapie generowania outline'u.*
    * * **Liczba nagłówków:** Sterowanie liczbą nagłówków w tekście, ponieważ ilość tekstu generowana na nagłówek jest w miarę przewidywalna.*
    * * **Fine-tuning modelu:** Wytrenowanie modelu na datasetach tekstów o pożądanej długości. Jest to bardziej zaawansowane, wymaga danych treningowych i serwera z GPU.*

---

**Pytanie:** W raporcie e-commerce pojawiła się teza, że opisy kategorii w przedziale ~6000 znaków mają pozytywny wpływ na widoczność, ale dłuższe teksty mogą powodować spadek. Jak to rozumieć? Czy długość to czynnik rankingowy?

**Odpowiedź:**
*Długość tekstu nie jest bezpośrednim czynnikiem rankingowym. Wydaje się, że dłuższy tekst (do pewnego momentu) ma większą "pojemność" na słowa kluczowe, co może zwiększać prawdopodobieństwo pojawienia się na więcej fraz (np. z długiego ogona). Gdy tekst jest zbyt długi (np. powyżej 6000 znaków w tym badaniu), Google może zacząć traktować stronę jako coś innego niż kategoria produktowa, zmieniając intencję strony, co może prowadzić do spadków. Punkt 6000 znaków to wynik statystyczny z konkretnego badania (na 90 tys. stron) i nie jest uniwersalną zasadą. Optymalna długość może się różnić w zależności od tematyki sklepu i struktury kategorii.*

---

**Pytanie:** Czy obecny proces generowania treści (trzy etapy: Perplexity, humanizacja, formatowanie) został zastąpiony wytrenowanym modelem robiącym wszystko naraz? Jak pozyskać dane do trenowania takiego modelu?

**Odpowiedź:**
*Tak, stosujemy wytrenowany model (np. Gemma 3.27b) do humanizacji tekstów.*
* * **Cel humanizacji:** LLM-y mają tendencję do nadużywania pewnych zwrotów i konstrukcji (np. podwójny myślnik, specyficzne pary słów), co sprawia, że tekst jest wykrywany jako generowany przez AI. Humanizacja polega na nauczeniu modelu, aby nie nadużywał tych pojęć i używał słownictwa bardziej charakterystycznego dla tekstów pisanych przez człowieka.*
* * **Pozyskanie danych do fine-tuningu:***
    * * Pobrać duży dataset tekstów pisanych przez człowieka (np. z Hugging Face, 50 tys. tekstów).*
    * * Używać AI, aby przepisało te teksty (np. "weź ten tekst i przepisz go zachowując sens, ale używając innych słów"). Powstaje dataset tekstów "AI-owych" opartych na ludzkich.*
    * * Przygotować dane do fine-tuningu w formie par prompt-response, gdzie prompt to prośba o przepisanie tekstu, a response to tekst ludzki (ten oryginalny). Na przykład: "przepisz ten tekst [tekst AI] na taki styl [tekst ludzki]".*
    * * Wytrenować model (np. Gemma 3.27b) na tych danych. Wymaga serwera z GPU (np. wynajęcie maszyny na 12h, H100).*
    * * Po wytrenowaniu, model przepisując teksty generowane przez LLM-y, będzie bazował na datasetcie ludzkich tekstów i unikał "AI-owego" słownictwa.*
*Temat jest zaawansowany i będzie szerzej omawiany w przyszłości.*

---

**Pytanie:** Czy w tym kursie będzie omawiane zaawansowane temat fine-tuningu?

**Odpowiedź:**
*Fine-tuning został usunięty z obecnej edycji kursu. Mateusz może udostępnić lekcję z poprzedniego kursu na ten temat. Możliwe, że pod koniec kursu pojawią się dodatkowe materiały (lekcja, spis wniosków) na temat humanizacji przez fine-tuning.*

---

**Pytanie:** Czy w ramach tygodnia o automatyzacji i blogowaniu dowiemy się, jak uruchomić tę funkcjonalność od A do Z i dostaniemy gotowe workflow na Make lub Zapier (Siemen)?

**Odpowiedź:**
*Tak, w dedykowanym tygodniu wszystkie gotowe workflow i instrukcje zostaną przedstawione.*

---

**Pytanie:** Czy replit.com to narzędzie, którym warto się pochylić w ramach narzędzi AI?

**Odpowiedź:**
*Replit jest wart uwagi, ponieważ oferuje od razu hostowanie aplikacji. Jednak Cursor czy Lovable mogą być lepszymi narzędziami. Replit wydaje się promować jako narzędzie dla osób niezwiązanych z technologią.*

---

**Pytanie:** Czy za pomocą AI można stworzyć rozwiązanie dla małego e-commerce typu pop-up "zostaw swój numer a oddzwonimy za 5 minut"?

**Odpowiedź:**
*Tak, to bardzo proste zadanie, które można zrealizować za pomocą narzędzii AI. Nauczenie się narzędzia pozwoli zrobić to w około 30 minut (plus czas na poprawki).*

---

**Pytanie:** Make kontra Dify - różnice, podobieństwa, zastosowanie.

**Odpowiedź:**
*Będzie o tym oddzielna lekcja.*
* * **Ogólnie:** Make ma szersze zastosowanie i pozwala zautomatyzować wszystko. Dify jest bardziej ograniczony, ale do współpracy z modelami językowymi jest dużo lepszy niż Make.*

---

**Pytanie:** Czy warto przesiąść się na Gemini 2.5, jeśli jest się przyzwyczajonym do OpenAI? Dlaczego tak lub nie?

**Odpowiedź:**
*Tak, warto rozważyć przesiadkę.*
* * **Powody "Tak":***
    * * Gemini 2.5 (zwłaszcza Flash) jest istotnie tańszy (Milion tokenów we Flashu kosztuje 15 centów).*
    * * Gemini 2.5 Pro jest znacznie lepszy do programowania niż modele OpenAI.*
    * * Jeśli korzysta się z pakietu Google WorkSpace (premium), Opti Advance (na bazie modeli Google) jest często wliczony w cenę.*
* * **Ogólna uwaga:** Nie warto przyzwyczajać się do jednego modelu. Rynek dynamicznie się zmienia, modele wyprzedzają się co tydzień. Należy stworzyć środowisko i mindset pozwalające na szybkie przełączanie między modelami (np. w 5 minut), aby model nie ograniczał i nie przyzwyczajał.*

---

**Pytanie:** Jakie narzędzia AI (oprócz omawianych w 1. tygodniu) warto poznać w kontekście efektywności?

**Odpowiedź:**
* * **Super Whisper:** Narzędzie do komunikacji głosowej z komputerem, wykorzystujące model Whisper. Pozwala tworzyć prompt template dla różnych aplikacji (np. dyktowanie notatek do Obsidiana w odpowiednim formacie, dyktowanie maili).*
* * **Spark Mail / Superhuman:** Klienci poczty z funkcjami AI.*
* * **Make:** Tworzenie agentów do automatyzacji codziennych zadań (np. wysyłanie planu dnia na podstawie kalendarza i Notion, wybieranie zadań przez model reasoningowy).*
* * **IDE (Cursor):** Centralne narzędzie do pracy z kodem i modelami.*
* * **API:** Komunikacja z modelami głównie przez API zamiast interfejsów chatowych.*
* * **Lovable, V0:** Narzędzia (omawiane w osobnym tygodniu).*
* * **Notebook LM:** Narzędzie do pracy z dokumentami (lekcja w 1. tygodniu). Obsługuje język polski (aktualizacja od czasu nagrania lekcji).*

---

**Pytanie:** Czy w ramach strategii SEO na przykładzie Dr. Max umieszczanie linków w stopce (do listingów kategorii produktów) daje lepsze pozycje, czy tylko indeksowanie?

**Odpowiedź:**
*Bez szczegółowej analizy projektu trudno jednoznacznie stwierdzić.*
* * **Możliwe cele i efekty:***
    * * **Trendy:** Reagowanie na pojawiające się trendy (np. link do kategorii "opalanie kremy FF do twarzy" w stopce).*
    * * **Nowości:** Promowanie nowych kategorii (np. "mleko dla niemowląt").*
    * * **Duże wolumeny:** Kierowanie ruchu do kategorii z dużym potencjałem fraz (np. "probiotyki", "magnezy").*
    * * **Indeksacja:** Zwiększenie indeksacji stron kategorii poprzez linkowanie wewnętrzne.*
    * * **Pozycje:** Choć może nie daje ogromnego wzrostu pozycji, może pozytywnie wpływać na indeksację, co pośrednio wpływa na widoczność.*
*Przy dużych e-commerce takie działania mogą mieć kilka znaczeń jednocześnie.*

---

**Pytanie:** Czy bardzo spadają CTR-y (współczynniki klikalności) po wdrożeniu AI Overview w wynikach wyszukiwania? Czy badacie to?

**Odpowiedź:**
*Tak, badamy. Na podstawie polskich danych obserwuje się spadki CTR-ów rzędu 30-35%. Jest to zbieżne z badaniami (np. Ahre, który podał 37%).*

---

**Pytanie:** AI Overview Google. Które serwisy/intencje wyszukiwania powinny walczyć o widoczność w tych blokach?

**Odpowiedź:**
*Nie tylko intencje informacyjne. AI Overviews pojawiają się również dla innych intencji. Prawdopodobnie za chwilę pojawią się dla produktów, pytań o produkty, a nawet z reklamami. Wszyscy będą o to walczyć. W Polsce AI Overview pojawia się dla bardzo dużej części fraz. Obserwuje się, że wchodzą też frazy, które wcześniej nie były typowo "jak, gdzie, kiedy". Google intensywnie testuje i rozwija tę funkcjonalność.*

---

**Pytanie:** Czy są jakieś warte uwagi modele z poluzowaną cenzurą, które generują treści (np. erotyka)?

**Odpowiedź:**
*Modele od Mistrala (open source) mają poluzowaną cenzurę.*

---

**Pytanie:** Czy budowanie grafu wiedzy na bazie wektorów/RACa umiera na rzecz pozyskiwania danych z user generated content (np. Reddit) w USA? Czy to kierunek dla Polski (np. Wykop)?

**Odpowiedź:**
*Dyskusja klasy filozoficznej.*
* * **Kontekst USA:** W USA Google bardzo promuje Reddita w wynikach wyszukiwania (około 7% wyników). Wynika to częściowo ze specyficznych zachowań amerykańskich użytkowników, którzy preferują strony z szybkim przekazem informacji i korzystają z platform typu Reddit, Yelp, Pinterest do wyszukiwania informacji. Google prawdopodobnie płaci Redditowi za dane, co napędza widoczność Reddita. Dodatkowo, Reddit może być nowym źródłem danych dla Google do trenowania modeli AI, ponieważ internet jest "zaśmiecony" tekstami generowanymi przez AI.*
* * **Kontekst Polski:** W Polsce Reddit nie jest popularny. Choć Wykop czy inne fora są źródłem user generated content, logika działania wyszukiwarek się nie zmienia – Google wciąż przetwarza ciągi znaków niezależnie od źródła, ekstrakując dane do grafów wiedzy i informacji.*
* * **Zmiana w SEO:** Klasyczne SEO, jak je rozumiemy z ostatnich 5 lat, prawdopodobnie czeka znacząca zmiana. Zasady ekonomii wejdą w grę – sens będzie miało SEO, które będzie realizowane tanio. Jeśli koszty operacyjne nie zostaną istotnie zmniejszone, przy potencjalnie mniejszym ruchu z organicznych wyników, klasyczne metody mogą przestać być opłacalne.*
*Pozyskiwanie danych z niszowych źródeł (jak Reddit dla specyficznych tematów) jest nadal cenne do dokładnego pokrycia intencji użytkownika, tak jak w Polsce analizuje się fora czy grupy. To samo robi się na Reddicie.*

---

**Pytanie:** Czy macie jakieś doświadczenie z Apple Intelligence? Czy warto używać?

**Odpowiedź:**
*Brak doświadczenia. Według opinii jest to "kawał gówna" i jeszcze nie działa poprawnie.*

---

**Pytanie:** Czy polecacie Malediwy?

**Odpowiedź:**
*Tak, fajne miejsce. Długa podróż, stała temperatura (30 stopni woda, powietrze, basen). Inny świat. Warto odwiedzić raz na 15 lat.*

---

**Pytanie:** Jakie narzędzie polecacie do badania obecności strony w wyszukiwarkach (Graph, AI Assistant), np. na polskim rynku?

**Odpowiedź:**
*Na polskim rynku narzędzie nazywa się Chatbot (chyba od Brand24). Potrafi rozpoznawać obecność strony w chatbotach (LLMach). Pojawiły się też narzędzia do skrapowania danych z chatów przez API (np. w Breakdance - do potwierdzenia). W planach jest wdrożenie narzędzia, które będzie badać obecność w Perplexity, ChatGPT, Cloder, DeepSeek, Copilot.*

---

**Pytanie:** Kiedy warto kupować linki nofollow z serwisów typu radio (mocne domeny)? Kiedy nie warto przestawać (z aplikników)?

**Odpowiedź:**
*(Pytanie pozostawione do odpowiedzi na Discordzie ze względu na brak czasu i odejście pytającego).*

---

**Pytanie:** Czy są jeszcze jakieś pytania?

**Odpowiedź:**
*Brak dalszych pytań od uczestników.*