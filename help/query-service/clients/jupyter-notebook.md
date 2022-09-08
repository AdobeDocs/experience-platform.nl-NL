---
title: Verbind Jupyter Notitieboekje aan de Dienst van de Vraag
description: Leer hoe u Jupyter-laptop kunt verbinden met Adobe Experience Platform Query Service.
source-git-commit: f910deca43ac49d3a3452b8dbafda20ffdf3bf48
workflow-type: tm+mt
source-wordcount: '610'
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
>U kunt [uw voorkeursversie van de toepassing installeren](https://docs.anaconda.com/anaconda/install/) van hun website.
>Volg het geleide installatieproces. Selecteer in het beginscherm van de Anaconda Navigator de optie **[!DNL Jupyter Notebook]** in de lijst met ondersteunde toepassingen om het programma te starten.
>![De [!DNL Anaconda Navigator] beginscherm met [!DNL Jupyter Notebook] gemarkeerd.](../images/clients/jupyter-notebook/anaconda-navigator-home.png)
>Meer informatie vindt u in de [officiële documentatie](https://docs.anaconda.com/anaconda/navigator/).

## Starten [!DNL Jupyter Notebook]

Nadat u een nieuwe [!DNL Jupyter Notebook] webtoepassing, selecteert u de **[!DNL New]** vervolgkeuzelijst gevolgd door **[!DNL Python 3]** om een nieuw notebook te maken. De [!DNL Notebook] wordt weergegeven.

![De [!DNL Jupiter Notebook] Het lusje van het dossier met [!DNL New dropdown] en [!DNL Python] 3 gemarkeerd.](../images/clients/jupyter-notebook/new-notebook.png)

Op de eerste regel van de [!DNL Notebook] Voer de volgende waarde in in de editor: `pip install psycopg2-binary` en selecteert u **[!DNL Run]** in de opdrachtbalk. Onder de invoerregel wordt een succesbericht weergegeven.

>[!IMPORTANT]
>
>Als onderdeel van dit proces om een verbinding te maken, moet u **[!DNL Run]** om elke coderegel uit te voeren.

![De [!DNL Notebook] UI met de opdracht van de installatiebibliotheken gemarkeerd.](../images/clients/jupyter-notebook/install-library.png)

Importeer vervolgens een [!DNL PostgreSQL] databaseadapter voor [!DNL Python]. Voer de waarde in: `import psycopg2`en selecteert u **[!DNL Run]**. Er is geen succesbericht voor dit proces. Ga door met de volgende stap als er geen foutbericht wordt weergegeven.

![De [!DNL Notebook] UI met de code van het de gegevensbestandbestuurder van de invoer benadrukte.](../images/clients/jupyter-notebook/import-dbdriver.png)

U moet nu uw Adobe Experience Platform-gebruikersgegevens opgeven door de waarde in te voeren: `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. De verbindingsgegevens vindt u in het dialoogvenster [!UICONTROL Queries] onder [!UICONTROL Credentials] van de gebruikersinterface van het Platform. Zie de documentatie over hoe u [zoeken uw organisatiegeloofsbrieven](../ui/credentials.md) voor gedetailleerde instructies.

Het gebruik van niet-vervallende gegevens wordt aanbevolen wanneer u clients van derden gebruikt om de moeite te besparen dat u herhaaldelijk uw gegevens invoert. Zie de documentatie voor instructies op [hoe te om niet vervallende geloofsbrieven te produceren en te gebruiken](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>Wanneer het kopiëren van geloofsbrieven van UI van het Platform, zorg ervoor dat er geen extra het formatteren van de geloofsbrieven is. Ze moeten allemaal op één regel staan, met één spatie tussen de eigenschappen en waarden. De referenties staan tussen aanhalingstekens en **niet** gescheiden door komma&#39;s.

![De [!DNL Notebook] UI met de benadrukte verbindingsgeloofsbrieven.](../images/clients/jupyter-notebook/provide-credentials.png)

Uw [!DNL Jupyter Notebook] -instantie is nu verbonden met Query Service.

## Voorbeeld van queryuitvoering

Nu hebt u verbinding [!DNL Jupyter Notebook] aan de Dienst van de Vraag, kunt u vragen op uw datasets uitvoeren gebruikend uw [!DNL Notebook] invoer. In het volgende voorbeeld wordt een eenvoudige query gebruikt om het proces aan te tonen.

Voer de volgende waarden in:

```console
cur = conn.cursor()
cur.execute('''{YOUR_QUERY_HERE}''')
data = [r for r in cur]
```

Roep vervolgens de parameter (`data` in het bovenstaande voorbeeld) als u de query wilt weergeven, resulteert dit in een reactie zonder opmaak.

![De [!DNL Notebook] UI met bevelen om SQL resultaten binnen de Notitie terug te keren en te tonen.](../images/clients/jupyter-notebook/example-query.png)

Gebruik de volgende opdrachten om de resultaten op een meer leesbare manier op te maken:

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`

Deze opdrachten genereren geen succesbericht. Als er geen foutbericht is, kunt u vervolgens een functie gebruiken om de resultaten van uw SQL-query in een tabelindeling uit te voeren.

![De opdrachten die nodig zijn om de SQL-resultaten op te maken.](../images/clients/jupyter-notebook/format-results-commands.png)

Voer de `df.head()` om de in tabelvorm weergegeven queryresultaten te zien.

![In tabelvorm geschreven resultaten van uw SQL-query binnen [!DNL Jupyter Notebook].](../images/clients/jupyter-notebook/format-results-output.png)

## Volgende stappen

Nu u met de Dienst van de Vraag hebt verbonden, kunt u gebruiken [!DNL Jupyter Notebook] om query&#39;s te schrijven. Lees voor meer informatie over het schrijven en uitvoeren van query&#39;s de [gids voor uitvoeren van query&#39;s](../best-practices/writing-queries.md).
