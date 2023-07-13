---
title: Overzicht van gegevenshygiëne
description: Met Adobe Experience Platform Data Hygiene kunt u de levenscyclus van uw gegevens beheren door verouderde of onjuiste gegevens bij te werken of te wissen.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: e59def7a05862ad880d0b6ada13b1c69c655ff90
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---

# Gegevenshygiëne in Adobe Experience Platform

>[!IMPORTANT]
>
>Gegevenshygiëne is momenteel alleen beschikbaar voor organisaties die deze hebben aangeschaft **Adobe Healthcare Shield** of **Adobe Privacy- en beveiligingsschild**. Deze mogelijkheden zullen in de nabije toekomst algemeen beschikbaar zijn. Neem contact op met uw Adobe-servicevertegenwoordiger voor meer informatie over de beschikbaarheid van Adobe. U kunt echter onmiddellijk [verwijder datasets door [!UICONTROL Datasets] UI](../catalog/datasets/user-guide.md#delete).

Adobe Experience Platform biedt een robuuste set hulpmiddelen voor het beheer van grote, gecompliceerde gegevensbewerkingen om de ervaringen van de consument te kunnen indelen. Aangezien het gegeven in tijd in het systeem wordt opgenomen, wordt het steeds belangrijker om uw gegevensopslag te beheren zodat de gegevens zoals verwacht worden gebruikt, wordt bijgewerkt wanneer de onjuiste gegevens moeten verbeteren, en wordt geschrapt wanneer het organisatorische beleid het noodzakelijk acht.

<!-- Platform's data hygiene capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

Deze activiteiten kunnen worden uitgevoerd met behulp van de [[!UICONTROL Data Hygiene] UI-werkruimte](#ui) of de [API voor gegevenshygiëne](#api). Wanneer een taak voor gegevenshygiëne wordt uitgevoerd, zorgt het systeem voor transparantie-updates bij elke stap van het proces. Zie de sectie over [tijdlijnen en transparantie](#timelines-and-transparency) voor meer informatie over hoe elk baantype in het systeem wordt vertegenwoordigd.

## [!UICONTROL Data Hygiene] UI-werkruimte {#ui}

De [!UICONTROL Data Hygiene] De werkruimte in de interface van het Platform staat u toe om verrichtingen van de gegevenshygiëne te vormen en te plannen, die helpen ervoor te zorgen dat uw verslagen worden gehandhaafd zoals verwacht.

Voor gedetailleerde stappen bij het beheren van de taken van de gegevenshygiëne in UI, zie [Handleiding voor gegevenshygiëne](./ui/overview.md).

## API voor gegevenshygiëne {#api}

De [!UICONTROL Data Hygiene] De gebruikersinterface is gebaseerd op de API voor gegevenshygiëne, waarvan de eindpunten direct beschikbaar zijn voor u als u uw activiteiten voor gegevenshygiëne liever automatiseert. Zie de [Handleiding voor API voor gegevenshygiëne](./api/overview.md) voor meer informatie .

## Tijdlijnen en transparantie

Verzoeken om gegevens te verwijderen en gegevenssets te laten vervallen hebben elk hun eigen verwerkingstijden en verschaffen transparantie-updates op de belangrijkste punten in hun respectieve workflows.

<!-- ### Dataset expirations {#dataset-expiration-transparency} -->

Het volgende gebeurt wanneer een [Vervalaanvraag gegevensset](./ui/dataset-expiration.md) wordt gemaakt:

| Stadium | Tijd na geplande vervaldatum | Beschrijving |
| --- | --- | --- |
| Verzoek is ingediend | 0 uur | Een gegevensbeheerder of privacyanalist dient een verzoek in om een dataset op een bepaald tijdstip te laten verlopen. De aanvraag is zichtbaar in het dialoogvenster [!UICONTROL Data Hygiene UI] nadat de aanvraag is ingediend en in behandeling blijft tot de geplande vervaldatum, waarna de aanvraag zal worden uitgevoerd. |
| Gegevensset wordt verwijderd | 1 uur | De dataset wordt geschrapt van [inventarisatiepagina van gegevensset](../catalog/datasets/user-guide.md) in de gebruikersinterface. De gegevens in het datumpeer worden slechts zachte geschrapt, en zullen zo tot het eind van het proces blijven, waarna het hard zal worden geschrapt. |
| Aantal profielen bijgewerkt | 30 uur | Afhankelijk van de inhoud van de dataset die wordt geschrapt, kunnen sommige profielen uit het systeem worden verwijderd als alle hun componentenattributen aan die dataset worden gebonden. 30 uur nadat de dataset wordt geschrapt, worden om het even welke resulterende veranderingen in algemene profieltellingen weerspiegeld in [dashboardwidgets](../dashboards/guides/profiles.md#profile-count-trend) en andere verslagen. |
| Soorten publiek bijgewerkt | 48 uur | Wanneer alle betrokken profielen zijn bijgewerkt, worden alle gerelateerde [publiek](../segmentation/home.md) worden aangepast aan de nieuwe grootte. Afhankelijk van de gegevensset die is verwijderd en de kenmerken waarop u segmenteert, kan de grootte van elk publiek toenemen of afnemen als gevolg van de verwijdering. |
| Reizen en bestemmingen bijgewerkt | 50 uur | [Reizen](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campagnes](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), en [bestemmingen](../destinations/home.md) worden bijgewerkt op basis van wijzigingen in gerelateerde segmenten. |
| Harde verwijdering voltooid | 14 dagen | Alle gegevens met betrekking tot de gegevensset zijn hard verwijderd uit het datumpeer. De [status van het hygiënisch werk](./ui/browse.md#view-details) die de gegevensset heeft verwijderd, wordt bijgewerkt om deze gegevens weer te geven. |

{style="table-layout:auto"}

<!-- ### Record deletes {#record-delete-transparency}

>[!IMPORTANT]
>
>Record deletes are only available for organizations that have purchased Adobe Healthcare Shield.

The following takes place when a [record delete request](./ui/record-delete.md) is created:

| Stage | Time after request submission | Description |
| --- | --- | --- |
| Request is submitted | 0 hours | A data steward or privacy analyist submits a record delete request. The request is visible in the [!UICONTROL Data Hygiene UI] after it has been submitted. |
| Profile lookups updated | 3 hours | The change in profile counts caused by the deleted identity are reflected in [dashboard widgets](../dashboards/guides/profiles.md#profile-count-trend) and other reports. |
| Segments updated | 24 hours | Once profiles are removed, all related [segments](../segmentation/home.md) are updated to reflect their new size. |
| Journeys and destinations updated | 26 hours | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campaigns](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), and [destinations](../destinations/home.md) are updated according to changes in related segments. |
| Records soft deleted in data lake | 7 days | The data is soft deleted from the data lake. |
| Data vacuuming completed | 14 days | The [status of the hygiene job](./ui/browse.md#view-details) updates to indicate that the job has completed, meaning that data vacuuming has been completed on the data lake and the relevant records have been hard deleted. |

{style="table-layout:auto"} -->

## Volgende stappen

Dit document gaf een overzicht van de mogelijkheden van het Platform op het gebied van gegevenshygiëne. Ga naar de [UI-hulplijn](./ui/overview.md). Als u wilt leren hoe u via programmacode taken voor gegevenshygiëne kunt maken, raadpleegt u de [Handleiding voor API voor gegevenshygiëne](./api/overview.md)
