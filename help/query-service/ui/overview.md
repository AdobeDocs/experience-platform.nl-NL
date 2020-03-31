---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handleiding voor de gebruikersinterface van Adobe Experience Platform Query Service
topic: guide
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce

---


# Handleiding Query Service

De Adobe Experience Platform Query Service biedt een gebruikersinterface die kan worden gebruikt voor het schrijven en uitvoeren van query&#39;s, het weergeven van eerder uitgevoerde query&#39;s en het openen van query&#39;s die zijn opgeslagen door gebruikers binnen uw IMS-organisatie. Als u de gebruikersinterface wilt openen in het [Adobe Experience Platform][platform-ui], selecteert u **Vragen** in de linkernavigatie.

## Query-editor

De redacteur van de Vraag laat u toe om vragen te schrijven en uit te voeren zonder een externe cliënt te gebruiken. Klik op Query **** maken om de Query-editor te openen en een nieuwe query te maken. U kunt tot de Redacteur van de Vraag ook toegang hebben door een vraag van de *Logboek* te selecteren of *doorbladert* lusjes. Als u een eerder uitgevoerde of opgeslagen query selecteert, wordt de Query Editor geopend en wordt de SQL voor de geselecteerde query weergegeven.

![Afbeelding](../images/queries/ui-overview/overview.png)

De redacteur van de vraag verstrekt het uitgeven ruimte waar u kunt beginnen een vraag typen. Terwijl u typt, wordt in de editor automatisch de voor SQL gereserveerde woorden, tabellen en veldnamen in tabellen ingevuld. Als u klaar bent met het schrijven van de query, klikt u op **Afspelen** om de query uit te voeren. Het lusje van de *Console* onder de redacteur toont welke Dienst van de Vraag momenteel doet, erop wijzend wanneer een vraag is teruggekeerd. Op het tabblad *Resultaat* naast de Console worden de resultaten van de query weergegeven. Zie de gids [van de Redacteur van de][query-editor] Vraag voor meer informatie bij het gebruiken van de vraagredacteur.

![Afbeelding](../images/queries/ui-overview/query-editor.png)

## Bladeren

Op het tabblad *Bladeren* worden query&#39;s weergegeven die door gebruikers in uw organisatie zijn opgeslagen. Het is nuttig om van deze als vraagprojecten te denken, aangezien de vragen hier worden bewaard nog onder bouw kunnen zijn. De vragen die op het *Browse* lusje worden getoond tonen ook als looppasvragen op het lusje van het *Logboek* als zij eerder door de Dienst van de Vraag zijn uitgevoerd.

![Afbeelding](../images/queries/ui-overview/browse.png)

| Kolom | Beschrijving |
| --- | --- |
| Naam | De naam van de query die door de gebruiker is gemaakt. U kunt op de naam klikken om de vraag in de Redacteur van de Vraag te openen. U kunt de onderzoeksbar ook gebruiken om op de Naam van een vraag te zoeken. Zoekopdrachten zijn hoofdlettergevoelig. |
| SQL | De eerste paar tekens van de SQL-query. Als u de muis boven de code houdt, wordt de volledige query weergegeven. |
| Gewijzigd door | De laatste gebruiker die de query heeft gewijzigd. Om het even welke gebruiker in uw organisatie met toegang tot de Dienst van de Vraag kan vragen wijzigen. |
| Laatst gewijzigd | De datum en de tijd van de laatste wijziging in de query, in de tijdzone van de browser. |

## Logboek

Het tabblad *Logboek* bevat een lijst met query&#39;s die eerder zijn uitgevoerd. Door gebrek, maakt een lijst van het logboek van de vragen in omgekeerde chronologie.

![Afbeelding](../images/queries/ui-overview/log.png)

| Kolom | Beschrijving |
| --- | --- |
| Naam | De naam van de query, die bestaat uit de eerste verschillende tekens van de SQL-query. Als u op de naam klikt, wordt de Query-editor geopend, zodat u de query kunt bewerken. Met de zoekbalk kunt u zoeken op de naam van een query. Zoekopdrachten zijn hoofdlettergevoelig. |
| Gemaakt door | De naam van de persoon die de query heeft gemaakt. |
| Client | De client die voor de query wordt gebruikt. |
| Gegevensset | De inputdataset die door de vraag wordt gebruikt. Klik op de dataset om naar het scherm van de details van de inputdataset te gaan. |
| Status | De huidige status van de query. |
| Laatste uitvoering | Wanneer de query voor het laatst is uitgevoerd. U kunt de lijst in oplopende of aflopende volgorde sorteren door op de pijl boven deze kolom te klikken. |
| Runtime | De hoeveelheid tijd nam het om de vraag in werking te stellen. |

## Credentials

Op het tabblad *Credentials* worden uw referenties van de leverancier weergegeven. Klik op het pictogram **Kopiëren** naast een veld om de inhoud ervan op te slaan in uw toetsenbordbuffer. Lees de handleiding [Verbinding maken met clients voor meer informatie over hoe u deze gegevens kunt gebruiken om verbinding te maken met externe clients][connect-clients].

![Afbeelding](../images/queries/ui-overview/credentials.png)

## Volgende stappen

Nu u met de gebruikersinterface van de Dienst van de Vraag op Platform vertrouwd bent, kunt u tot de Redacteur van de Vraag toegang hebben beginnen uw eigen vraagprojecten te creëren om met andere gebruikers in uw organisatie te delen. Voor meer informatie over het ontwerpen van en het runnen van vragen in de Redacteur van de Vraag, zie de de gebruikersgids [van de Redacteur van de][query-editor]Vraag.

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
