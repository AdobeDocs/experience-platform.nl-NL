---
keywords: Experience Platform;huis;populaire onderwerpen;vraagdienst;de dienst van de Vraag;vraag;vraagredacteur;de redacteur van de vraag;de redacteur van de Vraag;
solution: Experience Platform
title: UI-gids voor zoekservice
topic-legacy: guide
description: Adobe Experience Platform Query Service biedt een gebruikersinterface die kan worden gebruikt voor het schrijven en uitvoeren van query's, het weergeven van eerder uitgevoerde query's en het openen van query's die zijn opgeslagen door gebruikers binnen uw IMS-organisatie.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: a887c502213e96d6af90af0859da78c2984f89a7
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# [!DNL Query Service] UI-hulplijn

De Adobe Experience Platform [!DNL Query Service] biedt een gebruikersinterface die kan worden gebruikt voor het schrijven en uitvoeren van query&#39;s, het weergeven van eerder uitgevoerde query&#39;s en het openen van query&#39;s die zijn opgeslagen door gebruikers binnen uw IMS-organisatie. Om tot UI binnen toegang te hebben [Adobe Experience Platform](https://platform.adobe.com), selecteert u **[!UICONTROL Queries]** in de linkernavigatie.

## [!DNL Query Editor]

De [!DNL Query Editor] laat u toe om vragen te schrijven en uit te voeren zonder een externe cliënt te gebruiken. Selecteren **[!UICONTROL Create Query]** om de [!DNL Query Editor] en maak een nieuwe query. U hebt ook toegang tot de [!DNL Query Editor] door een query te selecteren in het menu **[!UICONTROL Log]** of **[!UICONTROL Browse]** tabs. Als u een eerder uitgevoerde of opgeslagen query selecteert, wordt het dialoogvenster [!DNL Query Editor] en geeft u de SQL voor de geselecteerde query weer.

![Het dashboard Vragen met de markering Query maken.](../images/ui/overview/overview.png)

[!DNL Query Editor] biedt bewerkruimte waarin u een query kunt typen. Terwijl u typt, voltooit de redacteur automatisch SQL gereserveerde woorden, lijsten, en gebiedsnamen binnen lijsten. Wanneer u klaar bent met het schrijven van uw query, selecteert u de opdracht **Afspelen** om de query uit te voeren. De **[!UICONTROL Console]** onder de editor ziet u wat [!DNL Query Service] doet momenteel, erop wijst die wanneer een vraag is teruggekeerd. De **[!UICONTROL Result]** naast de Console worden de resultaten van de query weergegeven. Zie de [Handleiding voor Query-editor](./user-guide.md) voor meer informatie over het gebruik van de [!DNL Query Editor].

![Een ingezoomd object met het oog op de [!DNL Query Editor].](../images/ui/overview/query-editor.png)

## Bladeren {#browse}

De **[!UICONTROL Browse]** tabblad geeft query&#39;s weer die zijn opgeslagen door gebruikers in uw organisatie. Het is nuttig om van deze als vraagprojecten te denken, aangezien de vragen hier worden bewaard nog onder bouw kunnen zijn. Vragen weergegeven op de **[!UICONTROL Browse]** tabblad wordt ook weergegeven als query&#39;s in het dialoogvenster **[!UICONTROL Log]** tab als ze eerder zijn uitgevoerd door [!DNL Query Service].

![Een ingezoomd in mening het dashboard van Vragen doorbladert lusje die verscheidene bewaarde vragen toont.](../images/ui/overview/browse.png)

| Kolom | Beschrijving |
| --- | --- |
| **[!UICONTROL Name]** | De naam van de query die door de gebruiker is gemaakt. U kunt op de naam selecteren om de query te openen in het dialoogvenster [!DNL Query Editor]. U kunt de onderzoeksbar ook gebruiken om op de Naam van een vraag te zoeken. Zoekopdrachten zijn hoofdlettergevoelig. |
| **[!UICONTROL SQL]** | De eerste paar tekens van de SQL-query. Als u de muis boven de code houdt, wordt de volledige query weergegeven. |
| **[!UICONTROL Modified by]** | De laatste gebruiker die de query heeft gewijzigd. Elke gebruiker in uw organisatie die toegang heeft tot [!DNL Query Service] kan query&#39;s wijzigen. |
| **[!UICONTROL Last modified]** | De datum en de tijd van de laatste wijziging in de query, in de tijdzone van de browser. |

## Logboek

De **[!UICONTROL Log]** bevat een lijst met query&#39;s die eerder zijn uitgevoerd. Door gebrek, maakt een lijst van het logboek van de vragen in omgekeerde chronologie.

![Een ingezoomd in mening van het lusje van het Logboek van het Dashboard van Vragen die een lijst van vragen in omgekeerde chronologische orde toont.](../images/ui/overview/log.png)

| Kolom | Beschrijving |
| --- | --- |
| **[!UICONTROL Name]** | De naam van de query, die bestaat uit de eerste verschillende tekens van de SQL-query. Als u de naam selecteert, wordt het dialoogvenster [!DNL Query Editor], zodat u de query kunt bewerken. Met de zoekbalk kunt u zoeken op de naam van een query. Zoekopdrachten zijn hoofdlettergevoelig. |
| **[!UICONTROL Created by]** | De naam van de persoon die de query heeft gemaakt. |
| **[!UICONTROL Client]** | De client die voor de query wordt gebruikt. |
| **[!UICONTROL Dataset]** | De inputdataset die door de vraag wordt gebruikt. Selecteer de dataset om naar het scherm van de details van de inputdataset te gaan. |
| **[!UICONTROL Status]** | De huidige status van de query. |
| **[!UICONTROL Last run]** | Wanneer de query voor het laatst is uitgevoerd. U kunt de lijst in oplopende of aflopende volgorde sorteren door de pijl boven deze kolom te selecteren. |
| **[!UICONTROL Run time]** | De hoeveelheid tijd nam het om de vraag in werking te stellen. |

## Credentials

De **[!UICONTROL Credentials]** geeft zowel uw vervallende als niet-vervallende referenties weer. Voor meer informatie over hoe u deze referenties kunt gebruiken om verbinding te maken met externe clients, leest u de [aanmeldingsgids](../clients/overview.md).

![Het dashboard Vragen met het tabblad Referenties gemarkeerd.](../images/ui/overview/credentials.png)

## Volgende stappen

Nu bent u bekend met [!DNL Query Service] gebruikersinterface op [!DNL Platform], kunt u [!DNL Query Editor] beginnen uw eigen vraagprojecten te creëren om met andere gebruikers in uw organisatie te delen. Voor meer informatie over creatie en het runnen van vragen in [!DNL Query Editor], zie de [[!DNL Query Editor] gebruikershandleiding](./user-guide.md).