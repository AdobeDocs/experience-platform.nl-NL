---
title: Verbind Jupyter Notitieboekje aan de Dienst van de Vraag
description: Leer hoe u Jupyter-laptop kunt verbinden met Adobe Experience Platform Query Service.
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# Verbinden [!DNL Jupyter Notebook] met de Dienst van de Vraag

In dit document worden de stappen beschreven die zijn vereist om [!DNL Jupyter Notebook] te verbinden met Adobe Experience Platform Query Service.

## Aan de slag

Deze handleiding vereist dat u al toegang hebt tot [!DNL Jupyter Notebook] en vertrouwd bent met de interface. Om [!DNL Jupyter Notebook] of voor meer informatie te downloaden, zie de [ officiële  [!DNL Jupyter Notebook]  documentatie ](https://jupyter.org/).

U hebt toegang tot de [!UICONTROL Queries] -werkruimte in de gebruikersinterface van Experience Platform nodig om de vereiste gegevens voor het verbinden van [!DNL Jupyter Notebook] met Experience Platform te verkrijgen. Neem contact op met uw organisatiebeheerder als u momenteel geen toegang hebt tot de werkruimte van [!UICONTROL Queries] .

>[!TIP]
>
>[!DNL Anaconda Navigator] is een grafische gebruikersinterface voor desktops (GUI) waarmee algemene [!DNL Python] -programma&#39;s zoals [!DNL Jupyter Notebook] gemakkelijker kunnen worden geïnstalleerd en gestart. Het helpt ook om pakketten, milieu&#39;s, en kanalen te beheren zonder bevel-lijn bevelen te gebruiken.
>Volg het geleide installatieproces op hun website om [ uw aangewezen versie van de toepassing ](https://docs.anaconda.com/anaconda/install/) te installeren.
>Selecteer in het beginscherm van de Anaconda Navigator de optie **[!DNL Jupyter Notebook]** in de lijst met ondersteunde toepassingen om het programma te starten.
>Meer informatie kan in de [ officiële documentatie Anaconda ](https://docs.anaconda.com/anaconda/navigator/) worden gevonden.

De officiële documentatie van de Jupyter verstrekt instructies [ in werking stellen de notitie van de interface van de bevellijn ](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (CLI).

## Starten [!DNL Jupyter Notebook]

Nadat u een nieuwe [!DNL Jupyter Notebook] webtoepassing hebt geopend, selecteert u het vervolgkeuzemenu **[!DNL New]** in de gebruikersinterface, gevolgd door **[!DNL Python 3]** om een nieuwe laptop te maken. De editor van [!DNL Notebook] wordt weergegeven.

Voer op de eerste regel van de [!DNL Notebook] -editor de volgende waarde in: `pip install psycopg2-binary` en selecteer **[!DNL Run]** in de opdrachtbalk. Onder de invoerregel wordt een succesbericht weergegeven.

>[!IMPORTANT]
>
>Als onderdeel van dit proces om een verbinding te vormen, moet u **[!DNL Run]** selecteren om elke coderegel uit te voeren.

Importeer vervolgens een [!DNL PostgreSQL] databaseadapter voor [!DNL Python] . Voer de waarde in: `import psycopg2` en selecteer **[!DNL Run]** . Er is geen succesbericht voor dit proces. Ga door met de volgende stap als er geen foutbericht wordt weergegeven.

U moet nu uw Adobe Experience Platform-gebruikersgegevens opgeven door de waarde `conn = psycopg2.connect("{YOUR_CREDENTIALS}")` in te voeren. De verbindingsgegevens vindt u in de sectie [!UICONTROL Queries] onder het tabblad [!UICONTROL Credentials] van de gebruikersinterface van Experience Platform. Zie de documentatie op hoe te [ uw organisatiereferenties ](../ui/credentials.md) voor gedetailleerde instructies vinden.

Het gebruik van niet-vervallende gegevens wordt aanbevolen wanneer u clients van derden gebruikt om de moeite te besparen dat u herhaaldelijk uw gegevens invoert. Zie de documentatie voor instructies op [ hoe te om niet-het verlopen geloofsbrieven ](../ui/credentials.md#non-expiring-credentials) te produceren en te gebruiken.

>[!IMPORTANT]
>
>Wanneer het kopiëren van geloofsbrieven van de UI van Experience Platform, is er geen behoefte aan extra het formatteren van de geloofsbrieven. Ze kunnen op één regel worden gegeven, met één spatie tussen de eigenschappen en waarden. De geloofsbrieven worden ingesloten in aanhalingstekens en **niet** komma-gescheiden.

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

Uw [!DNL Jupyter Notebook] -instantie is nu verbonden met Query Service.

## Voorbeeld van queryuitvoering

Nu u [!DNL Jupyter Notebook] met de Dienst van de Vraag hebt verbonden, kunt u vragen op uw datasets uitvoeren gebruikend uw [!DNL Notebook] input. In het volgende voorbeeld wordt een eenvoudige query gebruikt om het proces aan te tonen.

Voer de volgende waarden in:

```python
cur = conn.cursor()
cur.execute('''<YOUR_QUERY_HERE>''')
data = [r for r in cur]
```

Vervolgens roept u de parameter (`data` in het bovenstaande voorbeeld) aan om de queryresultaten in een niet-opgemaakte reactie weer te geven.

Gebruik de volgende opdrachten om de resultaten op een meer leesbare manier op te maken:

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`
- `df = pd.DataFrame(samples,columns=colnames)`
- `df.fillna(0,inplace=True)`

Deze opdrachten genereren geen succesbericht. Als er geen foutbericht is, kunt u vervolgens een functie gebruiken om de resultaten van uw SQL-query in een tabelindeling uit te voeren.

Voer de functie `df.head()` in en voer deze uit om de resultaten van de query met tabellarisme weer te geven.

## Volgende stappen

Nu u met de Dienst van de Vraag hebt verbonden, kunt u [!DNL Jupyter Notebook] gebruiken om vragen te schrijven. Voor meer informatie over hoe te om vragen te schrijven en in werking te stellen, te lezen gelieve de [ lopende vraaggids ](../best-practices/writing-queries.md).
