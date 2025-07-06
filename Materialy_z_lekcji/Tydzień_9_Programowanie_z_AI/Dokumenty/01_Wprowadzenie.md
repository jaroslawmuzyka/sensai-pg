# Wprowadzenie do Programowania z AI

> ## “Everyone is a programmer. Now, you just have to say something to the computer.” - Jensen Huang

Podczas tego tygodnia dowiesz się:

*   jak programować korzystając z edytorów kodu jak Cursor, Windsurf i platform typu [Bolt.new](http://bolt.new/), czy Lovable
*   jak wybrać model do kodowania
*   jak pisać dobre prompty
*   jak korzystać z serwerów MCP do programowania
*   jak używać GitHuba
*   jak tworzyć ui, np. jako interfejs do automatyzacji w n8n czy do skryptów python
*   jak wystawić nasz kod do internetu, bezpiecznie wszystko skonfigurować tak żeby nie narazić się na utratę danych czy niespodziewane rachunki
*   jak tworzyć dodatki do przeglądarki

---

## Czemu uczyć się programować?

*   **Niezależność w tworzeniu rozwiązań:** Nie musisz czekać na programistów, aby wdrożyć swoje pomysły.
*   **Bo fajnie jest tworzyć coś swojego:** Satysfakcja z budowania działających aplikacji jest ogromna.
*   **Automatyzacja i oszczędność czasu:** Możesz zautomatyzować powtarzalne zadania i skupić się na strategii.
*   **Konkurencyjność na rynku pracy:** Umiejętność programowania to ogromny atut w każdej dziedzinie, a zwłaszcza w SEO.
*   **Zrozumienie technologii i programistów:** Będziesz w stanie lepiej komunikować się z zespołem deweloperskim i rozumieć ograniczenia techniczne.
*   **Możliwość budowania własnych rozwiązań pod własne potrzeby:** Twórz narzędzia idealnie dopasowane do Twoich potrzeb.
*   **Wykorzystanie z pracy innych i dostosowanie jej pod własne wymagania:** Możesz adaptować istniejące rozwiązania open-source do swoich celów.

Bariery techniczne znikają, co sprawia, że co raz więcej osób zaczyna programować, i że zaczyna liczyć się jeszcze bardziej pomysł. Jak wiadomo od pomysłu do wykonania często długa droga, ale nawet jeśli nie chcemy samemu wdrażać naszych pomysłów to świadomość możliwości jak i ograniczeń technicznych powinna sprawić że nasze pomysły będą jeszcze lepsze, a co za tym idzie zyskujemy przewagę na tym konkurencyjnym rynku jakim jest SEO. Świat zmienia się aktualnie tak szybko że codziennie pojawiają się nowe problemy do rozwiązania. Przedstawię Ci narzędzia i koncepty do realizacji Twoich pomysłów skutecznie i bezpiecznie.

---

## Czym jest programowanie?

**Programowanie to sposób tworzenia instrukcji, które mówią komputerowi, jak rozwiązać konkretny problem — najczęściej prowadząc użytkownika z punktu A do punktu B. Można je porównać do przepisu kulinarnego albo instrukcji dojazdu: zawierają krok po kroku, co ma się wydarzyć.**

![image](image.png)

<details>
<summary>Wizualizacja procesu</summary>

Myślenie o programowaniu jako o procesie pomaga zrozumieć jego logikę. Każdy krok w procesie to fragment kodu, który wykonuje określone zadanie.

![image](image%2010.png)

</details>

### Od No-Code do Kodu

<details>
<summary>N8N</summary>

W trakcie tego kursu zetknęłaś się już z formą programowania – automatyzacjami w **n8n**. Tam, zamiast pisać kod, używamy gotowych modułów, które łączymy graficznie. To podejście jest bardzo wygodne, szczególnie gdy zależy nam na **szybkim wdrożeniu i prostocie**.

</details>

<details>
<summary>Python</summary>

Teraz pójdziemy o krok dalej i zajmiemy się **programowaniem w Pythonie**. To język tekstowy, który daje nam **nieograniczone możliwości**, ale wymaga nieco więcej nauki. Python jest idealny do zadań, które są zbyt złożone dla n8n, na przykład do zaawansowanej analizy danych, uczenia maszynowego czy budowania niestandardowych narzędzi.

![image](image%201.png)

</details>

<details>
<summary>Przykładowy skrypt w Pythonie</summary>

To jest przykład kompletnego skryptu w Pythonie, który pobiera wszystkie linki z mapy strony (sitemap) i zapisuje je do pliku CSV. Nie musisz go teraz w pełni rozumieć — chodzi o to, żeby zobaczyć, jak wygląda kod, który realizuje konkretne zadanie.

```python
import requests
import xml.etree.ElementTree as ET
import csv
from urllib.parse import urljoin, urlparse
import time
from typing import List, Set

class SitemapExtractor:
    def __init__(self, timeout: int = 10):
        """
        Inicjalizuje ekstraktor sitemap
        
        Args:
            timeout: Timeout dla HTTP requestów w sekundach
        """
        self.timeout = timeout
        self.session = requests.Session()
        self.session.headers.update({
            'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36'
        })
    
    def fetch_sitemap(self, url: str) -> str:
        """
        Pobiera zawartość sitemap z podanego URL
        
        Args:
            url: URL do sitemap
            
        Returns:
            Zawartość XML jako string
        """
        try:
            response = self.session.get(url, timeout=self.timeout)
            response.raise_for_status()
            return response.text
        except requests.RequestException as e:
            print(f"Błąd podczas pobierania {url}: {e}")
            return ""
    
    def parse_sitemap_index(self, xml_content: str) -> List[str]:
        """
        Parsuje sitemap index i zwraca listę URL-ów do sub-sitemaps
        
        Args:
            xml_content: Zawartość XML sitemap index
            
        Returns:
            Lista URL-ów do sub-sitemaps
        """
        try:
            root = ET.fromstring(xml_content)
            
            # Sprawdzamy różne namespace'y
            namespaces = {
                'ns': 'http://www.sitemaps.org/schemas/sitemap/0.9'
            }
            
            sitemap_urls = []
            
            # Szukamy elementów sitemap w sitemap index
            for sitemap in root.findall('.//ns:sitemap', namespaces):
                loc = sitemap.find('ns:loc', namespaces)
                if loc is not None and loc.text:
                    sitemap_urls.append(loc.text.strip())
            
            # Fallback - szukamy bez namespace
            if not sitemap_urls:
                for sitemap in root.findall('.//sitemap'):
                    loc = sitemap.find('loc')
                    if loc is not None and loc.text:
                        sitemap_urls.append(loc.text.strip())
            
            return sitemap_urls
            
        except ET.ParseError as e:
            print(f"Błąd parsowania XML sitemap index: {e}")
            return []
    
    def parse_sitemap_urls(self, xml_content: str) -> List[dict]:
        """
        Parsuje sitemap i zwraca listę URL-ów z metadanymi
        
        Args:
            xml_content: Zawartość XML sitemap
            
        Returns:
            Lista słowników z URL-ami i metadanymi
        """
        try:
            root = ET.fromstring(xml_content)
            
            # Sprawdzamy różne namespace'y
            namespaces = {
                'ns': 'http://www.sitemaps.org/schemas/sitemap/0.9'
            }
            
            urls = []
            
            # Szukamy elementów url w sitemap
            for url in root.findall('.//ns:url', namespaces):
                url_data = {}
                
                # Lokalizacja (wymagana)
                loc = url.find('ns:loc', namespaces)
                if loc is not None and loc.text:
                    url_data['loc'] = loc.text.strip()
                
                # Ostatnia modyfikacja (opcjonalna)
                lastmod = url.find('ns:lastmod', namespaces)
                if lastmod is not None and lastmod.text:
                    url_data['lastmod'] = lastmod.text.strip()
                
                # Częstotliwość zmian (opcjonalna)
                changefreq = url.find('ns:changefreq', namespaces)
                if changefreq is not None and changefreq.text:
                    url_data['changefreq'] = changefreq.text.strip()
                
                # Priorytet (opcjonalny)
                priority = url.find('ns:priority', namespaces)
                if priority is not None and priority.text:
                    url_data['priority'] = priority.text.strip()
                
                if 'loc' in url_data:
                    urls.append(url_data)
            
            # Fallback - szukamy bez namespace
            if not urls:
                for url in root.findall('.//url'):
                    url_data = {}
                    
                    loc = url.find('loc')
                    if loc is not None and loc.text:
                        url_data['loc'] = loc.text.strip()
                    
                    lastmod = url.find('lastmod')
                    if lastmod is not None and lastmod.text:
                        url_data['lastmod'] = lastmod.text.strip()
                    
                    changefreq = url.find('changefreq')
                    if changefreq is not None and changefreq.text:
                        url_data['changefreq'] = changefreq.text.strip()
                    
                    priority = url.find('priority')
                    if priority is not None and priority.text:
                        url_data['priority'] = priority.text.strip()
                    
                    if 'loc' in url_data:
                        urls.append(url_data)
            
            return urls
            
        except ET.ParseError as e:
            print(f"Błąd parsowania XML sitemap: {e}")
            return []

    def is_sitemap_index(self, xml_content: str) -> bool:
        """
        Sprawdza czy XML to sitemap index czy zwykły sitemap
        
        Args:
            xml_content: Zawartość XML
            
        Returns:
            True jeśli to sitemap index, False jeśli zwykły sitemap
        """
        try:
            root = ET.fromstring(xml_content)
            
            # Sprawdzamy czy istnieją elementy sitemapindex
            namespaces = {
                'ns': 'http://www.sitemaps.org/schemas/sitemap/0.9'
            }
            
            # Sprawdzamy z namespace
            if root.find('.//ns:sitemapindex', namespaces) is not None:
                return True
            if root.find('.//ns:sitemap', namespaces) is not None:
                return True
            
            # Sprawdzamy bez namespace
            if root.find('.//sitemapindex') is not None:
                return True
            if root.tag == 'sitemapindex' or 'sitemapindex' in root.tag:
                return True
            
            return False
            
        except ET.ParseError:
            return False
    
    def extract_urls_from_domain(self, domain: str) -> List[dict]:
        """
        Wyciąga wszystkie URL-e z sitemap danej domeny
        
        Args:
            domain: Domena (np. 'https://example.com' lub 'https://example.com/')
            
        Returns:
            Lista słowników z URL-ami i metadanymi
        """
        # Normalizujemy domenę
        if not domain.startswith(('http://', 'https://')):
            domain = 'https://' + domain
        
        if not domain.endswith('/'):
            domain += '/'
        
        # Konstruujemy URL do sitemap
        sitemap_url = urljoin(domain, 'sitemap.xml')
        
        print(f"Pobieranie sitemap z: {sitemap_url}")
        
        # Pobieramy główny sitemap
        xml_content = self.fetch_sitemap(sitemap_url)
        if not xml_content:
            return []
        
        all_urls = []
        
        # Sprawdzamy czy to sitemap index
        if self.is_sitemap_index(xml_content):
            print("Wykryto sitemap index, pobieranie sub-sitemaps...")
            
            # Pobieramy URL-e do sub-sitemaps
            sub_sitemap_urls = self.parse_sitemap_index(xml_content)
            print(f"Znaleziono {len(sub_sitemap_urls)} sub-sitemaps")
            
            # Pobieramy każdy sub-sitemap
            for i, sub_url in enumerate(sub_sitemap_urls, 1):
                print(f"Pobieranie sub-sitemap {i}/{len(sub_sitemap_urls)}: {sub_url}")
                
                sub_xml_content = self.fetch_sitemap(sub_url)
                if sub_xml_content:
                    urls = self.parse_sitemap_urls(sub_xml_content)
                    all_urls.extend(urls)
                    print(f"  Znaleziono {len(urls)} URL-ów")
                
                # Mała przerwa między requestami
                time.sleep(0.1)
        
        else:
            print("Wykryto zwykły sitemap, parsowanie URL-ów...")
            # To zwykły sitemap, parsujemy URL-e bezpośrednio
            all_urls = self.parse_sitemap_urls(xml_content)
        
        print(f"Łącznie znaleziono {len(all_urls)} URL-ów")
        return all_urls
    
    def extract_urls_from_sitemap_url(self, sitemap_url: str) -> List[dict]:
        """
        Wyciąga URL-e z konkretnego URL sitemap
        
        Args:
            sitemap_url: Bezpośredni URL do sitemap
            
        Returns:
            Lista słowników z URL-ami i metadanymi
        """
        print(f"Pobieranie sitemap z: {sitemap_url}")
        
        xml_content = self.fetch_sitemap(sitemap_url)
        if not xml_content:
            return []
        
        all_urls = []
        
        if self.is_sitemap_index(xml_content):
            print("Wykryto sitemap index, pobieranie sub-sitemaps...")
            
            sub_sitemap_urls = self.parse_sitemap_index(xml_content)
            print(f"Znaleziono {len(sub_sitemap_urls)} sub-sitemaps")
            
            for i, sub_url in enumerate(sub_sitemap_urls, 1):
                print(f"Pobieranie sub-sitemap {i}/{len(sub_sitemap_urls)}: {sub_url}")
                
                sub_xml_content = self.fetch_sitemap(sub_url)
                if sub_xml_content:
                    urls = self.parse_sitemap_urls(sub_xml_content)
                    all_urls.extend(urls)
                    print(f"  Znaleziono {len(urls)} URL-ów")
                
                time.sleep(0.1)
        else:
            print("Wykryto zwykły sitemap, parsowanie URL-ów...")
            all_urls = self.parse_sitemap_urls(xml_content)
        
        print(f"Łącznie znaleziono {len(all_urls)} URL-ów")
        return all_urls
    
    def save_to_csv(self, urls: List[dict], filename: str = 'sitemap_urls.csv'):
        """
        Zapisuje URL-e do pliku CSV
        
        Args:
            urls: Lista słowników z URL-ami
            filename: Nazwa pliku wyjściowego
        """
        if not urls:
            print("Brak URL-ów do zapisania")
            return
        
        # Zbieramy wszystkie możliwe klucze
        fieldnames = set()
        for url in urls:
            fieldnames.update(url.keys())
        
        fieldnames = sorted(list(fieldnames))
        
        with open(filename, 'w', newline='', encoding='utf-8') as csvfile:
            writer = csv.DictWriter(csvfile, fieldnames=fieldnames)
            writer.writeheader()
            writer.writerows(urls)
        
        print(f"Zapisano {len(urls)} URL-ów do pliku: {filename}")
    
    def save_to_txt(self, urls: List[dict], filename: str = 'sitemap_urls.txt'):
        """
        Zapisuje tylko URL-e do pliku tekstowego (jeden URL na linię)
        
        Args:
            urls: Lista słowników z URL-ami
            filename: Nazwa pliku wyjściowego
        """
        if not urls:
            print("Brak URL-ów do zapisania")
            return
        
        with open(filename, 'w', encoding='utf-8') as f:
            for url_data in urls:
                if 'loc' in url_data:
                    f.write(url_data['loc'] + '\n')
        
        print(f"Zapisano {len(urls)} URL-ów do pliku: {filename}")


def main():
    """
    Funkcja główna - przykład użycia
    """
    # Inicjalizujemy ekstraktor
    extractor = SitemapExtractor(timeout=10)
    
    # Opcja 1: Podaj domenę (automatycznie dodaje /sitemap.xml)
    domain = "https://phu.io.vn/"
    urls = extractor.extract_urls_from_domain(domain)
    
    # Opcja 2: Podaj bezpośredni URL do sitemap
    # sitemap_url = "https://example.com/sitemap.xml"
    # urls = extractor.extract_urls_from_sitemap_url(sitemap_url)
    
    if urls:
        # Zapisujemy wyniki
        extractor.save_to_csv(urls, 'sitemap_urls.csv')
        extractor.save_to_txt(urls, 'sitemap_urls.txt')
        
        # Wyświetlamy przykładowe URL-e
        print(f"\nPrzykładowe URL-e (pierwsze 5):")
        for i, url in enumerate(urls[:5]):
            print(f"{i+1}. {url.get('loc', 'N/A')}")
        
        # Statystyki
        print(f"\nStatystyki:")
        print(f"Łącznie URL-ów: {len(urls)}")
        
        # Sprawdzamy domeny
        domains = set()
        for url in urls:
            if 'loc' in url:
                parsed = urlparse(url['loc'])
                domains.add(parsed.netloc)
        
        print(f"Unikalne domeny: {len(domains)}")
        for domain in sorted(domains):
            print(f"  - {domain}")
    
    else:
        print("Nie znaleziono żadnych URL-ów")


if __name__ == "__main__":
    main()
```