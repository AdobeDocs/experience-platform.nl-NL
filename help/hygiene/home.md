---
title: Overzicht van geavanceerd gegevenslevenscyclusbeheer
description: Met Advanced Data Lifecycle Management kunt u de levenscyclus van uw gegevens beheren door verouderde of onjuiste gegevens bij te werken of te wissen.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: 6ef09957d1eb2c07e5607105c782c36f20344bfa
workflow-type: tm+mt
source-wordcount: '817'
ht-degree: 0%

---

# Advanced Data Lifecycle Management in Adobe Experience Platform

Adobe Experience Platform biedt een robuuste set hulpmiddelen voor het beheer van grote, gecompliceerde gegevensbewerkingen om de ervaringen van de consument te kunnen indelen. Aangezien het gegeven in tijd in het systeem wordt opgenomen, wordt het steeds belangrijker om uw gegevensopslag te beheren zodat de gegevens zoals verwacht worden gebruikt, wordt bijgewerkt wanneer de onjuiste gegevens moeten verbeteren, en wordt geschrapt wanneer het organisatorische beleid het noodzakelijk acht.

<!-- Platform's data lifecycle capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

Deze activiteiten kunnen worden uitgevoerd gebruikend de [[!UICONTROL Data Lifecycle] werkruimte UI ](#ui) of [ Hygiene API van Gegevens ](#api). Wanneer een gegevenslevenscyclusbaan uitvoert, verstrekt het systeem transparantie updates bij elke stap van proces. Zie de sectie op [ chronologie en transparantie ](#timelines-and-transparency) voor meer informatie over hoe elk baantype in het systeem wordt vertegenwoordigd.

>[!NOTE]
>
>Het geavanceerde Beheer van de Levenscyclus van Gegevens steunt datasetschrappingen door het [ eindpunt van de gegevenssetvervalsing ](./api/dataset-expiration.md) en identiteitskaart schrappingen (rij-vlakke gegevens) gebruikend primaire identiteiten via het [ werkordeeindpunt ](./api/workorder.md). U kunt [ datasetvervalingen ](./ui/dataset-expiration.md) en [ verslagschrappingen ](./ui/record-delete.md) door Platform UI ook beheren. Raadpleeg de gekoppelde documentatie voor meer informatie. Merk op dat de Levenscyclus van Gegevens geen partijschrapping steunt.

## [!UICONTROL Data Lifecycle] UI-werkruimte {#ui}

Met de [!UICONTROL Data Lifecycle] -werkruimte in de interface van het platform kunt u de levenscyclusbewerkingen van gegevens configureren en plannen, zodat u zeker weet dat uw records op de verwachte manier worden onderhouden.

Voor gedetailleerde stappen bij het beheren van de taken van de gegevenslevenscyclus in UI, zie de [ gids UI van de gegevenslevenscyclus ](./ui/overview.md).

## API voor gegevenshygiëne {#api}

De gebruikersinterface van [!UICONTROL Data Lifecycle] is gebaseerd op de API voor gegevenshygiëne, waarvan de eindpunten direct beschikbaar zijn voor u als u uw activiteiten tijdens de levenscyclus van gegevens liever wilt automatiseren. Zie de [ gids van de Hygiëne API van Gegevens ](./api/overview.md) voor meer informatie.

## Tijdlijnen en transparantie {#timelines-and-transparency}

[ schrapt het Verslag ](./ui/record-delete.md) en de verzoeken van de datasetvervalsing elk hun eigen verwerkingschronologie hebben en transparantie updates op zeer belangrijke punten in hun respectieve werkschema&#39;s verstrekken.

Het volgende vindt plaats wanneer het verzoek van de a [ datasetvervaldatum ](./ui/dataset-expiration.md) wordt gecreeerd:

| Stadium | Tijd na geplande vervaldatum | Beschrijving |
| --- | --- | --- |
| Verzoek is ingediend | 0 uur | Een gegevensbeheerder of privacyanalist dient een verzoek in om een dataset op een bepaald tijdstip te laten verlopen. Het verzoek is zichtbaar in [!UICONTROL Data Lifecycle UI] nadat het is voorgelegd, en blijft in een hangende status tot de geplande vervaltijd, waarna het verzoek zal uitvoeren. |
| Gegevensset is gemarkeerd voor verwijdering | 0-2 uur | Zodra het verzoek wordt uitgevoerd, wordt de dataset gemarkeerd voor schrapping. Als u Amazon Web Services (AWS)-gegevensopslag gebruikt, duurt dit proces maximaal twee uur. Tijdens deze tijd, sluiten de verrichtingen zoals partij en het stromen segmentatie, voorproef of schatting, de uitvoer, en de toegang deze dataset. |
| Gegevensset wordt verwijderd | 3 uur | **Één uur nadat de dataset voor schrapping** wordt gemarkeerd, wordt het volledig verwijderd uit het systeem. Op dit punt, wordt de dataset gelaten vallen van de [ pagina van de datasetinventaris ](../catalog/datasets/user-guide.md) in UI. De gegevens in het datumpigment worden echter in dit stadium slechts weinig verwijderd en blijven dat zo totdat het proces voor het verwijderen van harde gegevens is voltooid. |
| Aantal profielen bijgewerkt | 30 uur | Afhankelijk van de inhoud van de dataset die wordt geschrapt, kunnen sommige profielen uit het systeem worden verwijderd als alle hun componentenattributen aan die dataset worden gebonden. 30 uren nadat de dataset wordt geschrapt, worden om het even welke resulterende veranderingen in algemene profieltellingen weerspiegeld in [ dashboard widgets ](../dashboards/guides/profiles.md#profile-count-trend) en andere rapporten. |
| Soorten publiek bijgewerkt | 48 uur | Zodra alle beïnvloede profielen worden bijgewerkt, worden alle verwante [ publiek ](../segmentation/home.md) bijgewerkt om op hun nieuwe grootte te wijzen. Afhankelijk van de gegevensset die is verwijderd en de kenmerken waarop u segmenteert, kan de grootte van elk publiek toenemen of afnemen als gevolg van de verwijdering. |
| Reizen en bestemmingen bijgewerkt | 50 uur | [ de Reizen ](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [ campagnes ](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), en [ bestemmingen ](../destinations/home.md) worden bijgewerkt volgens veranderingen in verwante segmenten. |
| Harde verwijdering voltooid | 15 dagen | Alle gegevens met betrekking tot de gegevensset zijn hard verwijderd uit het datumpeer. De [ status van de baan van de gegevenslevenscyclus ](./ui/browse.md#view-details) die de dataset schrapte wordt bijgewerkt om dit te weerspiegelen. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Verwijderingen van gegevenssets in Amazon Web Services (AWS) moeten zo&#39;n drie uur duren voordat de wijzigingen volledig worden toegepast. Dit omvat tot twee uren voor de dataset die voor schrapping moet worden gemarkeerd, die door een extra uur wordt gevolgd alvorens het volledig van het systeem wordt gelaten vallen. In tegenstelling, leiden de schrappingsverzoeken voor de instanties van het Platform die de instanties van de Gegevens van Azure gebruiken in directe veranderingen over bedrijfsfuncties.
>
>Voor AWS-gebruikers kan deze vertraging invloed hebben op batchsegmentatie, streamingsegmentatie, voorvertoningen, schattingen, export en gegevenstoegang. Deze latentie is alleen van invloed op klanten die AWS gebruiken, aangezien Azure Data Lake-gebruikers directe updates ervaren. Voor AWS-gebruikers kan het maximaal drie uur duren voordat verzoeken tot verwijdering volledig zijn doorgevoerd in alle betrokken systemen. Pas uw verwachtingen dienovereenkomstig aan.


<!-- ### Record deletes {#record-delete-transparency}

The following takes place when a [record delete request](./ui/record-delete.md) is created:

| Stage | Time after request submission | Description |
| --- | --- | --- |
| Request is submitted | 0 hours | A data steward or privacy analyist submits a record delete request. The request is visible in the [!UICONTROL Data Lifecycle UI] after it has been submitted. |
| Profile lookups updated | 3 hours | The change in profile counts caused by the deleted identity are reflected in [dashboard widgets](../dashboards/guides/profiles.md#profile-count-trend) and other reports. |
| Segments updated | 24 hours | Once profiles are removed, all related [segments](../segmentation/home.md) are updated to reflect their new size. |
| Journeys and destinations updated | 26 hours | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campaigns](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), and [destinations](../destinations/home.md) are updated according to changes in related segments. |
| Records soft deleted in data lake | 7 days | The data is soft deleted from the data lake. |
| Data vacuuming completed | 14 days | The [status of the lifecycle job](./ui/browse.md#view-details) updates to indicate that the job has completed, meaning that data vacuuming has been completed on the data lake and the relevant records have been hard deleted. |

{style="table-layout:auto"} -->

## Volgende stappen

In dit document wordt een overzicht gegeven van de mogelijkheden van het platform voor de levenscyclus van gegevens. Om begonnen te worden het maken van verzoeken van de gegevenshygiëne in UI, verwijs naar de [ gids UI ](./ui/overview.md). Leren hoe te om de banen van de Levenscyclus van Gegevens te creëren programmatically, naar de [ gids van de Hygiëne API van Gegevens ](./api/overview.md) verwijzen
