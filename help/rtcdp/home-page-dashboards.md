---
title: Homepage en dashboards van het Klantgegevensplatform in real time
seo-title: Homepage en dashboards van het Klantgegevensplatform in real time
description: Dashboards, Home Page en First-Time User Experience Platform
seo-description: Dashboards, Home Page en First-Time User Experience Platform
translation-type: tm+mt
source-git-commit: 6c8d0757d7e7568b1976823d9c52221374e67cbb

---


# Overzicht van de gegevens van het platform van de Gegevens in real time van de Klant

De homepage van het Platform van de Gegevens van de Klant van Adobe In real time (CDP in real time), die een metriek dashboard omvat, verschijnt wanneer u login aan CDP in real time.

De homepage is slechts een van de plaatsen waar metrische kaarten verschijnen. CDP in real time verstrekt metrische kaarten door uw ervaring. Deze metriek informeren u over de gegevens, het profiel, en het segmentpubliek in het systeem.

![image](assets/home2.jpg)

Als er geen gegevens in het systeem zijn wanneer u login aan CDP in real time, verschijnt het dashboard op de homepage niet. In dit geval biedt de startpagina leermateriaal voor een eerste gebruikerservaring. Aangezien het gegeven wordt verzameld-in andere woorden, aangezien de <!--sources-->datasets, de profielen, de segmenten, en de bestemmingen worden gecreeerd en de gegevens stromen in systeem-dashboard automatisch bijgewerkt om informatie over die gegevens<!-- in metric cards-->te tonen.

## Dashboardweergave startpagina

<!--The dashboard shows information in several areas. Each category of information displays for the time range shown beneath the data.-->

Het dashboard bestaat uit<!-- two areas.-->:

* **Het leaderboard** bevindt zich boven aan het dashboard. Het leaderboard toont het aantal gegevenssets, profielen, segmenten en doelen in het systeem.

   ![image](assets/home-leaderboard2.jpg)

<!-- * **Metric cards** display beneath the leaderboard. Metric cards show additional information, such as percentages or trends. Metric cards appear as data is collected.
    ![image](assets/home-metrics.jpg)
Some information is shown in different ways on both the leaderboard and metric cards. -->
* **De recente punten** maken een lijst van de vijf meest recente datasets, bronnen, segmenten, en bestemmingen die aan het systeem worden toegevoegd.

   ![image](assets/home-recent.jpg)

De extra metriek-bijvoorbeeld voor profielen en segmenten-zijn beschikbaar in andere delen van het Platform van Gegevens van de Klant in real time.

### Gegevenssets

De **[!UICONTROL teller van Datasets]** toont het aantal datasets in het systeem en de hoeveelheid gegevens in Platform. Deze teller wordt bijgewerkt wanneer een dataset wordt gecreeerd.

Voor meer informatie over datasets, zie de Gegevens van de [Samenvatting in het Platform](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/data_ingestion_tutorial/data_ingestion_tutorial.md)van de Ervaring van Adobe.

### Profielen

Het aantal **[!UICONTROL profielen]** geeft het totale aantal personen met profielen weer in het realtime profiel van de klant. Het bevat geen profielfragmenten. Dit is uw totaal adresseerbare publiek.

Deze telling gebruikt het standaardsamenvoegbeleid [](profile/merge-policies.md) zoals die in de configuratie van het fusiebeleid in Verenigd Profiel wordt geplaatst.

Het aantal profielen wordt eenmaal per 24 uur bijgewerkt.

Voor meer informatie over profielen, zie [een verenigde mening van uw klant in real time CDP](profile/profile-overview.md).

### Segmenten

**[!UICONTROL De segmenten]** tonen het totale aantal segmenten die voor de organisatie worden gecreeerd. Dit aantal wordt bijgewerkt wanneer de nieuwe segmenten worden gecreeerd.

Voor meer informatie over segmenten, zie het overzicht [van de Dienst van de](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/segmentation/segmentation-overview.md)Segmentatie.

### Doelen

**[!UICONTROL De bestemmingen]** tonen het totale aantal bestemmingen die voor de organisatie worden gecreeerd. Dit aantal wordt bijgewerkt wanneer de nieuwe bestemmingen worden gecreeerd.

Voor meer informatie over bestemmingen, zie het overzicht [van](destinations/destinations-overview.md)Doelen.

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Click **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Click **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Click **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->

### Recente gegevensbestanden

De **[!UICONTROL Recente datasets]** kaart toont de vijf meest recente datasets die binnen de organisatie worden gecreeerd. Deze lijst wordt bijgewerkt wanneer een nieuwe dataset wordt gecreeerd.

Klik een dataset om de details voor dat punt te bekijken, of allen **[!UICONTROL te]** bekijken om de lijst van datasets te zien. Hier kunt u op een specifieke bron klikken voor meer informatie.

Voor meer informatie over datasets, zie de Gegevens van de [Samenvatting in het Platform](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/data_ingestion_tutorial/data_ingestion_tutorial.md)van de Ervaring van Adobe.

### Recente bronnen

De **[!UICONTROL Recente bronnen]** metrische kaart toont de vijf meest recente die bronnen binnen de organisatie worden gecreeerd. Deze lijst wordt bijgewerkt wanneer een nieuwe bron wordt gemaakt.

Klik een bron om de details voor dat punt te bekijken, of allen **[!UICONTROL te]** bekijken om de lijst van bronnen te zien. Hier kunt u op een specifieke bron klikken voor meer informatie.

Voor meer informatie over bronnen, zie [Bronoverzicht](sources/sources-overview.md).

### Recente segmenten

De **[!UICONTROL Recente segmenten]** metrische kaart toont de vijf meest recente segmenten die binnen de organisatie worden gecreeerd. Deze lijst wordt bijgewerkt wanneer een nieuw segment wordt gecreeerd.

Klik een segment om de details voor dat punt te bekijken, of allen **[!UICONTROL te]** bekijken om informatie over meer segmenten te zien.

Voor meer informatie over segmenten, zie het overzicht [van de Dienst van de](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/segmentation/segmentation-overview.md)Segmentatie.

### Recente bestemmingen

De **[!UICONTROL Recente bestemmingen]** metrische kaart toont de vijf meest recente bestemmingen binnen de organisatie worden gecreeerd die. Deze lijst wordt bijgewerkt wanneer een nieuwe bestemming wordt gecreeerd.

Klik een bestemming om de details voor dat punt te bekijken, of allen **[!UICONTROL te]** bekijken om informatie over meer bestemmingen te zien.

Voor meer informatie over bestemmingen, zie het overzicht [van](destinations/destinations-overview.md)Doelen.
