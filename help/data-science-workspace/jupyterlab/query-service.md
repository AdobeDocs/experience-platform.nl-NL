---
keywords: Experience Platform;JupyterLab;laptops;Data Science Workspace;populaire onderwerpen;query-service
solution: Experience Platform
title: Query-service in Jupyter-laptop
topic: tutorial
type: Tutorial
description: Met Adobe Experience Platform kunt u SQL (Structured Query Language) gebruiken in de Data Science Workspace door Query Service te integreren in JupyterLab als een standaardfunctie. In deze zelfstudie wordt een voorbeeld gegeven van SQL-query's voor veelvoorkomende gebruiksscenario's voor het verkennen, transformeren en analyseren van Adobe Analytics-gegevens.
translation-type: tm+mt
source-git-commit: 9d84fc1eb898020ed4b154c091fcc9fc4933c7de
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 1%

---


# Query-service in Jupyter-laptop

[!DNL Adobe Experience Platform] Hiermee kunt u SQL (Structured Query Language) gebruiken  [!DNL Data Science Workspace] door  [!DNL Query Service] in te integreren  [!DNL JupyterLab] als standaardfunctie.

In deze zelfstudie worden voorbeelden van SQL-query&#39;s getoond voor veelvoorkomende gebruiksscenario&#39;s voor het verkennen, transformeren en analyseren van [!DNL Adobe Analytics]-gegevens.

## Aan de slag

Voordat u deze zelfstudie kunt starten, moet u aan de volgende voorwaarden voldoen:

- Toegang tot [!DNL Adobe Experience Platform]. Als u geen toegang tot een IMS Organisatie in [!DNL Experience Platform] hebt, gelieve met uw systeembeheerder te spreken alvorens te werk te gaan

- Een [!DNL Adobe Analytics]-gegevensset

- Een goed begrip van de volgende belangrijkste concepten die in deze zelfstudie worden gebruikt:
   - [[!DNL Experience Data Model (XDM) and XDM System]](../../xdm/home.md)
   - [[!DNL Query Service]](../../query-service/home.md)
   - [[!DNL Query Service SQL Syntax]](../../query-service/sql/overview.md)
   - Adobe Analytics

## Toegang [!DNL JupyterLab] en [!DNL Query Service] {#access-jupyterlab-and-query-service}

1. Navigeer in [[!DNL Experience Platform]](https://platform.adobe.com) naar **[!UICONTROL Laptops]** vanuit de linkernavigatiekolom. Laat JupyterLab even laden.

   ![](../images/jupyterlab/query/jupyterlab-launcher.png)

   >[!NOTE]
   >
   >Als er niet automatisch een nieuw tabblad Launcher wordt weergegeven, opent u een nieuw tabblad Launcher door te klikken op **[!UICONTROL Bestand]** en vervolgens **[!UICONTROL Nieuwe Launcher]** te selecteren.

2. Klik op het tabblad Launcher op het pictogram **[!UICONTROL Lege]** in een Python 3-omgeving om een lege laptop te openen.

   ![](../images/jupyterlab/query/blank_notebook.png)

   >[!NOTE]
   >
   >Python 3 is momenteel de enige ondersteunde omgeving voor Query Service in laptops.

3. Klik in de linkerselectieregel op het pictogram **[!UICONTROL Gegevens]** en dubbelklik op de map **[!UICONTROL Datasets]** om alle datasets weer te geven.

   ![](../images/jupyterlab/query/dataset.png)

4. Zoek een [!DNL Adobe Analytics] dataset om op de lijst te onderzoeken en met de rechtermuisknop aan te klikken, **[!UICONTROL Gegevens van de Vraag in Notitieboekje]** om SQL vragen in de lege notitieboekje te produceren.

5. Klik op de eerste cel die de functie `qs_connect()` bevat en voer deze uit door op de afspeelknop te klikken. Met deze functie maakt u een verbinding tussen uw laptopexemplaar en [!DNL Query Service].

   ![](../images/jupyterlab/query/execute.png)

6. Kopieer de naam van de [!DNL Adobe Analytics] dataset van de tweede gegenereerde SQL-query omlaag. Dit is de waarde na `FROM`.

   ![](../images/jupyterlab/query/dataset_name.png)

7. Voeg een nieuwe laptopcel in door op de knop **+** te klikken.

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

   - `target_table` : Naam van uw  [!DNL Adobe Analytics] gegevensset.
   - `target_year` : Specifiek jaar waarvoor de doelgegevens afkomstig zijn.
   - `target_month` : Specifieke maand waarvan het doel afkomstig is.
   - `target_day` : De specifieke dag waarop de doelgegevens afkomstig zijn.

   >[!NOTE]
   >
   >U kunt deze waarden op elk gewenst moment wijzigen. Zorg er daarbij voor dat u de cel met variabelen uitvoert voor de wijzigingen die moeten worden toegepast.

## Vraag uw gegevens {#query-your-data}

Voer de volgende SQL-query&#39;s in voor afzonderlijke laptopcellen. Voer een vraag door op zijn cel te selecteren door **[!UICONTROL play]** knoop te selecteren wordt gevolgd. De succesvolle vraagresultaten of foutenlogboeken worden getoond onder de uitgevoerde cel.

Wanneer een laptop gedurende langere tijd inactief is, kan de verbinding tussen de laptop en [!DNL Query Service] verbroken worden. Start in dergelijke gevallen [!DNL JupyterLab] opnieuw door de **Herstart**-knop ![Opnieuw starten](../images/jupyterlab/user-guide/restart_button.png) in de rechterbovenhoek naast de aan/uit-knop te selecteren.

De notebookkernel wordt opnieuw ingesteld, maar de cellen blijven, en alle cellen worden opnieuw uitgevoerd om verder te gaan waar u was weggegaan.

### Aantal uren bezoeker {#hourly-visitor-count}

De volgende query retourneert het aantal bezoekers per uur voor een opgegeven datum:

#### Queryactiviteit

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

In de bovenstaande query wordt de tijdstempel in de `WHERE`-component ingesteld als de waarde van `target_year`. Neem variabelen op in SQL-query&#39;s door deze tussen accolades (`{}`) te plaatsen.

De eerste regel van de query bevat de optionele variabele `hourly_visitor`. De resultaten van de vraag zullen in deze variabele als dataframe van Pandas worden opgeslagen. Het opslaan van resultaten in een dataframe staat u toe om de vraagresultaten later te visualiseren gebruikend gewenst [!DNL Python] pakket. Voer de volgende [!DNL Python] code in een nieuwe cel uit om een bar grafiek te produceren:

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

Als u de bovenstaande query uitvoert, worden de resultaten in `hourly_actions` opgeslagen als een dataframe. Voer de volgende functie in een nieuwe cel uit om de resultaten te bekijken:

```python
hourly_actions.head()
```

De bovenstaande query kan worden gewijzigd om het aantal acties per uur te retourneren voor een opgegeven datumbereik met behulp van logische operatoren in de **WHERE**-component:

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

Als u de gewijzigde query uitvoert, worden de resultaten in `hourly_actions_date_range` opgeslagen als een dataframe. Voer de volgende functie in een nieuwe cel uit om de resultaten te bekijken:

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

Voer de volgende [!DNL Python] code uit om een histogram voor het aantal gebeurtenissen per bezoekzitting te produceren:

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

### Actieve steden op basis van gebruikersactiviteit {#active-cities-by-user-activity}

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

Deze zelfstudie laat een aantal voorbeelden zien van het gebruik van [!DNL Query Service] in [!DNL Jupyter]-laptops. Volg de zelfstudie [Uw gegevens analyseren met behulp van Jupyter-laptops](./analyze-your-data.md) om te zien hoe vergelijkbare bewerkingen worden uitgevoerd met behulp van de SDK voor gegevenstoegang.