---
keywords: Experience Platform;home;popular topics;query service;Query service;query;query editor;Query Editor;Query editor;
solution: Experience Platform
title: Handleiding gebruikersinterface Adobe Experience Platform Query Service
topic: guide
description: De Adobe Experience Platform Query Service biedt een gebruikersinterface die kan worden gebruikt voor het schrijven en uitvoeren van query's, het weergeven van eerder uitgevoerde query's en het openen van query's die zijn opgeslagen door gebruikers binnen uw IMS-organisatie.
translation-type: tm+mt
source-git-commit: d2f098cb9e4aaf5beaad02173a22a25a87a43756
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 1%

---


# [!DNL Query Service] hulplijn

De Adobe Experience Platform [!DNL Query Service] biedt een gebruikersinterface die kan worden gebruikt voor het schrijven en uitvoeren van query&#39;s, het weergeven van eerder uitgevoerde query&#39;s en het openen van query&#39;s die zijn opgeslagen door gebruikers binnen uw IMS-organisatie. U opent de gebruikersinterface in [Adobe Experience Platform][platform-ui]door **[!UICONTROL query&#39;s]** in de linkernavigatie te selecteren.

## [!DNL Query Editor]

Met [!DNL Query Editor] deze optie kunt u query&#39;s schrijven en uitvoeren zonder een externe client te gebruiken. Klik op Query **** maken om de query te openen [!DNL Query Editor] en een nieuwe query te maken. U kunt tot de toegang ook toegang hebben [!DNL Query Editor] door een vraag van de **[!UICONTROL Logboek]** te selecteren of **[!UICONTROL doorbladert]** lusjes. Als u een eerder uitgevoerde of opgeslagen query selecteert, wordt de query geopend [!DNL Query Editor] en wordt de SQL voor de geselecteerde query weergegeven.

![Image](../images/queries/ui-overview/overview.png)

[!DNL Query Editor] biedt bewerkruimte waarin u een query kunt typen. Terwijl u typt, wordt in de editor automatisch de voor SQL gereserveerde woorden, tabellen en veldnamen in tabellen ingevuld. Wanneer u klaar bent met het schrijven van uw query, klikt u op de knop **Afspelen** om de query uit te voeren. Op het tabblad **[!UICONTROL Console]** onder de editor ziet u wat er op dit moment [!DNL Query Service] gebeurt. Dit geeft aan wanneer een query is geretourneerd. Op het tabblad **[!UICONTROL Resultaat]** naast de Console worden de resultaten van de query weergegeven. Zie de gids [van de Redacteur van de][query-editor] Vraag voor meer informatie bij het gebruiken van [!DNL Query Editor].

![Image](../images/queries/ui-overview/query-editor.png)

## Bladeren

Op het tabblad **[!UICONTROL Bladeren]** worden query&#39;s weergegeven die door gebruikers in uw organisatie zijn opgeslagen. Het is nuttig om van deze als vraagprojecten te denken, aangezien de vragen hier worden bewaard nog onder bouw kunnen zijn. De vragen die op het **[!UICONTROL Browse]** lusje worden getoond tonen ook als looppasvragen op het lusje van het **[!UICONTROL Logboek]** als zij eerder door [!DNL Query Service]zijn uitgevoerd.

![Image](../images/queries/ui-overview/browse.png)

| Kolom | Beschrijving |
| --- | --- |
| Naam | De naam van de query die door de gebruiker is gemaakt. U kunt op de naam klikken om de vraag in te openen [!DNL Query Editor]. U kunt de onderzoeksbar ook gebruiken om op de Naam van een vraag te zoeken. Zoekopdrachten zijn hoofdlettergevoelig. |
| SQL | De eerste paar tekens van de SQL-query. Als u de muis boven de code houdt, wordt de volledige query weergegeven. |
| Gewijzigd door | De laatste gebruiker die de query heeft gewijzigd. Om het even welke gebruiker in uw organisatie met toegang tot [!DNL Query Service] kan vragen wijzigen. |
| Laatst gewijzigd | De datum en de tijd van de laatste wijziging in de query, in de tijdzone van de browser. |

## Logboek

Het tabblad **[!UICONTROL Logboek]** bevat een lijst met query&#39;s die eerder zijn uitgevoerd. Door gebrek, maakt een lijst van het logboek van de vragen in omgekeerde chronologie.

![Image](../images/queries/ui-overview/log.png)

| Kolom | Beschrijving |
| --- | --- |
| **[!UICONTROL Naam]** | De naam van de query, die bestaat uit de eerste verschillende tekens van de SQL-query. Als u op de naam klikt, wordt de query geopend, [!DNL Query Editor]zodat u de query kunt bewerken. Met de zoekbalk kunt u zoeken op de naam van een query. Zoekopdrachten zijn hoofdlettergevoelig. |
| **[!UICONTROL Gemaakt door]** | De naam van de persoon die de query heeft gemaakt. |
| **[!UICONTROL Client]** | De client die voor de query wordt gebruikt. |
| **[!UICONTROL Gegevensset]** | De inputdataset die door de vraag wordt gebruikt. Klik op de dataset om naar het scherm van de details van de inputdataset te gaan. |
| **[!UICONTROL Status]** | De huidige status van de query. |
| **[!UICONTROL Laatste uitvoering]** | Wanneer de query voor het laatst is uitgevoerd. U kunt de lijst in oplopende of aflopende volgorde sorteren door op de pijl boven deze kolom te klikken. |
| **[!UICONTROL Runtime]** | De hoeveelheid tijd nam het om de vraag in werking te stellen. |

## Credentials

Op het tabblad **[!UICONTROL Referenties]** worden uw [!DNL Postgres] referenties weergegeven. Klik op het pictogram **[!UICONTROL Kopiëren]** naast een veld om de inhoud ervan op te slaan in uw toetsenbordbuffer. Lees de handleiding [Verbinding maken met clients voor meer informatie over hoe u deze gegevens kunt gebruiken om verbinding te maken met externe clients][connect-clients].

![Image](../images/queries/ui-overview/credentials.png)

## Volgende stappen

Nu u met [!DNL Query Service] gebruikersinterface op vertrouwd bent [!DNL Platform], kunt u tot stand brengen beginnen uw eigen vraagprojecten [!DNL Query Editor] te creëren om met andere gebruikers in uw organisatie te delen. Voor meer informatie over creatie en lopende vragen in [!DNL Query Editor], zie de de gebruikersgids [van de Redacteur van de][query-editor]Vraag.

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
