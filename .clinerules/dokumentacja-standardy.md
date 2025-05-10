## Brief overview
Ten zestaw wytycznych określa standardy dokumentacji i formatowania treści w repozytorium kursu SEO 3.0. Dokument uzupełnia istniejące reguły, skupiając się na spójności formatowania, jakości dokumentacji i najlepszych praktykach tworzenia treści edukacyjnych.

## Standardy formatowania Markdown
- Używaj nagłówków Markdown (# dla tytułu głównego, ## dla sekcji, ### dla podsekcji) do strukturyzowania dokumentów.
- Stosuj listy wypunktowane (`*` lub `-`) dla elementów nieuporządkowanych i listy numerowane (`1.`, `2.`) dla sekwencji kroków.
- Wyróżniaj ważne pojęcia za pomocą **pogrubienia** lub *kursywy*.
- Kod, nazwy plików, ścieżki i polecenia umieszczaj w pojedynczych backtickach: `kod`.
- Dla bloków kodu używaj potrójnych backticks z określeniem języka (np. ```python).
- Tabele stosuj do prezentacji danych porównawczych lub zestawień.

## Struktura dokumentacji lekcji
- Każda notatka z lekcji powinna zawierać:
  - Nagłówek z numerem i tytułem lekcji
  - Krótkie wprowadzenie (1-2 zdania)
  - Spis treści (dla dłuższych dokumentów)
  - Główną treść podzieloną na logiczne sekcje
  - Podsumowanie lub wnioski
  - Sekcję "Dodatkowe materiały" (jeśli dotyczy)
- Transkrypcje powinny być czytelnie sformatowane, z wyraźnym podziałem na sekcje tematyczne.

## Jakość treści
- Używaj prostego, zrozumiałego języka, unikając żargonu technicznego bez wyjaśnienia.
- Definiuj nowe pojęcia przy ich pierwszym wystąpieniu.
- Stosuj przykłady praktyczne do ilustracji koncepcji teoretycznych.
- Dbaj o poprawność językową i interpunkcyjną.
- Unikaj długich, złożonych zdań - preferuj krótsze, bardziej przejrzyste konstrukcje.

## Linki i odniesienia
- Linki wewnętrzne (do innych plików w repozytorium) zawsze twórz jako ścieżki względne.
- Dla linków zewnętrznych dodawaj krótki opis, czego dotyczy dany zasób.
- Przy odwołaniach do narzędzi lub technologii, linkuj do ich oficjalnej dokumentacji.
- Sprawdzaj aktualność wszystkich linków zewnętrznych przed dodaniem ich do dokumentacji.

## Wizualizacje i media
- Diagramy i schematy twórz w formacie, który można łatwo edytować (np. Mermaid).
- Obrazy umieszczaj w dedykowanym podkatalogu `Obrazy/` w ramach odpowiedniego tygodnia.
- Każdy obraz powinien mieć czytelną nazwę pliku odzwierciedlającą jego zawartość.
- Dodawaj opisy alternatywne do obrazów dla lepszej dostępności.

## Aktualizacja dokumentacji
- Przy aktualizacji treści zawsze dodawaj datę modyfikacji na końcu dokumentu.
- Znaczące zmiany w treści oznaczaj sekcją "Aktualizacje" na początku dokumentu.
- Zachowuj historię zmian w komentarzach commitów Git.
- Przy usuwaniu przestarzałych treści, rozważ przeniesienie ich do sekcji "Archiwum" zamiast całkowitego usunięcia.
