---
title: Verbinding maken met Data Distiller vanaf een Jupyter-laptop
description: Leer hoe u verbinding maakt met Data Distiller vanaf een Jupyter-laptop.
source-git-commit: 12926f36514d289449cf0d141b5828df3fac37c2
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 0%

---

# Verbinding maken met DD vanuit een Jupyter-laptop

Om uw machine het leren pijpleidingen met de gegevens van de klantenervaring van de hoge waarde te verrijken, moet u eerst met Gegevens Distiller van Notitieboekjes van Jupyter verbinden. In dit document worden de stappen beschreven voor het maken van een verbinding met Data Distiller vanaf een Python-laptop in uw computerleeromgeving.

## Aan de slag

In deze handleiding wordt ervan uitgegaan dat u bekend bent met interactieve Python-laptops en toegang hebt tot een laptopomgeving. De laptop kan worden gehost in een leeromgeving voor machines in de cloud, of lokaal met [Jupyter-laptop](https://jupyter.org/).

### Verbindingsgegevens opvragen

Als u verbinding wilt maken met Data Distiller en andere Adobe Experience Platform-services, hebt u een API-referentie voor Experience Platforms nodig. API-referenties kunnen worden gemaakt in het dialoogvenster  [Adobe Developer Console](https://developer.adobe.com/console/home) door iemand met ontwikkelaars toegang tot het Experience Platform heeft. U wordt geadviseerd om een referentie van Oauth2 API specifiek voor de werkschema&#39;s van de gegevenswetenschap tot stand te brengen en een beheerder van het systeem van de Adobe van uw organisatie te hebben de geloofsbrieven aan een Rol met aangewezen toestemmingen toewijzen.

Zie [API&#39;s van Experience Platforms verifiëren en openen](../../../landing/api-authentication.md) voor gedetailleerde instructies voor het maken van een API-referentie en het verkrijgen van de vereiste machtigingen.

De geadviseerde toestemmingen voor gegevenswetenschap omvatten:

- Sandbox(s) die wordt (worden) gebruikt voor gegevenswetenschap (gewoonlijk pod)
- Gegevensmodellering: Schema&#39;s beheren
- Gegevensbeheer: Datasets beheren
- Gegevensinvoer: Bronnen weergeven
- Doelen: Dataset-doelen beheren en activeren
- Query-service: Query&#39;s beheren

Een rol (en API-referenties die aan die rol zijn toegewezen) heeft standaard geen toegang tot gelabelde gegevens. Afhankelijk van het beleid van het gegevensbeheer van de organisatie, kan een Systeembeheerder de Toegang van de Rol tot bepaalde geëtiketteerde gegevens verlenen die voor het gebruik van de gegevenswetenschap aangewezen wordt geacht. De klanten van het platform zijn verantwoordelijk om etikettoegang en beleid behoorlijk te beheren om aan relevante verordeningen en organisatiebeleid te voldoen.

### Referenties opslaan in een afzonderlijk configuratiebestand

Om uw referentie veilig te houden, verdient het aanbeveling geen referentie-informatie rechtstreeks in uw code te schrijven. Bewaar in plaats daarvan de referentie-informatie in een afzonderlijk configuratiebestand en lees de waarden in die nodig zijn om verbinding te maken met het Experience Platform en Data Distiller.

U kunt bijvoorbeeld een bestand maken met de naam `config.ini` en omvat de volgende informatie (samen met andere informatie, zoals dataset IDs, die nuttig zou zijn om tussen zittingen te bewaren):

```ini
[Credential]
ims_org_id=<YOUR_IMS_ORG_ID>
sandbox_name=<YOUR_SANDBOX_NAME>
client_id=<YOUR_CLIENT_ID>
client_secret=<YOUR_CLIENT_SECRET>
scopes=openid, AdobeID, read_organizations, additional_info.projectedProductContext, session
tech_acct_id=<YOUR_TECHNICAL_ACCOUNT_ID>
```

In uw laptop kunt u de referentie-informatie vervolgens in het geheugen lezen met de `configParser` pakket uit de standaard Python-bibliotheek:

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)
```

Vervolgens kunt u als volgt verwijzen naar waarden voor referentie-referenties binnen de code:

```python
org_id = config.get('Credential', 'ims_org_id')
```

## De `aepp` Python-bibliotheek

[aepp](https://github.com/adobe/aepp/tree/main) is een Adobe-beheerde open-bron bibliotheek van de Python die functies verstrekt om met Gegevens Distiller te verbinden en vragen voor te leggen, zoals het doen van verzoeken aan andere diensten van de Experience Platform. De `aepp` bibliotheek is op zijn beurt afhankelijk van het PostgreSQL-databaseadapterpakket  `psycopg2` voor interactieve Distiller-query&#39;s voor gegevens. Het is mogelijk om met Gegevens Distiller te verbinden en de datasets van het Experience Platform te vragen met `psycopg2` alleen, maar `aepp` biedt meer gemak en extra functionaliteit om aanvragen in te dienen bij alle API-services voor Experience Platforms.

Installeren of upgraden `aepp` en `psycopg2` in uw omgeving kunt u de `%pip` toveropdracht in uw laptop:

```python
%pip install --upgrade aepp
%pip install --upgrade psycopg2-binary
```

U kunt dan vormen `aepp` bibliotheek met uw referentie met behulp van de volgende code:

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)

# Configure aepp with your credentials
import aepp

aepp.configure(
  org_id=config.get('Credential', 'ims_org_id'),
  sandbox=config.get('Credential', 'sandbox_name'),
  client_id=config.get('Credential', 'client_id'), 
  secret=config.get('Credential', 'client_secret'),
  scopes=config.get('Credential', 'scopes'),
  tech_id=config.get('Credential', 'tech_acct_id')
)
```

## Verbinding maken met Data Distiller

Eenmaal `aepp` is geconfigureerd met uw referenties, kunt u de volgende code gebruiken om een verbinding met Data Distiller te maken en als volgt een interactieve sessie te starten:

```python
from aepp import queryservice

dd_conn = queryservice.QueryService().connection()
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

U kunt dan de datasets in uw zandbak van het Experience Platform vragen. Gezien identiteitskaart van een dataset u wilt vragen, kunt u de overeenkomstige lijstnaam van de dienst van de Catalogus terugwinnen en vragen op de lijst in werking stellen:

```python
table_name = 'ecommerce_events'
simple_query = f'''SELECT * FROM {table_name} LIMIT 5'''
dd_cursor.query(simple_query)
```

### Verbind met één enkele dataset voor snellere vraagprestaties

Standaard maakt de gegevensverbinding van Distiller verbinding met alle gegevenssets in uw sandbox. Voor snellere vragen en verminderd middelgebruik, kunt u met een specifieke dataset van belang in plaats daarvan verbinden. U kunt dit doen door de `dbname` in het Distiller-verbindingsobject Data naar `{sandbox}:{table_name}`:

```python
from aepp import queryservice

sandbox = config.get('Credential', 'sandbox_name')
table_name = 'ecommerce_events'

dd_conn = queryservice.QueryService().connection()
dd_conn['dbname'] = f'{sandbox}:{table_name}'
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

## Volgende stappen

Door dit document te lezen hebt u geleerd hoe u verbinding kunt maken met Data Distiller vanaf een Python-laptop in uw computerleeromgeving. De volgende stap bij het maken van functiepijpleidingen van Experience Platform naar aangepaste modellen in uw computerleeromgeving is: [uw gegevenssets verkennen en analyseren](./exploratory-analysis.md).
