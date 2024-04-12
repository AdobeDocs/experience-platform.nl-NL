---
title: Overzicht van geavanceerd gegevenslevenscyclusbeheer
description: Met Advanced Data Lifecycle Management kunt u de levenscyclus van uw gegevens beheren door verouderde of onjuiste gegevens bij te werken of te wissen.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: fc55e9a0849767d43c7f2a3bc3c540e776c8a072
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 1%

---

# Advanced Data Lifecycle Management in Adobe Experience Platform

Adobe Experience Platform biedt een robuuste set hulpmiddelen voor het beheer van grote, gecompliceerde gegevensbewerkingen om de ervaringen van de consument te kunnen indelen. Aangezien het gegeven in tijd in het systeem wordt opgenomen, wordt het steeds belangrijker om uw gegevensopslag te beheren zodat de gegevens zoals verwacht worden gebruikt, wordt bijgewerkt wanneer de onjuiste gegevens moeten verbeteren, en wordt geschrapt wanneer het organisatorische beleid het noodzakelijk acht.

<!-- Platform's data lifecycle capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

Deze activiteiten kunnen worden uitgevoerd met behulp van [[!UICONTROL Data Lifecycle] UI-werkruimte](#ui) of de [API voor gegevenshygiëne](#api). Wanneer een gegevenslevenscyclusbaan uitvoert, verstrekt het systeem transparantie updates bij elke stap van proces. Zie de sectie over [tijdlijnen en transparantie](#timelines-and-transparency) voor meer informatie over hoe elk baantype in het systeem wordt vertegenwoordigd.

## [!UICONTROL Data Lifecycle] UI-werkruimte {#ui}

De [!UICONTROL Data Lifecycle] In de werkruimte van het Platform UI kunt u de verrichtingen van de gegevenslevenscyclus vormen en plannen, die helpen om ervoor te zorgen dat uw verslagen worden gehandhaafd zoals verwacht.

Voor gedetailleerde stappen voor het beheren van taken van de gegevenslevenscyclus in UI, zie [UI-gids voor gegevenslevenscyclus](./ui/overview.md).

## API voor gegevenshygiëne {#api}

De [!UICONTROL Data Lifecycle] De gebruikersinterface is gebaseerd op de API voor gegevenshygiëne, waarvan de eindpunten direct beschikbaar zijn voor u als u uw activiteiten in de levenscyclus van gegevens liever wilt automatiseren. Zie de [Handleiding voor API voor gegevenshygiëne](./api/overview.md) voor meer informatie .

## Tijdlijnen en transparantie

[Opnemen verwijderen](./ui/record-delete.md) en verzoeken om gegevensset te laten verlopen hebben elk hun eigen verwerkingstijden en verschaffen transparantie-updates op belangrijke punten in hun respectieve werkstromen.

<!-- ### Dataset expirations {#dataset-expiration-transparency} -->

Het volgende vindt plaats wanneer een [Vervalaanvraag gegevensset](./ui/dataset-expiration.md) wordt gemaakt:

| Stadium | Tijd na geplande vervaldatum | Beschrijving |
| --- | --- | --- |
| Verzoek is ingediend | 0 uur | Een gegevensbeheerder of privacyanalist dient een verzoek in om een dataset op een bepaald tijdstip te laten verlopen. De aanvraag is zichtbaar in het dialoogvenster [!UICONTROL Data Lifecycle UI] nadat de aanvraag is ingediend en in behandeling blijft tot de geplande vervaldatum, waarna de aanvraag zal worden uitgevoerd. |
| Gegevensset wordt verwijderd | 1 uur | De dataset wordt geschrapt van [inventarisatiepagina van gegevensset](../catalog/datasets/user-guide.md) in de gebruikersinterface. De gegevens in het datumpeer worden slechts zachte geschrapt, en zullen zo tot het eind van het proces blijven, waarna het hard zal worden geschrapt. |
| Aantal profielen bijgewerkt | 30 uur | Afhankelijk van de inhoud van de dataset die wordt geschrapt, kunnen sommige profielen uit het systeem worden verwijderd als alle hun componentenattributen aan die dataset worden gebonden. 30 uur nadat de dataset wordt geschrapt, worden om het even welke resulterende veranderingen in algemene profieltellingen weerspiegeld in [dashboardwidgets](../dashboards/guides/profiles.md#profile-count-trend) en andere verslagen. |
| Soorten publiek bijgewerkt | 48 uur | Wanneer alle betrokken profielen zijn bijgewerkt, worden alle gerelateerde [publiek](../segmentation/home.md) worden aangepast aan de nieuwe grootte. Afhankelijk van de gegevensset die is verwijderd en de kenmerken waarop u segmenteert, kan de grootte van elk publiek toenemen of afnemen als gevolg van de verwijdering. |
| Reizen en bestemmingen bijgewerkt | 50 uur | [Reizen](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campagnes](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), en [bestemmingen](../destinations/home.md) worden bijgewerkt op basis van wijzigingen in gerelateerde segmenten. |
| Harde verwijdering voltooid | 15 | Alle gegevens met betrekking tot de gegevensset zijn hard verwijderd uit het datumpeer. De [status van de levenscyclus van de gegevens](./ui/browse.md#view-details) die de gegevensset heeft verwijderd, wordt bijgewerkt om deze gegevens weer te geven. |

{style="table-layout:auto"}

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

In dit document wordt een overzicht gegeven van de mogelijkheden van het platform voor de levenscyclus van gegevens. Ga naar de pagina [UI-hulplijn](./ui/overview.md). Als u wilt leren hoe u via programmacode taken in de levenscyclus van gegevens maakt, raadpleegt u de [Handleiding voor API voor gegevenshygiëne](./api/overview.md)
