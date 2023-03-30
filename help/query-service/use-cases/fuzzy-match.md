---
title: Fuzzy Match in de Dienst van de Vraag
description: Leer hoe te om een gelijke op uw Platform gegevens uit te voeren die resultaten van veelvoudige datasets door ongeveer een koord van uw keus combineert te passen.
source-git-commit: 633210fe5e824d8686a23b877a406db3780ebdd4
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 0%

---

# Fuzzy match in de Dienst van de Vraag

Gebruik een &#39;vage&#39; match op je Adobe Experience Platform-gegevens om de meest waarschijnlijke, bijna overeenkomende overeenkomsten te retourneren zonder dat er naar tekenreeksen met identieke tekens moet worden gezocht. Hierdoor kunt u uw gegevens veel flexibeler doorzoeken en uw gegevens toegankelijker maken door tijd en moeite te besparen.

In plaats van te proberen om de onderzoekskoorden opnieuw te formatteren om hen aan te passen, analyseert de vage gelijke de verhouding van gelijkenis tussen twee opeenvolgingen en keert het percentage van gelijkenis terug. [[!DNL FuzzyWuzzy]](https://pypi.org/project/fuzzywuzzy/) wordt aanbevolen voor dit proces, aangezien de functies ervan geschikter zijn om tekenreeksen in complexere situaties aan te passen in vergelijking met [!DNL regex] of [!DNL difflib].

Het voorbeeld dat in dit gebruiksgeval wordt gegeven, is gericht op het afstemmen van vergelijkbare kenmerken van een zoekopdracht in een hotelkamer in twee verschillende gegevensbestanden voor reisbureaus. In het document wordt weergegeven hoe tekenreeksen op basis van de mate van overeenkomst met grote, afzonderlijke gegevensbronnen moeten worden vergeleken. In dit voorbeeld vergelijkt de wazzy match de zoekresultaten met de functies van een kamer van de reisbureaus Luma en Acme.

## Aan de slag {#getting-started}

Als onderdeel van dit proces moet u een model voor machinaal leren trainen, wordt in dit document uitgegaan van een praktische kennis van een of meer computerleeromgevingen.

Dit voorbeeld gebruikt [!DNL Python] en de [!DNL Jupyter Notebook] ontwikkelomgeving. Hoewel er veel opties beschikbaar zijn, [!DNL Jupyter Notebook] wordt aanbevolen omdat het een opensource webtoepassing is met lage computervereisten. Het kan worden gedownload van [de officiële Jupyter-site](https://jupyter.org/).

Voordat u begint, moet u de benodigde bibliotheken importeren. [!DNL FuzzyWuzzy] is een open-sourced [!DNL Python] op de [!DNL difflib] en wordt gebruikt om tekenreeksen aan te passen. Gebruikt [!DNL Levenshtein Distance] om de verschillen tussen reeksen en patronen te berekenen. [!DNL FuzzyWuzzy] heeft de volgende eisen:

- [!DNL Python] 2.4 (of hoger)
- [!DNL Python-Levenshtein]

Gebruik vanaf de opdrachtregel de volgende opdracht om te installeren [!DNL FuzzyWuzzy]:

```console
pip install fuzzywuzzy
```

Of gebruik de volgende opdracht om te installeren [!DNL Python-Levenshtein] ook:

```console
pip install fuzzywuzzy[speedup]
```

Meer technische informatie over [!DNL Fuzzywuzzy] kan worden gevonden in hun [officiële documentatie](https://pypi.org/project/fuzzywuzzy/).

### Verbinding maken met Query-service

U moet het model van het machinleren aan de Dienst van de Vraag verbinden door uw verbindingsgeloofsbrieven te verstrekken. Zowel kunnen het verlopen als niet-het verlopen geloofsbrieven worden verstrekt. Zie de [aanmeldingsgids](../ui/credentials.md) voor meer informatie over hoe te om de noodzakelijke geloofsbrieven te verkrijgen. Als u [!DNL Jupyter Notebook], lees de volledige handleiding op [hoe te met de Dienst van de Vraag te verbinden](../clients/jupyter-notebook.md).

Zorg er ook voor dat u de [!DNL numpy] in uw [!DNL Python] omgeving om lineaire algebra mogelijk te maken.

```python
import numpy as np
```

De hieronder bevelen zijn noodzakelijk om met de Dienst van de Vraag van te verbinden [!DNL Jupyter Notebook]:

```python
import psycopg2
conn = psycopg2.connect('''
sslmode=require
host=<YOUR_ORGANIZATION_ID>
port=80
dbname=prod:all
user=<YOUR_ADOBE_ID_TO_CONNECT_TO_QUERY_SERVICE>
password=<YOUR_QUERY_SERVICE_PASSWORD>
''')
cur = conn.cursor()
```

Uw [!DNL Jupyter Notebook] -instantie is nu verbonden met Query Service. Als de verbinding tot stand is gebracht, wordt er geen bericht weergegeven. Als de verbinding mislukt, wordt een fout weergegeven.

### Gegevens tekenen vanuit de Luminagedataset {#luma-dataset}

De gegevens voor analyse worden getrokken van de eerste dataset met de volgende bevelen. Kortom, de voorbeelden zijn beperkt tot de eerste tien resultaten van de kolom.

```python
cur.execute('''SELECT * FROM luma;
''')    
luma = np.array([r[0] for r in cur])

luma[:10]
```

Selecteren **Uitvoer** om de geretourneerde array weer te geven.

+++Uitvoer

```console
array(['Deluxe King Or Queen Room', 'Kona Tower City / Mountain View',
       'Luxury Double Room', 'Alii Tower Ocean View With King Bed',
       'Club Two Queen', 'Corner Deluxe Studio',
       'Luxury Queen Room With Two Queen Beds', 'Grand Corner King Room',
       'Accessible Club Ocean View Suite With One King Bed',
       'Junior Suite'], dtype='<U66')
```

+++

### Gegevens tekenen uit de gegevensset Acme {#acme-dataset}

De gegevens voor analyse worden nu getrokken van de tweede dataset met de volgende bevelen. Om kort te gaan, zijn de voorbeelden beperkt gebleven tot de eerste 10 resultaten van de kolom.

```python
cur.execute('''SELECT * FROM acme;
''')    
acme = np.array([r[0] for r in cur])

acme[:10]
```

Selecteren **Uitvoer** om de geretourneerde array weer te geven.

+++Uitvoer

```console
array(['Deluxe King Or Queen Room', 'Kona Tower City / Mountain View',
       'Luxury Double Room', 'Alii Tower Ocean View With King Bed',
       'Club Two Queen', 'Corner Deluxe Studio',
       'Luxury Queen Room With Two Queen Beds', 'Grand Corner King Room',
       'Accessible Club Ocean View Suite With One King Bed',
       'Junior Suite'], dtype='<U66')
```

+++

### Een vage scores-functie maken {#fuzzy-scoring}

Vervolgens moet u importeren `fuzz` uit de FuzzyWuzzy-bibliotheek en voer een vergelijking van de tekenreeksen in gedeeltelijke verhouding uit. Met de functie voor partiële verhoudingen kunt u overeenkomende subtekenreeksen uitvoeren. Hierbij wordt de kortste tekenreeks gebruikt die overeenkomt met alle subtekenreeksen met dezelfde lengte. De functie retourneert een percentage gelijkenis van maximaal 100%. De functie voor gedeeltelijke verhouding zou bijvoorbeeld de volgende tekenreeksen &#39;Deluxe Room&#39;, &#39;1 King Bed&#39; en &#39;Deluxe King Room&#39; vergelijken en een vergelijkbare score van 69% retourneren.

In de het gebruikscase van de de ruimteovereenkomst van het hotel, wordt dit gedaan gebruikend de volgende bevelen:

```python
from fuzzywuzzy import fuzz
def compute_match_score(x,y):
    return fuzz.partial_ratio(x,y)
```

Volgende, importeren `cdist` van de [!DNL SciPy] bibliotheek om de afstand tussen elk paar in de twee inzamelingen van input gegevens te berekenen. Dit berekent de scores onder alle paren hotelkamers die door elk van de reisbureaus worden verstrekt.

```python
from scipy.spatial.distance import cdist
pairwise_distance =  cdist(luma.reshape((-1,1)),acme.reshape((-1,1)),compute_match_score)
```

### Toewijzingen maken tussen de twee kolommen met behulp van de vage samenvoegscore

Nu de kolommen zijn gescoord op afstand, kunt u de paren indexeren en alleen overeenkomsten behouden die een score hoger dan een bepaald percentage hebben. In dit voorbeeld blijven alleen paren behouden die overeenkomen met een score van 70% of hoger.

```python
matched_pairs = []
for i,c1 in enumerate(luma):
    idx = np.where(pairwise_distance[i,:] > 70)[0]
    for j in idx:
        matched_pairs.append((luma[i].replace("'","''"),acme[j].replace("'","''")))
```

De resultaten kunnen met het volgende bevel worden getoond. Kortom, de resultaten zijn beperkt tot tien rijen.

```python
matched_pairs[:10]
```

Selecteren **Uitvoer** om de resultaten te zien.

+++Uitvoer

```console
[('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Standard Room, Lagoon View', 'Standard Room With Ocean View'),
 ('Standard Room, Lagoon View', 'Standard Room Dolphin Lagoon View'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, Corner', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Suite', 'Corner Deluxe Studio')]
```

+++

De resultaten worden dan aangepast gebruikend SQL met het volgende bevel:

<!-- Q) Why and is this accurate? -->

```python
matching_sql = ' OR '.join(["(e.luma = '{}' AND b.acme = '{}')".format(c1,c2) for c1,c2 in matched_pairs])
```

## Pas de afbeeldingen toe om vage verbindingen in de Dienst van de Vraag uit te voeren {#mappings-for-query-service}

Daarna, worden de high-scoring passende paren aangesloten bij het gebruiken van SQL om een nieuwe dataset tot stand te brengen.

```python
:
cur.execute('''
SELECT *  FROM luma e
CROSS JOIN acme b
WHERE 
{}
'''.format(matching_sql)) 
[r for r in cur]
```

Selecteren **Uitvoer** om de resultaten van deze verbinding te zien.

+++Uitvoer

```console
[('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Standard Room, Lagoon View', 'Standard Room With Ocean View'),
 ('Standard Room, Lagoon View', 'Standard Room Dolphin Lagoon View'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, Corner', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Suite', 'Corner Deluxe Studio'),
 ('Deluxe Suite', 'Deluxe Suite'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Club Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Business King Room'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds',
  'Business Double Room With Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Deluxe Double Room'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Deluxe Suite, 1 Bedroom', 'Deluxe Suite'),
 ('City Room, City View', 'Room With City View'),
 ('City Room, City View', 'Queen Room With City View'),
 ('City Room, City View', 'Club Level King Or Queen Room with City View'),
 ('Club Room, Premium 2 Queen Beds', 'Club Premium Two Queen'),
 ('Club Room, Premium 2 Queen Beds', 'Premium Two Queen'),
 ('Deluxe Room, Lake View', 'Deluxe King Or Queen Room with Lake View'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('Deluxe Suite, 1 King Bed, Non Smoking, Kitchen', 'Deluxe Suite'),
 ('Junior Suite, 1 King Bed, Accessible (Roll-in Shower)', 'Junior Suite'),
 ('Regency Club, Mountain View', 'Regency Club Ocean View'),
 ('Regency Club, Mountain View', 'Regency Club Mountain View'),
 ('Club Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Room, 2 Queen Beds, City View',
  'Queen Room With Two Queen Beds and City View'),
 ('Deluxe Room', 'Queen Room'),
 ('Deluxe Room', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Room', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room', 'Deluxe Room - One King Bed'),
 ('Room, Partial Ocean View', 'Room With Ocean View'),
 ('Room, Partial Ocean View', 'Partial Ocean View With Two Double Beds'),
 ('Room, Partial Ocean View', 'Kona Tower Partial Ocean View'),
 ('Room, Partial Ocean View', 'Partial Ocean View Room'),
 ('Room, Partial Ocean View', 'Waikiki Tower Partial Ocean View'),
 ('Premium Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Grand Corner King Room, 1 King Bed', 'Grand Corner King Room'),
 ('Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Room, 1 King Bed', 'Ocean View Room With King Bed'),
 ('Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, 1 King Bed, Non Smoking', 'Deluxe Room - One King Bed'),
 ('Room, 2 Double Beds, Accessible, Partial Ocean View',
  'Accessible Partial Ocean View With Two Double Beds'),
 ('Room, 2 Double Beds, Accessible, Partial Ocean View',
  'Partial Ocean View Room'),
 ('Room, Ocean View ', 'Room With Ocean View'),
 ('Room, Ocean View ', 'King Or Two Queen Room With Ocean View'),
 ('Room, Ocean View ', 'Standard Room With Ocean View'),
 ('Signature Suite, 1 Bedroom', 'Signature King'),
 ('Room, 2 Queen Beds (Waikiki View)',
  'Queen Room With Two Queen Beds and Waikiki View'),
 ('Deluxe Room', 'Queen Room'),
 ('Deluxe Room', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Room', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room', 'Deluxe Room - One King Bed'),
 ('Standard Room, Oceanfront', 'Standard Room With Ocean View'),
 ('Standard Room, Oceanfront', 'Standard Room With Ocean Front View'),
 ('Standard Room, Mountain View (City View - Kona Tower) - No Resort Fee',
  'Standard Room With Mountain View'),
 ('Standard Room, Mountain View (City View - Kona Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('High-Floor Premium Room, 1 King Bed', 'High-Floor Premium King Room'),
 ('Club Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Junior Suite, 1 King Bed with Sofa Bed', 'Junior Suite'),
 ('Junior Suite, 1 King Bed with Sofa Bed', 'Deluxe King Suite With Sofa Bed'),
 ('Deluxe Room, City View', 'Queen Room With City View'),
 ('Deluxe Room, City View', 'Club Level King Or Queen Room with City View'),
 ('Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Room, 1 King Bed', 'Ocean View Room With King Bed'),
 ('Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Room, 2 Double Beds, Partial Ocean View', 'Kona Tower Partial Ocean View'),
 ('Room, 2 Double Beds, Partial Ocean View', 'Partial Ocean View Room'),
 ('Room, 1 Queen Bed, City View',
  'Queen Room With Two Queen Beds and City View'),
 ('Room, Ocean View', 'Room With Ocean View'),
 ('Room, Ocean View', 'King Or Two Queen Room With Ocean View'),
 ('Room, Ocean View', 'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Partial Ocean View Room'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Standard Room With Ocean Front View'),
 ('Standard Room, Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean Front View'),
 ('Regency Club, Ocean View',
  'Accessible Club Ocean View Suite With One King Bed'),
 ('Regency Club, Ocean View', 'Regency Club Ocean View'),
 ('Regency Club, Ocean View', 'Regency Club Mountain View'),
 ('Standard Room, Mountain View (Scenic)', 'Standard Room With Mountain View'),
 ('Standard Room, Mountain View (Scenic)', 'Standard Room With Ocean View'),
 ('Room, 1 Queen Bed', 'Deluxe Room - Two Queen Beds'),
 ('Double Room', 'Luxury Double Room'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Queen Room'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Business Double Room With Two Double Beds'),
 ('Double Room', 'Deluxe Double Room'),
 ('Club Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Twin Room', 'High-Floor Premium King Room'),
 ('Premier Twin Room', 'Premier King Room'),
 ('Premier Twin Room', 'Premier Queen Room With Two Queen Beds'),
 ('Premier Twin Room', 'Premium King Room With Free Wi-Fi'),
 ('Premium Room, 1 Queen Bed', 'Premium Two Queen'),
 ('Premium Room, 2 Queen Beds', 'Premium Two Queen'),
 ('Deluxe Room, 1 Queen Bed (High Floor)', 'Deluxe Room - Two Queen Beds'),
 ('Room, 2 Queen Beds, Garden View',
  'Queen Room With Two Queen Beds and Garden View'),
 ('Signature Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Signature Room, 2 Queen Beds', 'Signature Two Queen'),
 ('Standard Room, Ocean View', 'Room With Ocean View'),
 ('Standard Room, Ocean View', 'Standard Room With Ocean View'),
 ('Standard Room, Ocean View', 'Standard Room With Ocean Front View')]
```

+++

### Zwak overeenkomende resultaten opslaan in Platform {#save-to-platform}

Tot slot kunnen de resultaten van de vage gelijke als dataset voor gebruik in Adobe Experience Platform worden bewaard gebruikend SQL.

```python
cur.execute(''' 
Create table luma_acme_join
AS
(SELECT *  FROM luma e
CROSS JOIN acme b
WHERE 
{})
'''.format(matching_sql))
```


