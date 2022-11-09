---
title: Overzicht van gegevenshygiëne
description: Met Adobe Experience Platform Data Hygiene kunt u de levenscyclus van uw gegevens beheren door verouderde of onjuiste gegevens bij te werken of te wissen.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: 850ab3c98fb27d1dcf98b02dfbef0c8ae3b2ad62
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---

# Gegevenshygiëne in Adobe Experience Platform

>[!IMPORTANT]
>
>Gegevenshygiëne is momenteel alleen beschikbaar voor organisaties die deze hebben aangeschaft **Adobe Healthcare Shield** of **Adobe Privacy- en beveiligingsschild**.

Adobe Experience Platform biedt een robuuste set hulpmiddelen voor het beheer van grote, gecompliceerde gegevensbewerkingen om de ervaringen van de consument te kunnen indelen. Aangezien het gegeven in tijd in het systeem wordt opgenomen, wordt het steeds belangrijker om uw gegevensopslag te beheren zodat de gegevens zoals verwacht worden gebruikt, wordt bijgewerkt wanneer de onjuiste gegevens moeten verbeteren, en wordt geschrapt wanneer het organisatorische beleid het noodzakelijk acht.

Met de mogelijkheden voor gegevenshygiëne van het Platform kunt u uw opgeslagen consumentengegevens als volgt beheren:

* Het plannen van geautomatiseerde datasetvervaldatums
* Verwijderen van consumentengegevens op basis van ingebedde identiteiten

Deze activiteiten kunnen worden uitgevoerd met behulp van de [[!UICONTROL Data Hygiene] UI-werkruimte](#ui) of de [API voor gegevenshygiëne](#api). Wanneer een taak voor gegevenshygiëne wordt uitgevoerd, zorgt het systeem voor transparantie-updates bij elke stap van het proces. Zie de sectie over [tijdlijnen en transparantie](#timelines-and-transparency) voor meer informatie over hoe elk baantype in het systeem wordt vertegenwoordigd.

## [!UICONTROL Data Hygiene] UI-werkruimte {#ui}

De [!UICONTROL Data Hygiene] De werkruimte in de interface van het Platform staat u toe om verrichtingen van de gegevenshygiëne te vormen en te plannen, die helpen ervoor te zorgen dat uw verslagen worden gehandhaafd zoals verwacht.

Voor gedetailleerde stappen bij het beheren van de taken van de gegevenshygiëne in UI, zie [Handleiding voor gegevenshygiëne](./ui/overview.md).

## API voor gegevenshygiëne {#api}

De [!UICONTROL Data Hygiene] De gebruikersinterface is gebaseerd op de API voor gegevenshygiëne, waarvan de eindpunten direct beschikbaar zijn voor u als u uw activiteiten voor gegevenshygiëne liever automatiseert. Zie de [Handleiding voor API voor gegevenshygiëne](./api/overview.md) voor meer informatie .

## Tijdlijnen en transparantie

Verzoeken voor het verwijderen en verlopen van gegevenssets door de consument hebben elk hun eigen verwerkingstijden en bieden updates voor de transparantie op belangrijke punten in hun respectieve workflows. Raadpleeg de onderstaande secties voor meer informatie over elk taaktype.

### Verlopen gegevensset {#dataset-expiration-transparency}

Het volgende gebeurt wanneer een [Vervalaanvraag gegevensset](./ui/dataset-expiration.md) wordt gemaakt:

| Stage | Tijd na geplande vervaldatum | Beschrijving |
| --- | --- | --- |
| Verzoek is ingediend | 0 uur | Een gegevensbeheerder of privacyanalist dient een verzoek in om een dataset op een bepaald tijdstip te laten verlopen. De aanvraag is zichtbaar in het dialoogvenster [!UICONTROL Data Hygiene UI] nadat de aanvraag is ingediend en in behandeling blijft tot de geplande vervaldatum, waarna de aanvraag zal worden uitgevoerd. |
| Gegevensset wordt verwijderd | 1 uur | De dataset wordt geschrapt van [inventarisatiepagina van gegevensset](../catalog/datasets/user-guide.md) in de gebruikersinterface. De gegevens in het datumpeer worden slechts zachte geschrapt, en zullen zo tot het eind van het proces blijven, waarna het hard zal worden geschrapt. |
| Aantal profielen bijgewerkt | 30 uur | Afhankelijk van de inhoud van de dataset die wordt geschrapt, kunnen sommige profielen uit het systeem worden verwijderd als alle hun componentenattributen aan die dataset worden gebonden. 30 uur nadat de dataset wordt geschrapt, worden om het even welke resulterende veranderingen in algemene profieltellingen weerspiegeld in [dashboardwidgets](../dashboards/guides/profiles.md#profile-count-trend) en andere verslagen. |
| Segmenten bijgewerkt | 48 uur | Wanneer alle betrokken profielen zijn bijgewerkt, worden alle gerelateerde [segmenten](../segmentation/home.md) worden aangepast aan de nieuwe grootte. Afhankelijk van de dataset die werd verwijderd en de attributen die u op segmenteert, zou de grootte van elk segment als gevolg van de schrapping kunnen stijgen of verminderen. |
| Reizen en bestemmingen bijgewerkt | 50 uur | [Reizen](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campagnes](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), en [bestemmingen](../destinations/home.md) worden bijgewerkt op basis van wijzigingen in gerelateerde segmenten. |
| Harde verwijdering voltooid | 14 dagen | Alle gegevens met betrekking tot de gegevensset zijn hard verwijderd uit het datumpeer. De [status van het hygiënisch werk](./ui/browse.md#view-details) die de gegevensset heeft verwijderd, wordt bijgewerkt om deze gegevens weer te geven. |

{style=&quot;table-layout:auto&quot;}

### Verwijderen van consumenten {#consumer-delete-transparency}

Het volgende gebeurt wanneer een [verzoek om verwijdering door consument](./ui/delete-consumer.md) wordt gemaakt:

| Werkgebied | Tijd na indiening van verzoek | Beschrijving |
| --- | --- | --- |
| Verzoek is ingediend | 0 uur | Een gegevensbeheerder of privacyanalist verzendt een aanvraag voor verwijderen door de consument. De aanvraag is zichtbaar in het dialoogvenster [!UICONTROL Data Hygiene UI] nadat zij is ingediend. |
| Profielzoekopdrachten bijgewerkt | 3 uur | De wijziging in het aantal profielen die wordt veroorzaakt door de verwijderde identiteit wordt weerspiegeld in [dashboardwidgets](../dashboards/guides/profiles.md#profile-count-trend) en andere verslagen. |
| Segmenten bijgewerkt | 24 uur | Als profielen eenmaal zijn verwijderd, gelden alle verwante [segmenten](../segmentation/home.md) worden aangepast aan de nieuwe grootte. |
| Reizen en bestemmingen bijgewerkt | 26 uur | [Reizen](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campagnes](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), en [bestemmingen](../destinations/home.md) worden bijgewerkt op basis van wijzigingen in gerelateerde segmenten. |
| Verslagen worden zacht verwijderd in gegevensmeer | 7 dagen | De gegevens worden zacht verwijderd uit het data-meer. |
| Gegevensvacuüm voltooid | 14 dagen | De [status van het hygiënisch werk](./ui/browse.md#view-details) updates om aan te geven dat de taak is voltooid, wat betekent dat het gegevensvacuüm op het datumpeer is voltooid en dat de relevante gegevens hard zijn verwijderd. |

{style=&quot;table-layout:auto&quot;}

## Volgende stappen

Dit document gaf een overzicht van de mogelijkheden van het Platform op het gebied van gegevenshygiëne. Ga naar de [UI-hulplijn](./ui/overview.md). Als u wilt leren hoe u via programmacode taken voor gegevenshygiëne kunt maken, raadpleegt u de [Handleiding voor API voor gegevenshygiëne](./api/overview.md)
