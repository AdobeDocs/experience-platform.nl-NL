---
keywords: Experience Platform;huis;populaire onderwerpen;vraagdienst;de dienst van de Vraag;vraag;vraagredacteur;de redacteur van de vraag;de redacteur van de Vraag;
solution: Experience Platform
title: UI-gids voor zoekservice
topic-legacy: guide
description: Adobe Experience Platform Query Service biedt een gebruikersinterface die kan worden gebruikt voor het schrijven en uitvoeren van query's, het weergeven van eerder uitgevoerde query's en het openen van query's die zijn opgeslagen door gebruikers binnen uw IMS-organisatie.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: 30c3ca4aa3e8f42140566c8fdf9fbc855ec72e1b
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 1%

---

# [!DNL Query Service] hulplijn

Adobe Experience Platform [!DNL Query Service] verstrekt een gebruikersinterface die kan worden gebruikt om vragen te schrijven en uit te voeren, eerder uitgevoerde vragen te bekijken, en tot vragen toegang te hebben die door gebruikers binnen uw IMS Organisatie worden bewaard. Om tot UI binnen [Adobe Experience Platform](https://platform.adobe.com) toegang te hebben, selecteer **[!UICONTROL Queries]** in de linkernavigatie.

## [!DNL Query Editor]

Met [!DNL Query Editor] kunt u query&#39;s schrijven en uitvoeren zonder een externe client te gebruiken. Selecteer **[!UICONTROL Create Query]** om [!DNL Query Editor] te openen en een nieuwe vraag tot stand te brengen. U kunt tot [!DNL Query Editor] ook toegang hebben door een vraag van **[!UICONTROL Log]** of **[!UICONTROL Browse]** lusjes te selecteren. Als u een eerder uitgevoerde of opgeslagen query selecteert, wordt [!DNL Query Editor] geopend en wordt de SQL voor de geselecteerde query weergegeven.

![Image](../images/ui/overview/overview.png)

[!DNL Query Editor] biedt bewerkruimte waarin u een query kunt typen. Terwijl u typt, voltooit de redacteur automatisch SQL gereserveerde woorden, lijsten, en gebiedsnamen binnen lijsten. Wanneer het gebeëindigd schrijven van uw vraag, selecteer **Spel** knoop om de vraag in werking te stellen. Het **[!UICONTROL Console]** lusje onder de redacteur toont wat [!DNL Query Service] momenteel doet, erop wijzend wanneer een vraag is teruggekeerd. Het **[!UICONTROL Result]** lusje, naast de Console, toont vraagresultaten. Zie [de gids van de Redacteur van de Vraag](./user-guide.md) voor meer informatie bij het gebruiken van [!DNL Query Editor].

![Afbeelding](../images/ui/overview/query-editor.png)

## Bladeren

Op het tabblad **[!UICONTROL Browse]** worden query&#39;s weergegeven die zijn opgeslagen door gebruikers in uw organisatie. Het is nuttig om van deze als vraagprojecten te denken, aangezien de vragen hier worden bewaard nog onder bouw kunnen zijn. Vragen die op het tabblad **[!UICONTROL Browse]** worden weergegeven, worden ook weergegeven als query&#39;s op het tabblad **[!UICONTROL Log]** als deze eerder zijn uitgevoerd door [!DNL Query Service].

![Afbeelding](../images/ui/overview/browse.png)

| Kolom | Beschrijving |
| --- | --- |
| Naam | De naam van de query die door de gebruiker is gemaakt. U kunt op de naam selecteren om de vraag in [!DNL Query Editor] te openen. U kunt de onderzoeksbar ook gebruiken om op de Naam van een vraag te zoeken. Zoekopdrachten zijn hoofdlettergevoelig. |
| SQL | De eerste paar tekens van de SQL-query. Als u de muis boven de code houdt, wordt de volledige query weergegeven. |
| Gewijzigd door | De laatste gebruiker die de query heeft gewijzigd. Om het even welke gebruiker in uw organisatie met toegang tot [!DNL Query Service] kan vragen wijzigen. |
| Laatst gewijzigd | De datum en de tijd van de laatste wijziging in de query, in de tijdzone van de browser. |

## Logboek

Het tabblad **[!UICONTROL Log]** bevat een lijst met query&#39;s die eerder zijn uitgevoerd. Door gebrek, maakt een lijst van het logboek van de vragen in omgekeerde chronologie.

![Afbeelding](../images/ui/overview/log.png)

| Kolom | Beschrijving |
| --- | --- |
| **[!UICONTROL Name]** | De naam van de query, die bestaat uit de eerste verschillende tekens van de SQL-query. Als u de naam selecteert, wordt [!DNL Query Editor] geopend, zodat u de query kunt bewerken. Met de zoekbalk kunt u zoeken op de naam van een query. Zoekopdrachten zijn hoofdlettergevoelig. |
| **[!UICONTROL Created By]** | De naam van de persoon die de query heeft gemaakt. |
| **[!UICONTROL Client]** | De client die voor de query wordt gebruikt. |
| **[!UICONTROL Dataset]** | De inputdataset die door de vraag wordt gebruikt. Selecteer de dataset om naar het scherm van de details van de inputdataset te gaan. |
| **[!UICONTROL Status]** | De huidige status van de query. |
| **[!UICONTROL Last Run]** | Wanneer de query voor het laatst is uitgevoerd. U kunt de lijst in oplopende of aflopende volgorde sorteren door de pijl boven deze kolom te selecteren. |
| **[!UICONTROL Run Time]** | De hoeveelheid tijd nam het om de vraag in werking te stellen. |

## Credentials

Het **[!UICONTROL Credentials]** lusje toont zowel uw het verlopen als niet-verlopen geloofsbrieven. Lees voor meer informatie over het gebruik van deze referenties om verbinding te maken met externe clients de [aanmeldingsgids](../clients/overview.md).

![Afbeelding](../images/ui/overview/credentials.png)

## Volgende stappen

Nu u met [!DNL Query Service] gebruikersinterface op [!DNL Platform] vertrouwd bent, kunt u tot [!DNL Query Editor] toegang hebben beginnen creërend uw eigen vraagprojecten om met andere gebruikers in uw organisatie te delen. Voor meer informatie over creatie en het runnen van vragen in [!DNL Query Editor], zie [de gebruikersgids van de Redacteur van de Vraag](./user-guide.md).