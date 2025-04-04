---
title: Verbinding maken met Data Distiller vanaf een Jupyter-laptop
description: Leer hoe u verbinding maakt met Data Distiller vanaf een Jupyter-laptop.
exl-id: e6238b00-aaeb-40c0-a90f-9aebb1a1c421
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# Verbinding maken met Data Distiller vanaf een Jupyter-laptop

Als u uw computer wilt verrijken met instructiepijpleidingen met hoogwaardige gegevens voor klanten, moet u eerst verbinding maken met Data Distiller via [!DNL Jupyter Notebooks] . In dit document worden de stappen beschreven voor het maken van een verbinding met Data Distiller vanaf een [!DNL Python] -laptop in de leeromgeving van uw computer.

## Aan de slag

In deze handleiding wordt ervan uitgegaan dat u bekend bent met interactieve [!DNL Python] -laptops en toegang hebt tot een laptopomgeving. De laptop kan worden gehost in een leeromgeving voor computers in de cloud, of lokaal met [[!DNL Jupyter Notebook] ](https://jupyter.org/) .

### Verbindingsgegevens opvragen {#obtain-credentials}

Als u verbinding wilt maken met Data Distiller en andere Adobe Experience Platform-services, hebt u een Experience Platform API-referentie nodig. API geloofsbrieven kunnen in [ Adobe Developer Console ](https://developer.adobe.com/console/home) door iemand met de toegang van de Ontwikkelaar tot Experience Platform worden gecreeerd. U wordt geadviseerd om een referentie van Oauth2 API specifiek voor de werkschema&#39;s van de gegevenswetenschap tot stand te brengen en een het systeemadmin van Adobe van uw organisatie te hebben de geloofsbrieven aan een rol met aangewezen toestemmingen toewijzen.

Zie [ voor authentiek verklaren en toegang Experience Platform APIs ](../../../landing/api-authentication.md) voor gedetailleerde instructies bij het creëren van een API referentie en het verkrijgen van de vereiste toestemmingen.

De geadviseerde toestemmingen voor gegevenswetenschap omvatten:

- Sandbox(s) die wordt (worden) gebruikt voor gegevenswetenschap (gewoonlijk `prod`)
- Gegevensmodellering: [!UICONTROL Manage Schemas]
- Gegevensbeheer: [!UICONTROL Manage Datasets]
- Gegevensinvoer: [!UICONTROL View Sources]
- Doelen: [!UICONTROL Manage and Activate Dataset Destinations]
- Query-service: [!UICONTROL Manage Queries]

Een rol (en API-referenties die aan die rol zijn toegewezen) heeft standaard geen toegang tot gelabelde gegevens. Afhankelijk van het beleid van de organisatie inzake gegevensbeheer, kan een Admin van het Systeem de rol toegang verlenen tot bepaalde geëtiketteerde gegevens die voor gebruik van de gegevenswetenschap aangewezen worden geacht. Experience Platform-klanten zijn verantwoordelijk voor het op passende wijze beheren van toegang tot labels en beleid om te voldoen aan de desbetreffende regelgeving en het desbetreffende organisatiebeleid.

### Referenties opslaan in een afzonderlijk configuratiebestand {#store-credentials}

Om uw referentie veilig te houden, verdient het aanbeveling geen referentie-informatie rechtstreeks in uw code te schrijven. Bewaar in plaats daarvan de referentie-informatie in een afzonderlijk configuratiebestand en lees de waarden in die nodig zijn om verbinding te maken met de Experience Platform en Data Distiller.

U kunt bijvoorbeeld een bestand met de naam `config.ini` maken en de volgende informatie (samen met andere informatie, zoals id&#39;s van gegevenssets, die u tussen sessies kunt opslaan) opnemen:

```ini
[Credential]
ims_org_id=<YOUR_IMS_ORG_ID>
sandbox_name=<YOUR_SANDBOX_NAME>
client_id=<YOUR_CLIENT_ID>
client_secret=<YOUR_CLIENT_SECRET>
scopes=openid, AdobeID, read_organizations, additional_info.projectedProductContext, session
tech_acct_id=<YOUR_TECHNICAL_ACCOUNT_ID>
```

In uw laptop kunt u de referentie-informatie vervolgens in het geheugen lezen met behulp van het pakket `configParser` uit de standaard [!DNL Python] -bibliotheek:

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

## PP Python-bibliotheek installeren {#install-python-library}

[ aepp ](https://github.com/adobe/aepp/tree/main) is een Adobe-Beheerde open-source [!DNL Python] bibliotheek die functies verstrekt om met Gegevens Distiller te verbinden en vragen voor te leggen, zoals het doen van verzoeken aan andere diensten van Experience Platform. De `aepp` -bibliotheek is op zijn beurt afhankelijk van het PostgreSQL-databaseadapterpakket `psycopg2` voor interactieve Distiller-query&#39;s voor gegevens. Het is mogelijk verbinding te maken met Data Distiller en Experience Platform-gegevenssets te controleren met `psycopg2` alleen, maar `aepp` biedt meer gebruiksgemak en extra functionaliteit om aanvragen in te dienen bij alle Experience Platform API-services.

Als u `aepp` en `psycopg2` wilt installeren of upgraden in uw omgeving, kunt u de opdracht `%pip` Magisch in uw notitieboekje gebruiken:

```python
%pip install --upgrade aepp
%pip install --upgrade psycopg2-binary
```

Vervolgens kunt u de `aepp` -bibliotheek configureren met uw referentie aan de hand van de volgende code:

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

## Verbinding maken met Data Distiller {#create-connection}

Wanneer `aepp` is geconfigureerd met uw referenties, kunt u de volgende code gebruiken om een verbinding met Data Distiller te maken en als volgt een interactieve sessie te starten:

```python
from aepp import queryservice

dd_conn = queryservice.QueryService().connection()
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

U kunt dan de datasets in uw zandbak van Experience Platform vragen. Gezien identiteitskaart van een dataset u wilt vragen, kunt u de overeenkomstige lijstnaam van de dienst van de Catalogus terugwinnen en vragen op de lijst in werking stellen:

```python
table_name = 'ecommerce_events'
simple_query = f'''SELECT * FROM {table_name} LIMIT 5'''
dd_cursor.query(simple_query)
```

### Verbind met één enkele dataset voor snellere vraagprestaties {#connect-to-single-dataset}

Standaard maakt de gegevensverbinding van Distiller verbinding met alle gegevenssets in uw sandbox. Voor snellere vragen en verminderd middelgebruik, kunt u met een specifieke dataset van belang in plaats daarvan verbinden. U kunt dit doen door het `dbname` in het Distiller-verbindingsobject Data te wijzigen in `{sandbox}:{table_name}` :

```python
from aepp import queryservice

sandbox = config.get('Credential', 'sandbox_name')
table_name = 'ecommerce_events'

dd_conn = queryservice.QueryService().connection()
dd_conn['dbname'] = f'{sandbox}:{table_name}'
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

## Volgende stappen

Door dit document te lezen, hebt u geleerd hoe u verbinding kunt maken met Data Distiller vanaf een [!DNL Python] -laptop in de leeromgeving van uw computer. De volgende stap in het creëren van eigenschappijpleidingen van Experience Platform om douanemodellen in uw machine het leren milieu te voeren moet [ uw datasets ](./exploratory-analysis.md) onderzoeken en analyseren.
