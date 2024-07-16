---
keywords: metriek - overzicht; rtcdp metriek
title: Homepage van Real-time Customer Data Platform en dashboards
description: Krijg inzicht in diverse dashboards, de startpagina en de eerste gebruikerservaring van Adobe Real-Time CDP.
feature: Dashboards, Get Started
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: 2704184446f7945c744e7e2d2a8c3cda3fc12527
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 1%

---

# [!DNL Real-Time Customer Data Platform] homepage

De startpagina van Adobe Real-time Customer Data Platform (Real-Time CDP) is de eerste pagina die wordt weergegeven nadat u zich hebt aangemeld bij Real-Time CDP.

De Real-Time CDP-startpagina bevat een widget Aan de slag waarmee u snel toegang kunt krijgen tot verschillende functies en een sectie Metrics die bijgewerkte informatie over gegevens binnen uw organisatie weergeeft.

Dit document biedt een overzicht van de Real-Time CDP-startpagina en het dashboard voor meetgegevens.

![ De homepage van Platform UI.](assets/platform-home/home.png)

## Aan de slag-widget

De widget [!UICONTROL Getting started with Real-Time Customer Profile] bestaat uit vier secties:

* **Samenvatting gegevens in Platform**: Deze widget leidt u aan de broncatalogus. Gebruik de broncatalogus om een bron te selecteren en uw gegevens in te voeren in het Experience Platform. Selecteer **[vormen bronnen]** om aan de broncatalogus te navigeren. Voor meer informatie, lees het [ overzicht van bronnen ](../sources/home.md).
* **Model gegevensstructuren**: Deze widget leidt u aan het schemaoverzicht. Gebruik het schemaoverzicht om naar bestaande schema&#39;s te doorbladeren of een blauwdruk tot stand te brengen die de structuur van uw gegevens beschrijven. Selecteer **[!UICONTROL Create schema]** om naar de interface voor het maken van het schema te navigeren. Voor meer informatie, lees het [ schema&#39;s overzicht ](../xdm/home.md).
* **bouwt publiek**: Deze widget richt u aan de Bouwer van het Segment in UI. Gebruik de Bouwer van het Segment om met de gegevenselementen van het Profiel in wisselwerking te staan en de criteria voor uw segmentdefinitie te bepalen. Selecteer **[!UICONTROL Create audience]** om naar de Segment Builder te navigeren. Voor meer informatie, lees het [ overzicht van de Dienst van de Segmentatie ](../segmentation/home.md).
* **verzendt gegevens naar bestemmingen**: Deze widget richt u aan de catalogus van bestemmingen. Gebruik de bestemmingscatalogus om een bestemming te selecteren die u dan met kunt verbinden en publiek naar verzenden. Selecteer **[!UICONTROL Set up destinations]** om naar de doelcatalogus te navigeren. Voor meer informatie, lees het [ overzicht van bestemmingen ](../destinations/home.md).

![ de homepage UI van het Platform die het worden begonnen widget ](assets/platform-home/getting-started-widget.png) toont

## Metrisch dashboard {#metrics-dashboard}

>[!CONTEXTUALHELP]
>id="platform_home_metrics_totalProfiles"
>title="Totaal aantal profielen"
>abstract="Het totale aantal profielen dat uw organisatie binnen het Experience Platform heeft. Dit aantal is gebaseerd op het samenvoegbeleid van uw organisatie en omvat geen profielfragmenten. Het aantal profielen wordt eenmaal per 24 uur bijgewerkt."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html#profile-count" text="Meer informatie in documentatie"

Op het dashboard Metrics wordt actuele informatie over de gegevens van het Experience Platform weergegeven. Het dashboard bestaat uit twee gedeelten:

### Het leaderboard

Het leaderboard toont het huidige totale aantal schema&#39;s, datasets, profielen en soorten publiek in uw organisatie en de meest recente updatedatum.

![ de leaderboard sectie in de homepage van Platform UI.](assets/platform-home/leaderboard.png)

* **Totale schema&#39;s**: De **Totale schema&#39;s** teller toont het aantal schema&#39;s in het systeem. Deze teller wordt bijgewerkt wanneer een schema wordt gecreeerd. Voor meer informatie, lees het [ schema&#39;s overzicht ](../xdm/home.md).
* **Totale datasets**: De **Volledige datasets** teller toont het aantal datasets in het systeem en de hoeveelheid gegevens in Experience Platform. Deze teller wordt bijgewerkt wanneer een dataset wordt gecreeerd. Voor meer informatie over datasets, lees het [ overzicht van datasets ](../catalog/datasets/overview.md).
* **Totale profielen**: De **3} telling van Profielen {toont het totale aantal profielen uw organisatie binnen Experience Platform heeft.** Het bevat geen profielfragmenten. Dit is uw totaal adresseerbare publiek. Dit aantal gebruikt het standaard [ samenvoegbeleid ](profile/merge-policies.md) zoals die in de configuratie van het fusiebeleid in het Profiel van de Klant in real time wordt geplaatst. Het aantal profielen wordt eenmaal per 24 uur bijgewerkt. Selecteer **[!UICONTROL Profiles]** om naar de overzichtspagina Profielen te navigeren en alle maatstaven van uw profiel weer te geven. Voor meer informatie over profielen, lees het [ overzicht van het Profiel van de Klant in real time ](../profile/home.md).
* **Totaal publiek**: Het **Totale publiek** teller toont het totale aantal publiek dat voor uw organisatie wordt gecreeerd. Dit nummer wordt bijgewerkt wanneer een nieuw publiek wordt gemaakt. Voor meer informatie over publiek, lees het [ overzicht van de Dienst van de Segmentatie ](../segmentation/home.md).

### Recente objecten

Recente items geven een overzicht van de meest recente wijzigingen in uw organisatie. In het onderstaande voorbeeld hebben de meest recente wijzigingen betrekking op gegevenssets, bronnen, doelgroepen en bestemmingen.

![ de recente puntensectie in de homepage van UI van het Platform.](assets/platform-home/recent-items.png)

* **Recente datasets**: De **[!UICONTROL Recent datasets]** kaart toont de vijf meest recente datasets die binnen de organisatie worden gecreeerd. Deze lijst wordt bijgewerkt wanneer een nieuwe dataset wordt gecreeerd. Selecteer een dataset om de details voor dat punt te bekijken, of **[!UICONTROL View all]** voor een lijst van datasets te selecteren. Van daar, kunt u een specifieke bron voor details selecteren. Voor meer informatie over datasets, zie het [ overzicht van datasets ](../catalog/datasets/overview.md).
* **Recente bronnen**: De **[!UICONTROL Recent sources]** metrische kaart toont de vijf meest recente die bronnen binnen de organisatie worden gecreeerd. Deze lijst wordt bijgewerkt wanneer een nieuwe bron wordt gemaakt. Selecteer een bron om de details voor dat item weer te geven of selecteer **[!UICONTROL View all]** voor een lijst met bronnen. Van daar, kunt u een specifieke bron voor details selecteren. Voor meer informatie over bronnen, zie [ Overzicht van Bronnen ](../sources/home.md).
* **Recent publiek**: De **[!UICONTROL Recent audiences]** metrische kaart toont de vijf meest recente die publiek binnen de organisatie wordt gecreeerd. Deze lijst wordt bijgewerkt wanneer een nieuw publiek wordt gemaakt. Selecteer een publiek om de details voor dat item weer te geven of selecteer **[!UICONTROL View all]** voor een lijst met soorten publiek. Voor meer informatie over publiek, zie [ Overzicht van de Dienst van de Segmentatie ](../segmentation/home.md).
* **Recente bestemmingen**: De **[!UICONTROL Recent destinations]** metrische kaart toont de vijf meest recente bestemmingen die binnen de organisatie worden gecreeerd. Deze lijst wordt bijgewerkt wanneer een nieuwe bestemming wordt gecreeerd. Selecteer een bestemming om de details voor dat item weer te geven of selecteer **[!UICONTROL View all]** voor een lijst met doelen. Voor meer informatie, lees het [ overzicht van bestemmingen ](../destinations/home.md).

## Bronnen

Tot slot verstrekt de middelen widget u van extra documentatiemiddelen die u kunt verwijzen. Deze omvatten:

![ de middelensectie in de homepage UI van het Platform.](assets/platform-home/resources.png)

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
