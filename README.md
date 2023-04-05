# Mechanical Scraper
Mechanical Scraper - Easy to Web Scraping

## Generating Code for HTTP Request
![image](https://user-images.githubusercontent.com/63570918/229982297-97abb684-30d2-4a05-98bf-a09ce3d28cfd.png)


![image](https://user-images.githubusercontent.com/63570918/229980797-7949bdca-49d0-4ce8-a749-15cb1ae225a9.png)

## Select Assistant
```python
from mechanical_scraper import MechanicalScraper


ms = MechanicalScraper()
ms.set_base_url('https://finance.naver.com/')

url = f'{ms.base_url}'
headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/111.0.0.0 Safari/537.36 Edg/111.0.1661.54'
}

# If a value of True is entered in the second argument, a browser will automatically pop up for the response. Then, you can easily copy css selectors via developer's tool.
response = ms.get(url, True, headers=headers)

response.raise_for_status()

bs = BeautifulSoup(response.text, 'html.parser')
elements = bs.select('#container > div.aside > div > div.aside_area.aside_popular > table > tbody > tr')
for el in elements:
    title = el.select_one('th > a').text.strip()
    price = el.select_one('td:nth-child(2)').text.replace(',', '').strip()
    link = ms.get_full_url(el.select_one('th > a')['href'])

    print(title, price, link)
    print()
```
