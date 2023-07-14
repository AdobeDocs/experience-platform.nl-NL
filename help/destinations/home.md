---
keywords: doelen;adobe Experience platform;platform;bestemmingen, overzicht;activate gegevens;activate;
title: Overzicht van doelen
description: Doelen zijn vooraf gebouwde integraties met bestemmingsplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos in te schakelen. Met Doelen in de Adobe Experience Platform kunt u bekende en onbekende gegevens activeren voor marketingcampagnes over meerdere kanalen, e-mailcampagnes, gerichte advertenties en vele andere gebruiksgevallen.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# [!DNL Destinations]-overzicht {#overview}

![Overzicht van doelen banner](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Doelen en bronnen {#destinations-and-sources}

Een van de kernfuncties van Platform is het opnemen van uw gegevens van de eerste partij en het activeren ervan voor uw bedrijfsbehoeften. Gebruiken [bronnen](../sources/home.md) om gegevens in Platform en bestemmingen in te voeren om gegevens uit Platform uit te voeren.

## Doelstappen {#steps}

* Kiezen uit een [zelfbedieningscatalogus](./catalog/overview.md) van alle in Platform beschikbare bestemmingen.
* Gebruik bestemmingen om profielen of publiek naar marketing automatiseringsplatforms, digitale reclameplatforms, en meer te verzenden.
* De gegevens van het programma voeren regelmatig naar uw aangewezen bestemmingen uit.

## Besturingselementen {#controls}

De besturingselementen in de [werkruimte doelen](./ui/destinations-workspace.md) staat u toe:

* Blader door de catalogus met doelplatforms waar u uw gegevens kunt activeren;
* Gegevensstromen naar de doelen in de catalogus maken, bewerken, activeren en uitschakelen;
* Maak een account op een opslaglocatie of koppel een Platform naar de account op het doelplatform;
* Selecteer welk publiek moet worden geactiveerd voor bestemmingen;
* Selecteren [XDM-velden (Experience Data Model)](../xdm/home.md) om te exporteren wanneer een publiek wordt geactiveerd naar marketingbestemmingen via e-mail.

## Doeltypen en -categorieën {#types-and-categories}

Met Experience Platform, kunt u gegevens aan diverse soorten bestemmingen activeren, om aan uw activeringsgebruiksgevallen te voldoen. De bestemmingen variëren van op API-Gebaseerde integratie, tot integratie met dossierontvangstsystemen, de bestemmingen van de profielraadpleging, en meer. Voor gedetailleerde informatie over alle beschikbare bestemmingen, zie [doeltypen en -categorieën, overzicht](./destination-types.md).

## Doelen en toegangscontroles {#access-controls}

De bestemmingsfunctionaliteit in Platform werkt met de toegangsbeheertoestemmingen van Adobe Experience Platform. Afhankelijk van het machtigingsniveau van uw gebruiker, kunt u bestemmingen bekijken, beheren en activeren. Voor informatie over de individuele toestemmingen, zie [Toegangsbeheer in Adobe Experience Platform](../access-control/home.md) en schuift omlaag naar de onderkant van de pagina.

De volgende lijst schetst de toestemmingen en toestemmingscombinaties die worden vereist om bepaalde acties op bestemmingen uit te voeren:

| Machtigingsniveau | Beschrijving |
| ---- | ----|
| **[!UICONTROL Manage Destinations]** | Om met bestemmingen te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). |
| **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** | Om het publiek aan bestemmingen te activeren en toelaat [toewijzingsstap](ui/activate-batch-profile-destinations.md#mapping) van de workflow hebt u de **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). |
| **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL Activate Segments without Mapping]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** | Om het publiek aan bestemmingen te activeren en te verbergen [toewijzingsstap](ui/activate-batch-profile-destinations.md#mapping) van de workflow hebt u de **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL Activate Segments without Mapping]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). |

{style="table-layout:auto"}

Voor meer informatie over toegangscontroles, zie [Gebruikershandleiding voor toegangsbeheer](../access-control/ui/overview.md).

### Op kenmerken gebaseerd toegangsbeheer voor bestemmingen {#attribute-based-access}

Met toegangsbeheer op basis van kenmerken in Adobe Experience Platform kunnen beheerders de toegang tot specifieke objecten en/of mogelijkheden beheren op basis van kenmerken.

Met op attribuut-gebaseerde toegangsbeheer, kunt u toewijzingsconfiguraties op gebieden toepassen die u toestemmingen hebt. Bovendien kunt u geen gegevens naar een bestemming uitvoeren als u geen toegang tot alle gebieden in de dataset hebt.

Voor meer informatie over hoe de bestemmingen met op attribuut-gebaseerde toegangscontroles werken, lees [op attributen-gebaseerd toegangsbeheeroverzicht](../access-control/abac/overview.md#destinations).

## Controle van de bestemmingen {#destinations-monitoring}

Nadat u een verbinding met een doel hebt gemaakt en de activeringsworkflow hebt voltooid, kunt u de gegevens die u exporteert naar uw ontvangstsysteem controleren. Lees de [gids over het controleren van gegevensstromen aan bestemmingen in UI](/help/dataflows/ui/monitor-destinations.md) voor meer informatie .

U kunt ook controleren of gegevens naar uw bestemming zijn gekomen. De meeste doeldocumentatiepagina&#39;s in de catalogus hebben een *Sectie Gegevens exporteren valideren*, die erop wijst hoe u in het bestemmingsplatform kunt controleren dat de gegevens met succes van Experience Platform worden gebracht.

## Beperkingen op gegevensbeheer bij het activeren van gegevens naar bestemmingen {#data-governance}

Het gegevensbeheer wordt afgedwongen voor bestemmingen in de Platform via:

* *Marketingacties* dat u in creeert bestemmingswerkschema kunt selecteren;
* *Beleid voor gegevensgebruik* die de activering van gegevens met bepaalde gebruiksetiketten beperken tot bestemmingen met bepaalde marketingacties.

Zie Gegevensbeheer in de documentatie van het Platform voor meer informatie over [marketingacties](../data-governance/policies/overview.md) en [gegevensbeleidsovertredingen oplossen](../data-governance/enforcement/auto-enforcement.md).

Raadpleeg de volgende pagina&#39;s voor de verschillende doeltypen in het Platform voor meer informatie over het selecteren van marketingacties in de workflow Doel maken:

* [Reclamebestemmingen - Google Ad Manager](./catalog/advertising/google-ad-manager.md)
* [Reclamebestemmingen - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Advertentiebestemmingen - Google Display &amp; Video 360](./catalog/advertising/google-dv360.md)
* [Opslagdoelen voor cloud](./catalog/cloud-storage/overview.md)
* [E-mailmarketingdoelen](./catalog/email-marketing/overview.md)
* [Sociale bestemmingen](./catalog/social/overview.md)

Zie voor meer informatie over schendingen van gegevensbeleid in de workflow voor publiekactivering de **[!UICONTROL Review]** stap in de volgende hulplijnen:

* [De publieksgegevens van de activering aan het stromen publiek de uitvoerbestemmingen](./ui/activate-segment-streaming-destinations.md#review)
* [De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen](./ui/activate-streaming-profile-destinations.md#review)
* [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](./ui/activate-batch-profile-destinations.md#review)
