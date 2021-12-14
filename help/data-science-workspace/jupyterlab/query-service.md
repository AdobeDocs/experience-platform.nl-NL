---
keywords: Experience Platform;JupyterLab;laptops;Data Science Workspace;populaire onderwerpen;query-service
solution: Experience Platform
title: Query-service in Jupyter-laptop
topic-legacy: tutorial
type: Tutorial
description: Met Adobe Experience Platform kunt u SQL (Structured Query Language) gebruiken in de Data Science Workspace door Query Service te integreren in JupyterLab als een standaardfunctie. In deze zelfstudie wordt een voorbeeld gegeven van SQL-query's voor veelvoorkomende gebruiksscenario's voor het verkennen, transformeren en analyseren van Adobe Analytics-gegevens.
exl-id: c5ac7d11-a3bd-4ef8-a650-9f496a8bbaa7
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 1%

---

# Query-service in Jupyter-laptop

[!DNL Adobe Experience Platform] kunt u SQL (Structured Query Language) gebruiken in [!DNL Data Science Workspace] door [!DNL Query Service] in [!DNL JupyterLab] als een standaardfunctie.

Deze zelfstudie demonstreert voorbeeld van SQL-query&#39;s voor veelvoorkomende gebruiksscenario&#39;s voor het verkennen, transformeren en analyseren van bestanden [!DNL Adobe Analytics] gegevens.

## Aan de slag

Voordat u deze zelfstudie kunt starten, moet u aan de volgende voorwaarden voldoen:

- Toegang tot [!DNL Adobe Experience Platform]. Als u geen toegang hebt tot een IMS-organisatie in [!DNL Experience Platform], raadpleeg uw systeembeheerder voordat u verdergaat

- An [!DNL Adobe Analytics] gegevensset

- Een goed begrip van de volgende belangrijkste concepten die in deze zelfstudie worden gebruikt:
   - [[!DNL Experience Data Model (XDM) and XDM System]](../../xdm/home.md)
   - [[!DNL Query Service]](../../query-service/home.md)
   - [[!DNL Query Service SQL Syntax]](../../query-service/sql/overview.md)
   - Adobe Analytics

## Toegang [!DNL JupyterLab] en [!DNL Query Service] {#access-jupyterlab-and-query-service}

1. In [[!DNL Experience Platform]](https://platform.adobe.com), navigeer naar **[!UICONTROL Notebooks]** in de linkernavigatiekolom. Laat JupyterLab even laden.

   ![](../images/jupyterlab/query/jupyterlab-launcher.png)

   >[!NOTE]
   >
   >Als er niet automatisch een nieuw tabblad Launcher wordt weergegeven, opent u een nieuw tabblad Launcher door op **[!UICONTROL File]** Selecteer vervolgens **[!UICONTROL New Launcher]**.

2. Klik op het tabblad Launcher op het tabblad **[!UICONTROL Blank]** in een Python 3-omgeving om een lege laptop te openen.

   ![](../images/jupyterlab/query/blank_notebook.png)

   >[!NOTE]
   >
   >Python 3 is momenteel de enige ondersteunde omgeving voor Query Service in laptops.

3. Klik op de linkerselectieregel op de knop **[!UICONTROL Data]** en dubbelklik op **[!UICONTROL Datasets]** directory om van alle datasets een lijst te maken.

   ![](../images/jupyterlab/query/dataset.png)

4. Zoeken naar [!DNL Adobe Analytics] dataset om op de lijst te onderzoeken en met de rechtermuisknop aan te klikken, klik **[!UICONTROL Query Data in Notebook]** om SQL vragen in het lege notitieboekje te produceren.

5. Klik op de eerste cel die de functie bevat `qs_connect()` en voert u deze uit door op de afspeelknop te klikken. Met deze functie maakt u een verbinding tussen uw laptopexemplaar en de [!DNL Query Service].

   ![](../images/jupyterlab/query/execute.png)

6. Naar beneden kopiëren [!DNL Adobe Analytics] de naam van de dataset van de tweede geproduceerde SQL vraag, zal het de waarde na zijn `FROM`.

   ![](../images/jupyterlab/query/dataset_name.png)

7. Voeg een nieuwe laptopcel in door op de knop **+** knop.

   ![](../images/jupyterlab/query/insert_cell.gif)

8. Kopieer, plak en voer de volgende instructies voor importeren uit in een nieuwe cel. Deze instructies worden gebruikt om uw gegevens te visualiseren:

   ```python
   import plotly.plotly as py
   import plotly.graph_objs as go
   from plotly.offline import iplot
   ```

9. Kopieer en plak vervolgens de volgende variabelen in een nieuwe cel. Wijzig zo nodig de waarden en voer deze uit.

   ```python
   target_table = "your Adobe Analytics dataset name"
   target_year = "2019"
   target_month = "04"
   target_day = "01"
   ```

   - `target_table`: Naam van uw [!DNL Adobe Analytics] dataset.
   - `target_year`: Specifiek jaar waarvoor de doelgegevens afkomstig zijn.
   - `target_month`: Specifieke maand waarvan het doel afkomstig is.
   - `target_day`: De specifieke dag waarop de doelgegevens afkomstig zijn.

   >[!NOTE]
   >
   >U kunt deze waarden op elk gewenst moment wijzigen. Zorg er daarbij voor dat u de cel met variabelen uitvoert voor de wijzigingen die moeten worden toegepast.

## Uw gegevens opvragen {#query-your-data}

Voer de volgende SQL-query&#39;s in voor afzonderlijke laptopcellen. Voer een vraag door op zijn cel te selecteren door te selecteren gevolgd door **[!UICONTROL play]** knop. De succesvolle vraagresultaten of foutenlogboeken worden getoond onder de uitgevoerde cel.

Wanneer een laptop gedurende langere tijd inactief is, wordt de verbinding tussen de laptop en [!DNL Query Service] kan breken. In dergelijke gevallen start u de toepassing opnieuw op [!DNL JupyterLab] door **Opnieuw starten** knop ![knop Opnieuw starten](../images/jupyterlab/user-guide/restart_button.png) in de rechterbovenhoek naast de aan/uit-knop.

De notebookkernel wordt opnieuw ingesteld, maar de cellen blijven, en alle cellen worden opnieuw uitgevoerd om verder te gaan waar u was weggegaan.

### Aantal uren bezoeker {#hourly-visitor-count}

De volgende query retourneert het aantal bezoekers per uur voor een opgegeven datum:

#### Query

```sql
%%read_sql hourly_visitor -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                               AS Day,
       Substring(timestamp, 12, 2)                               AS Hour, 
       Count(DISTINCT concat(enduserids._experience.aaid.id, 
                             _experience.analytics.session.num)) AS Visit_Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

In de bovenstaande vraag, timestamp in `WHERE` -component is ingesteld als de waarde van `target_year`. Variabelen opnemen in SQL-query&#39;s door deze tussen accolades te plaatsen (`{}`).

De eerste regel van de query bevat de optionele variabele `hourly_visitor`. De resultaten van de vraag zullen in deze variabele als dataframe van Pandas worden opgeslagen. Het opslaan van resultaten in een dataframe staat u toe om de vraagresultaten later te visualiseren gebruikend gewenst [!DNL Python] pakket. Het volgende uitvoeren [!DNL Python] code in een nieuwe cel om een staafgrafiek te genereren:

```python
trace = go.Bar(
    x = hourly_visitor['Hour'],
    y = hourly_visitor['Visit_Count'],
    name = "Visitor Count"
)
layout = go.Layout(
    title = 'Visit Count by Hour of Day',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'Hour of Day'),
    yaxis = dict(title = 'Count')
)
fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

### Aantal Uuractiviteit {#hourly-activity-count}

De volgende query retourneert het aantal acties per uur voor een opgegeven datum:

#### Query <!-- omit in toc -->

```sql
%%read_sql hourly_actions -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

Als u de bovenstaande query uitvoert, worden de resultaten opgeslagen in `hourly_actions` als een dataframe. Voer de volgende functie in een nieuwe cel uit om de resultaten te bekijken:

```python
hourly_actions.head()
```

De bovenstaande query kan worden gewijzigd om het aantal acties per uur te retourneren voor een opgegeven datumbereik met behulp van logische operatoren in het dialoogvenster **WAAR** clausule:

#### Query <!-- omit in toc -->

```sql
%%read_sql hourly_actions_date_range -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE  timestamp >= TO_TIMESTAMP('2019-06-01 00', 'YYYY-MM-DD HH')
       AND timestamp <= TO_TIMESTAMP('2019-06-02 23', 'YYYY-MM-DD HH')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

Als u de gewijzigde query uitvoert, worden de resultaten opgeslagen in `hourly_actions_date_range` als een dataframe. Voer de volgende functie in een nieuwe cel uit om de resultaten te bekijken:

```python
hourly_actions_date_rage.head()
```

### Aantal gebeurtenissen per bezoekerssessie {#number-of-events-per-visitor-session}

De volgende query retourneert het aantal gebeurtenissen per bezoekerssessie voor een opgegeven datum:

#### Query <!-- omit in toc -->

```sql
%%read_sql events_per_session -c QS_CONNECTION
SELECT concat(enduserids._experience.aaid.id, 
              '-#', 
              _experience.analytics.session.num) AS aaid_sess_key, 
       Count(timestamp)                          AS Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP BY aaid_sess_key
ORDER BY Count DESC;
```

Het volgende uitvoeren [!DNL Python] code voor het genereren van een histogram voor het aantal gebeurtenissen per bezoekerssessie:

```python
data = [go.Histogram(x = events_per_session['Count'])]

layout = go.Layout(
    title = 'Histogram of Number of Events per Visit Session',
    xaxis = dict(title = 'Number of Events'),
    yaxis = dict(title = 'Count')
)

fig = go.Figure(data = data, layout = layout)
iplot(fig)
```

### Populaire pagina&#39;s voor een bepaalde dag {#popular-pages-for-a-given-day}

De volgende query retourneert de tien populairste pagina&#39;s voor een opgegeven datum:

#### Query <!-- omit in toc -->

```sql
%%read_sql popular_pages -c QS_CONNECTION
SELECT web.webpagedetails.name                 AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY web.webpagedetails.name 
ORDER  BY page_views DESC 
LIMIT  10;
```

### Actieve gebruikers voor een bepaalde dag {#active-users-for-a-given-day}

De volgende query retourneert de tien meest actieve gebruikers voor een opgegeven datum:

#### Query <!-- omit in toc -->

```sql
%%read_sql active_users -c QS_CONNECTION
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp)               AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY aaid
ORDER  BY Count DESC
LIMIT  10;
```

### Actieve steden per gebruikersactiviteit {#active-cities-by-user-activity}

De volgende vraag keert de tien steden terug die een meerderheid van gebruikersactiviteiten voor een gespecificeerde datum produceren:

#### Query <!-- omit in toc -->

```sql
%%read_sql active_cities -c QS_CONNECTION
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp)                                                     AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY state_city
ORDER  BY Count DESC
LIMIT  10;
```

## Volgende stappen

In deze zelfstudie werden voorbeelden van gebruiksgevallen getoond [!DNL Query Service] in [!DNL Jupyter] -laptops. Volg de [Uw gegevens analyseren met Jupyter-laptops](./analyze-your-data.md) zelfstudie om te zien hoe vergelijkbare bewerkingen worden uitgevoerd met behulp van de SDK voor gegevenstoegang.
