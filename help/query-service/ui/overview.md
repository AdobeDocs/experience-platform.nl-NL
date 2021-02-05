---
keywords: Experience Platform;huis;populaire onderwerpen;vraagdienst;de dienst van de Vraag;vraag;vraagredacteur;de redacteur van de vraag;de redacteur van de Vraag;
solution: Experience Platform
title: UI-gids voor zoekservice
topic: guide
description: Adobe Experience Platform Query Service biedt een gebruikersinterface die kan worden gebruikt voor het schrijven en uitvoeren van query's, het weergeven van eerder uitgevoerde query's en het openen van query's die zijn opgeslagen door gebruikers binnen uw IMS-organisatie.
translation-type: tm+mt
source-git-commit: 97dc0b5fb44f5345fd89f3f56bd7861668da9a6e
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 1%

---


# [!DNL Query Service] hulplijn

Adobe Experience Platform [!DNL Query Service] verstrekt een gebruikersinterface die kan worden gebruikt om vragen te schrijven en uit te voeren, eerder uitgevoerde vragen te bekijken, en tot vragen toegang te hebben die door gebruikers binnen uw IMS Organisatie worden bewaard. Om tot UI binnen [Adobe Experience Platform][platform-ui] toegang te hebben, selecteer **[!UICONTROL Vragen]** in de linkernavigatie.

## [!DNL Query Editor]

Met [!DNL Query Editor] kunt u query&#39;s schrijven en uitvoeren zonder een externe client te gebruiken. Klik **[!UICONTROL Create Vraag]** om [!DNL Query Editor] te openen en een nieuwe vraag tot stand te brengen. U kunt tot [!DNL Query Editor] ook toegang hebben door een vraag van &lt;a1 te selecteren/>Logboek ]**of**[!UICONTROL  Browse ]**lusjes.**[!UICONTROL  Als u een eerder uitgevoerde of opgeslagen query selecteert, wordt [!DNL Query Editor] geopend en wordt de SQL voor de geselecteerde query weergegeven.

![Image](../images/queries/ui-overview/overview.png)

[!DNL Query Editor] biedt bewerkruimte waarin u een query kunt typen. Terwijl u typt, wordt in de editor automatisch de voor SQL gereserveerde woorden, tabellen en veldnamen in tabellen ingevuld. Als u klaar bent met het schrijven van uw query, klikt u op de knop **Afspelen** om de query uit te voeren. Op het tabblad **[!UICONTROL Console]** onder de editor ziet u wat [!DNL Query Service] momenteel doet, om aan te geven wanneer een query is geretourneerd. Het **[!UICONTROL Resultaat]** lusje, naast de Console, toont vraagresultaten. Zie [de gids van de Redacteur van de Vraag][query-editor] voor meer informatie bij het gebruiken van [!DNL Query Editor].

![Afbeelding](../images/queries/ui-overview/query-editor.png)

## Bladeren

Het **[!UICONTROL Browse]** lusje toont vragen die door gebruikers in uw organisatie worden bewaard. Het is nuttig om van deze als vraagprojecten te denken, aangezien de vragen hier worden bewaard nog onder bouw kunnen zijn. De vragen die op **[!UICONTROL Browse]** tabel worden getoond tonen ook als looppasvragen op **[!UICONTROL Logboek]** tabel als zij eerder door [!DNL Query Service] zijn uitgevoerd.

![Afbeelding](../images/queries/ui-overview/browse.png)

| Kolom | Beschrijving |
| --- | --- |
| Naam | De naam van de query die door de gebruiker is gemaakt. U kunt op de naam klikken om de vraag in [!DNL Query Editor] te openen. U kunt de onderzoeksbar ook gebruiken om op de Naam van een vraag te zoeken. Zoekopdrachten zijn hoofdlettergevoelig. |
| SQL | De eerste paar tekens van de SQL-query. Als u de muis boven de code houdt, wordt de volledige query weergegeven. |
| Gewijzigd door | De laatste gebruiker die de query heeft gewijzigd. Om het even welke gebruiker in uw organisatie met toegang tot [!DNL Query Service] kan vragen wijzigen. |
| Laatst gewijzigd | De datum en de tijd van de laatste wijziging in de query, in de tijdzone van de browser. |

## Logboek

Het **[!UICONTROL Logboek]** lusje verstrekt een lijst van vragen die eerder zijn uitgevoerd. Door gebrek, maakt een lijst van het logboek van de vragen in omgekeerde chronologie.

![Afbeelding](../images/queries/ui-overview/log.png)

| Kolom | Beschrijving |
| --- | --- |
| **[!UICONTROL Naam]** | De naam van de query, die bestaat uit de eerste verschillende tekens van de SQL-query. Als u op de naam klikt, wordt de query geopend, zodat u deze kunt bewerken. [!DNL Query Editor] Met de zoekbalk kunt u zoeken op de naam van een query. Zoekopdrachten zijn hoofdlettergevoelig. |
| **[!UICONTROL Gemaakt door]** | De naam van de persoon die de query heeft gemaakt. |
| **[!UICONTROL Client]** | De client die voor de query wordt gebruikt. |
| **[!UICONTROL Gegevensset]** | De inputdataset die door de vraag wordt gebruikt. Klik op de dataset om naar het scherm van de details van de inputdataset te gaan. |
| **[!UICONTROL Status]** | De huidige status van de query. |
| **[!UICONTROL Laatste uitvoering]** | Wanneer de query voor het laatst is uitgevoerd. U kunt de lijst in oplopende of aflopende volgorde sorteren door op de pijl boven deze kolom te klikken. |
| **[!UICONTROL Runtime]** | De hoeveelheid tijd nam het om de vraag in werking te stellen. |

## Credentials

Op het tabblad **[!UICONTROL Referenties]** worden uw [!DNL Postgres]-referenties weergegeven. Klik op het pictogram **[!UICONTROL Kopiëren]** naast een veld om de inhoud ervan op te slaan in uw toetsenbordbuffer. Lees voor meer informatie over het gebruik van deze referenties om verbinding te maken met externe clients de [handleiding voor verbindingen met clients][connect-clients].

![Afbeelding](../images/queries/ui-overview/credentials.png)

## Volgende stappen

Nu u met [!DNL Query Service] gebruikersinterface op [!DNL Platform] vertrouwd bent, kunt u tot [!DNL Query Editor] toegang hebben beginnen creërend uw eigen vraagprojecten om met andere gebruikers in uw organisatie te delen. Voor meer informatie over creatie en het runnen van vragen in [!DNL Query Editor], zie [de gebruikersgids van de Redacteur van de Vraag][query-editor].

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
