import json
import requests
from bs4 import BeautifulSoup

data = requests.get('http://worldpopulationreview.com/continents/southern-africa-population/')


soup = BeautifulSoup(data.text, 'html.parser')

table = soup.find('div', id='main-page-content')
rows = table.find_all('tr')
for tr in rows:
    td = tr.find_all('td')
    row = [i.text for i in td]
      
    
    jsondata = json.dumps(row, indent=2, sort_keys=True)
with open('data.json', 'w') as f:
   f.write(jsondata)
