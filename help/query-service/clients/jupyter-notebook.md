---
title: Verbind Jupyter Notitieboekje aan de Dienst van de Vraag
description: Leer hoe u Jupyter-laptop kunt verbinden met Adobe Experience Platform Query Service.
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: 1af89160cbf5b689396921869fec6c30a5bcfff0
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Verbinden [!DNL Jupyter Notebook] aan de Dienst van de Vraag

In dit document worden de stappen beschreven die nodig zijn om verbinding te maken [!DNL Jupyter Notebook] met Adobe Experience Platform Query Service.

## Aan de slag

Voor deze handleiding hebt u al toegang tot [!DNL Jupyter Notebook] en vertrouwd zijn met zijn interface. Downloaden [!DNL Jupyter Notebook] Voor meer informatie raadpleegt u de [ambtenaar [!DNL Jupyter Notebook] documentatie](https://jupyter.org/).

Om de vereiste geloofsbrieven te verkrijgen voor het verbinden [!DNL Jupyter Notebook] aan Experience Platform, moet u toegang hebben tot [!UICONTROL Queries] in de gebruikersinterface van het Platform. Neem contact op met uw systeembeheerder als u momenteel geen toegang hebt tot de [!UICONTROL Queries] werkruimte.

>[!TIP]
>
>[!DNL Anaconda Navigator] is een grafische gebruikersinterface voor bureaublad (GUI) die een eenvoudigere manier biedt om veelgebruikte toepassingen te installeren en te starten [!DNL Python] programma&#39;s zoals [!DNL Jupyter Notebook]. Het helpt ook om pakketten, milieu&#39;s, en kanalen te beheren zonder bevel-lijn bevelen te gebruiken.
>Volg het geleide installatieproces op hun website om [uw voorkeursversie van de toepassing installeren](https://docs.anaconda.com/anaconda/install/).
>Selecteer in het beginscherm van de Anaconda Navigator de optie **[!DNL Jupyter Notebook]** in de lijst met ondersteunde toepassingen om het programma te starten.
>Meer informatie vindt u in de [Officiële Anaconda-documentatie](https://docs.anaconda.com/anaconda/navigator/).

De officiële Jupyter-documentatie bevat instructies voor [de laptop uitvoeren vanuit de opdrachtregelinterface](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (CLI).

## Starten [!DNL Jupyter Notebook]

Nadat u een nieuwe [!DNL Jupyter Notebook] webtoepassing, selecteert u de **[!DNL New]** vervolgkeuzelijst vanuit de gebruikersinterface, gevolgd door **[!DNL Python 3]** om een nieuw notebook te maken. De [!DNL Notebook] wordt weergegeven.

Op de eerste regel van de [!DNL Notebook] Voer de volgende waarde in in de editor: `pip install psycopg2-binary` en selecteert u **[!DNL Run]** in de opdrachtbalk. Onder de invoerregel wordt een succesbericht weergegeven.

>[!IMPORTANT]
>
>Als onderdeel van dit proces om een verbinding te maken, moet u **[!DNL Run]** om elke coderegel uit te voeren.

Importeer vervolgens een [!DNL PostgreSQL] databaseadapter voor [!DNL Python]. Voer de waarde in: `import psycopg2`en selecteert u **[!DNL Run]**. Er is geen succesbericht voor dit proces. Ga door met de volgende stap als er geen foutbericht wordt weergegeven.

U moet nu uw Adobe Experience Platform-gebruikersgegevens opgeven door de waarde in te voeren: `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. De verbindingsgegevens vindt u in het dialoogvenster [!UICONTROL Queries] onder [!UICONTROL Credentials] van de gebruikersinterface van het Platform. Zie de documentatie over hoe u [zoeken uw organisatiegeloofsbrieven](../ui/credentials.md) voor gedetailleerde instructies.

Het gebruik van niet-vervallende gegevens wordt aanbevolen wanneer u clients van derden gebruikt om de moeite te besparen dat u herhaaldelijk uw gegevens invoert. Zie de documentatie voor instructies op [hoe te om niet vervallende geloofsbrieven te produceren en te gebruiken](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>Wanneer het kopiëren van geloofsbrieven van UI van het Platform, is er geen behoefte aan extra het formatteren van de geloofsbrieven. Ze kunnen op één regel worden gegeven, met één spatie tussen de eigenschappen en waarden. De referenties staan tussen aanhalingstekens en **niet** gescheiden door komma&#39;s.

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

Uw [!DNL Jupyter Notebook] -instantie is nu verbonden met Query Service.

## Voorbeeld van queryuitvoering

Nu hebt u verbinding [!DNL Jupyter Notebook] aan de Dienst van de Vraag, kunt u vragen op uw datasets uitvoeren gebruikend uw [!DNL Notebook] invoer. In het volgende voorbeeld wordt een eenvoudige query gebruikt om het proces aan te tonen.

Voer de volgende waarden in:

```python
cur = conn.cursor()
cur.execute('''<YOUR_QUERY_HERE>''')
data = [r for r in cur]
```

Roep vervolgens de parameter (`data` in het bovenstaande voorbeeld) als u de query wilt weergeven, resulteert dit in een reactie zonder opmaak.

Gebruik de volgende opdrachten om de resultaten op een meer leesbare manier op te maken:

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`
- `df = pd.DataFrame(samples,columns=colnames)`
- `df.fillna(0,inplace=True)`

Deze opdrachten genereren geen succesbericht. Als er geen foutbericht is, kunt u vervolgens een functie gebruiken om de resultaten van uw SQL-query in een tabelindeling uit te voeren.

Voer de `df.head()` om de in tabelvorm weergegeven queryresultaten te zien.

## Volgende stappen

Nu u met de Dienst van de Vraag hebt verbonden, kunt u gebruiken [!DNL Jupyter Notebook] om query&#39;s te schrijven. Lees voor meer informatie over het schrijven en uitvoeren van query&#39;s de [gids voor uitvoeren van query&#39;s](../best-practices/writing-queries.md).
