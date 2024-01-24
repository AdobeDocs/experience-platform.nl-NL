---
keywords: metriek - overzicht; rtcdp metriek
title: Homepage van Real-time Customer Data Platform en dashboards
description: Dashboards, startpagina en eerste gebruikerservaring van Adobe Experience Platform
feature: Dashboards, Get Started
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: f7f49e4158f3aa95c3e96d3687642392e237aabc
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 1%

---

# [!DNL Real-Time Customer Data Platform] homepage

De startpagina van Adobe Real-time Customer Data Platform (Real-Time CDP) is de eerste pagina die wordt weergegeven nadat u zich hebt aangemeld bij Real-Time CDP.

De Real-Time CDP-startpagina bevat een widget Aan de slag waarmee u snel toegang kunt krijgen tot verschillende functies en een sectie Metrics die bijgewerkte informatie over gegevens binnen uw organisatie weergeeft.

Dit document biedt een overzicht van de Real-Time CDP-startpagina en het dashboard voor meetgegevens.

![De homepage van Platform UI.](assets/platform-home/home.png)

## Aan de slag-widget

De [!UICONTROL Getting started with Real-Time Customer Profile] widget bestaat uit vier secties:

* **Gegevens opnemen in platform**: Deze widget stuurt u naar de broncatalogus. Gebruik de broncatalogus om een bron te selecteren en uw gegevens in te voeren in het Experience Platform. Lees voor meer informatie de [overzicht van bronnen](../sources/home.md)
* **Modelgegevensstructuren**: Deze widget leidt u naar het schema&#39;s-overzicht. Gebruik het schemaoverzicht om naar bestaande schema&#39;s te doorbladeren of bouwstenen tot stand te brengen die de structuur van uw gegevens beschrijven. Lees voor meer informatie de [overzicht van schema&#39;s](../xdm/home.md).
* **Segmentpubliek**: Deze widget leidt u naar de [!DNL Segment Builder] in de gebruikersinterface. Gebruik de [!DNL Segment Builder] om met de gegevenselementen van het Profiel in wisselwerking te staan en regels voor uw segmenten te bepalen. Lees voor meer informatie de [Overzicht van segmentatieservice](../segmentation/home.md).
* **Gegevens verzenden naar doelen**: Deze widget stuurt u naar de doelcatalogus. Gebruik de bestemmingscatalogus om een bestemming te selecteren die u dan met kunt verbinden en segmenten verzenden naar. Lees voor meer informatie de [Overzicht van doelen](../destinations/home.md)

![De startpagina van de platformgebruikersinterface met de widget Aan de slag](assets/platform-home/getting-started-widget.png)

## Metrisch dashboard {#metrics-dashboard}

>[!CONTEXTUALHELP]
>id="platform_home_metrics_totalProfiles"
>title="Totaal aantal profielen"
>abstract="Het totale aantal profielen dat uw organisatie binnen het Experience Platform heeft. Dit aantal is gebaseerd op het samenvoegbeleid van uw organisatie en omvat geen profielfragmenten. Het aantal profielen wordt eenmaal per 24 uur bijgewerkt."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html#profile-count" text="Meer informatie in documentatie"

Op het dashboard Metrics wordt actuele informatie over de gegevens van het Experience Platform weergegeven. Het dashboard bestaat uit twee gedeelten:

### Het leaderboard

Het leaderboard toont het huidige totale aantal schema&#39;s, datasets, profielen en segmenten in uw organisatie en hun meest recente updatedatum.

![De leaderboard-sectie in de UI-startpagina van het platform.](assets/platform-home/leaderboard.png)

* **Totaal aantal schema&#39;s**: De **Totaal schema&#39;s** de teller toont het aantal schema&#39;s in het systeem. Deze teller wordt bijgewerkt wanneer een schema wordt gecreeerd. Lees voor meer informatie de [overzicht van schema&#39;s](../xdm/home.md).
* **Totaal aantal gegevenssets**: De **Totaal aantal gegevensbestanden** de teller toont het aantal datasets in het systeem en de hoeveelheid gegevens in [!DNL Platform]. Deze teller wordt bijgewerkt wanneer een dataset wordt gecreeerd. Voor meer informatie over datasets, lees [Overzicht van gegevenssets](../catalog/datasets/overview.md).
* **Totaal aantal profielen**: De **Profielen** het aantal toont het totale aantal profielen uw organisatie binnen Experience Platform heeft. Het bevat geen profielfragmenten. Dit is uw totaal adresseerbare publiek. Deze telling gebruikt het gebrek [samenvoegingsbeleid](profile/merge-policies.md) zoals ingesteld in de configuratie van het samenvoegbeleid in Real-Time Klantprofiel. Het aantal profielen wordt eenmaal per 24 uur bijgewerkt. Voor meer informatie over profielen leest u de [Overzicht van het realtime klantprofiel](../profile/home.md).
* **Totaal aantal segmenten**: **Segmenten** toont het totale aantal segmenten die voor de organisatie worden gecreeerd. Dit aantal wordt bijgewerkt wanneer de nieuwe segmenten worden gecreeerd. Voor meer informatie over segmenten leest u de [Overzicht van segmentatieservice](../segmentation/home.md).

### Recente objecten

Recente items geven een overzicht van de meest recente wijzigingen in uw organisatie. In het onderstaande voorbeeld hebben de meest recente wijzigingen betrekking op gegevenssets, bronnen, segmenten en bestemmingen.

![De recente puntensectie in de homepage van UI van het Platform.](assets/platform-home/recent-items.png)

* **Recente gegevensbestanden**: De **[!UICONTROL Recent datasets]** De kaart toont de vijf meest recente datasets die binnen de organisatie worden gecreeerd. Deze lijst wordt bijgewerkt wanneer een nieuwe dataset wordt gecreeerd. Selecteer een dataset om de details voor dat punt te bekijken, of selecteer **[!UICONTROL View all]** voor een lijst van gegevensbestanden. Van daar, kunt u een specifieke bron voor details selecteren. Voor meer informatie over datasets, zie [Overzicht van gegevenssets](../catalog/datasets/overview.md).
* **Recente bronnen**: De **[!UICONTROL Recent sources]** De metrische kaart toont de vijf meest recente die bronnen binnen de organisatie worden gecreeerd. Deze lijst wordt bijgewerkt wanneer een nieuwe bron wordt gemaakt. Selecteer een bron om de details voor dat item weer te geven of selecteer **[!UICONTROL View all]** voor een lijst van bronnen. Van daar, kunt u een specifieke bron voor details selecteren. Zie voor meer informatie over bronnen [Overzicht van bronnen](../sources/home.md).
* **Recente segmenten**: De **[!UICONTROL Recent segments]** De metrische kaart toont de vijf meest recente die segmenten binnen de organisatie worden gecreeerd. Deze lijst wordt bijgewerkt wanneer een nieuw segment wordt gecreeerd. Selecteer een segment om de details voor dat item weer te geven of selecteer **[!UICONTROL View all]** voor een lijst met segmenten. Zie voor meer informatie over segmenten [Overzicht van segmentatieservice](../segmentation/home.md).
* **Recente bestemmingen**: De **[!UICONTROL Recent destinations]** De metrische kaart toont de vijf meest recente bestemmingen binnen de organisatie worden gecreeerd die. Deze lijst wordt bijgewerkt wanneer een nieuwe bestemming wordt gecreeerd. Selecteer een bestemming om de details voor dat item weer te geven of selecteer **[!UICONTROL View all]** voor een lijst van bestemmingen. Lees voor meer informatie de [Overzicht van doelen](../destinations/home.md).

## Bronnen

Tot slot verstrekt de middelen widget u van extra documentatiemiddelen die u kunt verwijzen. Deze omvatten:

![De middelensectie in de homepage van UI van het Platform.](assets/platform-home/resources.png)

* [Schema&#39;s begrijpen](../xdm/schema/composition.md)
* [Bronnen verbinden](../sources/home.md)
* [Hoe te om uw Real-Time Profiel van de Klant te bevolken](../profile/home.md)
* [Verbindingsdoelen](../destinations/home.md)
* [Toegang beheren](../access-control/abac/overview.md)

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Select **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-Time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Select **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-Time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Select **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->
