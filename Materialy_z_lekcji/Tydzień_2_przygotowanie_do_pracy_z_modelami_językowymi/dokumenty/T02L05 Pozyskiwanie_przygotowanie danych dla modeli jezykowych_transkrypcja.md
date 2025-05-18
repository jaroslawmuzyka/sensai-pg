Cześć.

W tej lekcji zajmiemy się przygotowaniem i pozyskaniem danych dla modeli językowych.

Z kolejnych lekcji i tygodni dowiesz się, że jest to bardzo kluczowy proces w ramach pracy z modelami językowymi, ponieważ zazwyczaj jak korzystamy z modeli językowych przez API czy używając jakichś różnych automatyzacji, będziemy mieli taką potrzebę, żeby dostarczyć modelowi dane albo w jakiś sposób je przed dostarczeniem przetworzyć.

Więc ta lekcja ma właśnie na celu, żeby Cię do tego przygotować i pokazać Ci, jakie są, yy, tego powody i jakie są metody, żeby to-- tego dokonać.

Zacznijmy od tego, czego się w tej lekcji nauczysz.

Po pierwsze przejdę-- powiem Ci, dlaczego w ogóle modele potrzebują danych od nas, skąd je pozyskać i w jakiej formie należy je do modelu dostarczyć, bo to jest kluczowe.

Ok, zacznijmy od tego, dlaczego musimy dostarczyć w ogóle dane dla modelu językowego.

Dlaczego nie możemy po prostu korzystać ze swoich danych, które ma w danych treningowych i korzystać ze swojej wiedzy, którą nabył w ramach treningu?

Ponieważ modele językowe mają ograniczoną wiedzę i ona-- to wynika z tego, że są one trenowane na danych dostępnych do określonego momentu w czasie.

I jak sobie wejdziesz na stronę modeli językowych różnego rodzaju, na przykład na usługę AI Gemini i AI Studio od Google, to jest tam napisane na przykład knowledge cut off i jest na przykład October 2024.

I jest to właśnie informacja, że ten model językowy był trenowany na danych do momentu, yy, października dwa tysiące dwadzieścia cztery.

No i nie będzie miał wiedzy na temat jakichś aktualnych wydarzeń czy aktualnych zdarzeń, jeżeli mu ich po prostu nie dostarczysz, albo na przykład nie skorzysta on z jakichś dostępnych narzędzi, które ma, na przykład wyszukiwania w Google czy wyszukiwania w Bingu.

Dlatego to jest ważne, z tego powodu.

Model, on sam sobie nie zaktualizuje wiedzy.

Czyli na przykład, jeżeli korzystasz z czatu GPT i na przykład dasz mu jakąś informację, to on nie, nie zaktualizuje swojego wewnętrznego umysłu.

Najczęściej po prostu trenuje się model, wypuszcza i trenuje się kolejny, który ma trochę więcej już wiedzy aktualnej.

No i nie mają dostępnych informacji, które pojawiły się po okresie danym treningowym.

No i bez zewnętrznych dra-- danych nie mogą odpowiadać na aktualne wydarzenia.

Właśnie to wynika, właśnie wszystko, te trzy punkty wynikają z tego, że po prostu model ma jakoś odcięcie wiedzy.

Dalej kontekst is king.

To jest bardzo ważne, ponieważ model wymaga odpowiednich danych kontekstowych, by dostarczać bardzo trafne odpowiedzi do zadanych pytań.

O co chodzi?

Generalnie, jeżeli mamy na przykład jakieś konkretne zadanie, które ma jakieś konkretnych danych, to zazwyczaj model odpowie na to zadanie, ale jego jakość odpowiedzi nie będzie jakoś szczególnie dla Ciebie satysfakcjonująca.

I to jest właśnie to, z czym się wiele osób po prostu boryka, bo korzysta z czatu GPT, nie dostarczając żadnych danych i próbuje wykonywać takie operacje, na przykład jak wygenerowanie nagłówków i tak dalej, i tak dalej.

Generalnie modele nie były do tego celu jakoś szczególnie trenowane, więc bez naszych danych, bez naszej pomocy one po prostu sobie z tym średnio poradzą.

I aktualne dane pozwalają też, yy, odpowiadać modelowi na aktualne informacje, ponieważ to nie jest tak, że model nie może o aktualnych informacjach powiedzieć.

Może oczywiście, jeżeli wie, że to jest jakaś aktualna informacja i ma na jej temat jakieś dokładne dane.

I to, co zawsze mówię i powtarzam na każdej swojej w zasadzie prezentacji, że jak chcemy osiągać szczególnie dobre efekty we współpracy z modelami językowymi, to nie powinniśmy ich traktować jako źródło informacji, a procesor informacji.

Co to znaczy?

Generalnie nie polegaj na tym, co model wie, czego się nauczył w ramach treningu, tylko na tym, co mu dostarczysz.

I każdy nasz proces i każda nasza automatyzacja powinna rozbijać problem, który ma, yy, rozwiązać model na jak najmniejsze kawałki.

I każdy z tych kawałków pewnie zawiera jakieś dane, które należy mu dostarczyć i na bazie tych danych on ma pracować.

Na niczym więcej.

No i skąd takie dane można pozyskać?

Po pierwsze web scraping i będzie na ten temat oddzielna lekcja, więc dowiesz się, jak kraulować serwisy internetowe, żeby pozyskiwać dla siebie szczególnie istotne informacje.

Zewnętrzne serwisy API.

Możemy po prostu skorzystać z jakiegoś zewnętrznego API, które zawiera jakieś dane, które są dla nas akurat przydatne.

Na przykład, nie wiem, API z wynikami meczów i wtedy model, pomimo że nie wie, że jakiś mecz się odbył, to może napisać z niego relację, bo będzie miał wszystkie dane od nas dostarczone.

No i pliki lokalne, czyli to, co jesteśmy w stanie po prostu modelowi przesłać i w jakiej formie dostarczyć dane do modelu, bo to jest ostatni krok i też bardzo ważny, model może przyjąć dane jako zwykły tekst i generalnie jest to w miarę okej metoda, to znaczy, że wyślemy po prostu plain tekst i ma sobie model z tym poradzić, natomiast nie jest najbardziej optymalną.

JSON -- modele sobie dobrze radzą z formatem JSON.

Jeżeli dostaniemy jakiś format JSON z jakiegoś API, to możemy bezpośrednio przesłać go do modelu.

No i model sobie z tym poradzi.

Natomiast to, co jest tutaj istotne, to że model JSON, że model danych JSON zawiera też dodatkowe znaczniki, które też pobierają tokeny, więc jak wysyłamy jakiś duży JSON, który ma dużo nazw swoich cech albo nazw, powiedzmy elementów czy nawiasów klamrowych i tak dalej, i tak dalej, no to też płacimy za to.

Więc jeżeli chcemy optymalizować kosztowo, to JSON może nie być najlepszym wyborem.

CSV to też inaczej, powiedzmy, tekstowy format, natomiast też sobie modele z tym dobrze radzą.

XML — i on jest też bardzo czytelny dla modeli językowych, tylko właśnie znaczniki XML też pobierają tokeny, więc to jest kosztowne.

I taki mod-- powiedzmy format, który najczęściej stosujemy, to jest format Markdown, czyli taki oczyszczony tekst, który bardzo dobrze modele, eee, modele przyswajają i w ogóle producenci modeli językowych też zalecają, żeby w takim formacie przesyłać dane.

W ramach tego kursu zazwyczaj będziemy się posługiwać tylko tekstem zwykłym, JSON-em i Markdownem, bo to są najczęstsze typy danych, które wysyłamy do modelu językowego i najczęściej po prostu takich potrzebujemy.

To tyle z części teoretycznej.

Teraz przejdziemy do praktyki.

I tutaj też, jak w poprzednich lekcjach, przygotowałem specjalny Google Colab, który ma za zadanie wyjaśnić te wszystkie zagadnienia.

I tak jak zazwyczaj, przypominam o tym, żeby przed zaczęciem pracy z tym modelem, przed zaczęciem pracy z tym notatnikiem skopiować go, bo, yhm, inaczej nie będziesz mógł-mogła go edytować.

Yy, tutaj w pierwszym kroku konfigurujemy nasze klucze API.Yyy, z poprzednich lekcji wiesz, jak to zrobić, więc tutaj będziemy używać klucza Open AI, Gina, Open Router i Serpdata.

Serpdata to będzie służyć do pobierania wyników wyszukiwania z Google'u.

To jest usługa Senuto.

Dostaniesz do niej odpowiedni rabat, więc, yyy, więc będziesz, yyy, będzie można ją wykorzystywać.

Ok.

I tutaj, tak jak w prezentacji pokazywałem, dlaczego potrzebujemy danych zewnętrznych i jakie są ograniczenia modeli językowych.

No i teraz robimy taki prompt do modelu językowego, w którym pytamy, jaka jest stopa bezrobocia w Polsce.

No i wiemy, że model GPT4o ma knowledge cutoff na poziomie chyba 2024 roku.

Już dokładnie, dokładnie tego nie pamiętam, natomiast można to sprawdzić na stronie OpenAI.

No i wysyłamy taki prompt.

I tutaj jak jest bezrobocie w Polsce?

I tak jak widać model odpowiedział: "Na koniec września dwa tysiące dwadzieścia trzy roku stopa bezrobocia w Polsce wyniosła pięć procent".

No zapewne, jak zadajesz takie pytanie, to nie interesuje Cię, jaka stopa była bezrobocia praktycznie dwa lata temu.

I tak właśnie model jest ograniczony swoimi danymi.

Nie skorzystaliśmy tu z żadnych narzędzi, nie dostarczyliśmy mu żadnych danych, więc z tego powodu po prostu odpowiedział na to pytanie błędnie.

To znaczy nie błędnie, ponieważ wtedy taka stopa bezrobocia w Polsce była.

Natomiast nie interesuje nas takie pytanie i jak dojdziemy sobie do tego, żeby wskazać mu, jak powinien na to pytanie odpowiedzieć?

Po pierwsze musimy dostarczyć, musimy skądś pobrać te informacje.

I tutaj w naszych automatyzacjach, w naszych procesach i w ogóle w SEO najczęściej posługujemy się tym, co znajdziemy w wynikach wyszukiwania.

Zakładamy, że Google jest świetnym źródłem informacji na każdy temat i tutaj wykorzystamy API wyników wyszukiwania z serpdata.io.

Jak wspomniałem, to jest usługa Senuto, więc dostaniesz do niej dostęp i jakiś rabat, który pozwoli Ci bezpłatnie z niej korzystać w ramach kursu.

I tu pobieramy wyniki wyszukiwania, które występują na słowo kluczowe "Ile wynosi bezrobocie w Polsce" dla języka polskiego.

Pobieramy dziesięć wyników z wyników wyszukiwania.

Mamy tutaj wylistowane top dziesięć wyników wyszukiwania dla zapytania jakie wynosi, ile wynosi bezrobocie w Polsce.

I teraz musimy pobrać z tych stron treści, ponieważ te treści zawierają informacje.

Oczywiście mógłbym ten proces inaczej zaprojektować.

Być może występują te informacje już w snipecie FAQ z Google'a.

To API też zwraca snippet FAQ, więc stamtąd możesz te dane wyekstraktować i dostarczyć jako kontekst do modelu.

Niekoniecznie trzeba tutaj korzystać akurat z pełnych tekstów ze stron.

Tu wykorzystujemy narzędzie Jina, które służy do pobierania treści ze stron do formatu Markdown.

I tak jak sobie powiedzieliśmy, to jest taki format, który model językowy świetnie sobie z nim radzi.

Więc teraz przetworzymy trzy pierwsze adresy URL z tej listy tutaj i pobierzemy z nich treści.

OK, pobieramy sobie treści z tych adresów URL i można domniemać, że w tych treściach zawarta jest odpowiedź na nasze pytanie, które zadaliśmy modelowi językowemu.

Więc będziemy mogli dalej przejść do przetwarzania tych informacji.

OK, mamy tutaj już zapisane te treści i możemy przejść do dalszego przetwarzania.

Najczęściej, tak jak powiedziałem, zazwyczaj w procesach LLMowych staramy się rozbić problem na jak najmniejszej-- jak najwięcej małych kroków.

No i tutaj musimy jeszcze, zanim wyślemy do modelu językowego całe trzy teksty z danego, powiedzmy, całe trzy teksty z tych trzech URL-i, no to warto byłoby jeszcze w jakiś sposób przetworzyć.

Zazwyczaj takich operacji będziemy dokonywać wiele, czyli na przykład, nie wiem, przetwarzamy jakiś dataset, żeby model sobie z nim lepiej radził.

Załóżmy, mamy jakąś wewnętrzną bazę wiedzy, tak?

Mamy jakieś dokumenty firmowe, one zawierają jakieś informacje, no to moglibyśmy przetworzyć je na format Q&A.

Wtedy model będzie sobie z nimi lepiej radził i na przykład będziemy wtedy bardziej precyzyjnie odpowiadać na pytania.

Tutaj akurat wyślemy do modelu te wszystkie teksty i poprosimy go, żeby on wyekstraktował z tych tekstów tylko fakty.

Czyli dostaniemy listę faktów, czyli jakichś liczb, cyfr i faktów, które są na temat bezrobocia w Polsce, bo to są artykuły na ten temat, więc wywołamy ten skrypt i powinniśmy dodać, dostać listę faktów.

Tutaj wykorzystujemy GPT4o mini.

Możesz wykorzystać GPT4one mini i wszystkie takie małe modele językowe, ponieważ one są po prostu bardzo tanie, a zazwyczaj do takich ekstrakcji wystarczy taki model, który jest po prostu mały, bo nie potrzebujemy żadnych szczególnych zasobów i żadnych dużych modeli językowych, bo to jest proste zadanie do wykonania.

OK i mamy listę naszych faktów wyekstraktowaną przez model GPT4o mini z tekstów, które zostały tutaj dostarczone i mamy ją zapisaną w ramach dataframe'u.

OK i teraz jak, yy, wyślemy to samo zapytanie ponownie i zadamy to samo pytanie, ale załączymy te wszystkie fakty, które wygenerowaliśmy do promptu jako kontekst, czyli powiemy modelowi, że kontekst fakty wyekstrowane, wyekstraktowane z różnych źródeł i tutaj dostanie on fakty, które wcześniej wyświetliliśmy i on powinien teraz być w stanie odpowiedzieć na to pytanie dokładniej.

Tutaj mamy te fakty, które do niego wysłaliśmy, a tu jest odpowiedź modelu.

Bezrobocie w Polsce w końcu stycznia dwa tysiące dwadzieścia pięć wynosi pięć przecinek cztery procent, a liczba bezrobotnych to osiemset pięćdziesiąt pięć osób, pięćdziesiąt pięć tysięcy osób.

No i mamy już jakąś bardziej aktualną informację.

Możemy jeszcze zawęzić to pytanie.

Jakie jest bezrobocie w Polsce w maju, maju-- w kwietniu dwa tysiące dwadzieścia pięć?

I znowu on skorzysta z tych samych faktów.

I teraz co mamy?

W kwietniu dwa tysiące dwadzieścia pięć stopa bezrobocia w Polsce wynosiła dwa tysiące, pięć przecinek cztery procent.

Sprawdzimy jeszcze to, czy to się zgadza w wyszukiwarce.

No jest dwa tysiące dwadzieścia pięć, stopa bezrobocia pięć cztery proce.

W ten sposób dostarczając kontekst do modelu językowego.Daliśmy mu informację, taką, której użył do tego, żeby odpowiedzieć na aktualne wydarzenie.

Tak samo mógłbym go zapytać o wczorajszy mecz Ligi Mistrzów, dostarczyć mu wynik i on prawdopodobnie byłby w stanie właśnie dzięki temu odpowiedzieć na to pytanie.

Okej, i teraz kolejny temat w kontekście pozyskiwania danych dla modeli językowych to jest format danych.

Dlaczego akurat przesyłamy mu markdown, a nie HTML, który być może wydaje się takim standardowym?

Jak crawlujemy strony, dostajemy HTML, prawda?

No, wynika to z dwóch powodów.

Po pierwsze, HTML zje nam znacznie więcej tokenów, po drugie wprowadza pewien szum do promptu.

Czyli te znaczniki HTML mogą powodować, że model może dokonać jakiegoś złego wyboru po prostu lub źle zrozumieć pytanie.

Więc tutaj w tej komórce pobierzemy treści ze strony senseai.kademy i przeliczymy, ile by nas kosztowało przetworzenie tego zapytania, przy założeniu, że tysiąc tokenów kosztuje dwadzieścia centów.

I teraz Gina Reader pobierze ten sam tekst w Markdownie i ten sam tekst cały HTML.

I tak jak widzisz liczba tokenów na surowy HTML to jest pięćdziesiąt trzy tysiące tokenów, a liczba dla Markdowna to jest dwadzieścia tysięcy tokenów.

Więc jeżeli byśmy chcieli przetworzyć ten surowy HTML, zapłacilibyśmy takiemu modelu, który tyle kosztuje — dziesięć dolarów, a w Markdownie cztery dolary, więc Markdown jest sześćdziesiąt procent tańszy w tym konkretnym przypadku.

To też zależy od tego, ile tak naprawdę tych znaczników HTML jest na stronie, więc bardzo warto używać Markdowna i we wszystkich automatyzacjach i naszych pracach będziemy korzystać właśnie z Markdowna.

I to tyle z tej części praktycznej.

Jeżeli chodzi o jeszcze pozyskiwanie danych do modeli językowych, to polecam Ci dwa takie serwisy, które pomogą Ci pobrać różnego rodzaju dane.

Jednym jest RapidAPI.

To jest taki hub dla API.

To znaczy, że tu jest tysiące API różnych, które na przykład są w stanie, nie wiem, pobierać dane z Linkedina.

Dane na przykład o wynikach meczu, na przykład scores sports api na przykład.

I tutaj mogę właśnie zamiast pobierać wyniki top dziesięć Google'a, to mogę na przykład wysłać żądanie do tego API i pobrać na przykład aktualne wyniki, czy na przykład zaplanowane wydarzenia.

I wtedy mogę do modelu językowego wysłać informację, jakie są wydarzenia w tym tygodniu i on nam dostarczy mu kontekst i on może napisać nawet artykuł o tym, co w tym tygodniu planowanego jest w Warszawie.

To, co dają te serwisy, to jest to, że standaryzują zapytanie do API.

To znaczy, że wystarczy-- API działa zawsze tak samo, wystarczy, że zmienimy endpoint.

Więc jeżeli nauczysz-- jeżeli wdrożysz RapidAPI, to już dowolne API, a jest ich tu tysiące, będziesz mógł je, mogła wykorzystywać dowolnie.

I kolejnym takim serwisem jest Apify, czyli też taki agregator API, z którego możemy korzystać w taki sam dokładnie sposób, jak z RapidAPI.

Te narzędzia i ten notatnik, który pokazywałem, jest w materiałach dodatkowych na GitHubie.

Zachęcam cię, żebyś przeszedł, przeszła ten notatnik samodzielnie jeszcze, przeklikując się przez wszystkie te komórki.

No i skorzystaj z tych danych, żeby uruchomić jakiś swój projekt.

W tej lekcji to wszystko.

Zapraszam ciebie do kolejnej.

