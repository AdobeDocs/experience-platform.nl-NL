---
title: Schemas in Real-Time Customer Data Platform B2B edition
description: Een overzicht van de rol van de schema's van het Gegevensmodel van de Ervaring (XDM) in Adobe Real-Time Customer Data Platform B2B edition.
feature: Get Started, Data Management, Schemas
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/nl/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 09f671af0d04251ab7b0a71528cb4b9745594b1c
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# Schemas in Real-Time Customer Data Platform B2B edition

Adobe Real-Time Customer Data Platform B2B edition verstrekt verscheidene standaard [&#x200B; klassen van de Gegevens van de Ervaring Model (XDM) &#x200B;](../../xdm/schema/composition.md#class) die details over essentiële B2B gegevensentiteiten, zoals rekeningen, kansen, campagnes, en meer vangen. Bovendien staat Real-Time CDP B2B edition u toe om vele-aan-één verhoudingen tussen deze schema&#39;s te bepalen zodat kunnen zij aan geavanceerde segmentatiegebruikscase deelnemen.

>[!IMPORTANT]
>
>B2B-schema&#39;s zijn beschikbaar voor gebruik in Experience Platform-toepassingen (bijvoorbeeld in [&#x200B; Customer Journey Analytics B2B edition &#x200B;](https://experienceleague.adobe.com/nl/docs/analytics-platform/using/cja-overview/cja-b2b/cja-b2b-edition) ). <br/> Nochtans, moet u toegang tot Real-Time CDP B2B edition hebben opdat (profielen in) B2B- schema&#39;s aan [&#x200B; in real time het Profiel van de Klant &#x200B;](../../profile/home.md) deelnemen.

De volgende standaardklassen zijn beschikbaar in Real-Time CDP B2B edition:

* [XDM Business Account](../../xdm/classes/b2b/business-account.md)
* [XDM Zakelijke account Person Relatie](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md)
* [XDM Business Campaign-leden](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM Business Opportunity](../../xdm/classes/b2b/business-opportunity.md)
* [XDM Business Opportunity Person Relatie](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list.md)
* [Leden van XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list-members.md)

Om te begrijpen hoe schema&#39;s in uw B2B- werkschema passen, gelieve te zien [&#x200B; leerprogramma van begin tot eind &#x200B;](../b2b-tutorial.md).

Voor stappen op hoe te om een vele-aan-één verhouding tussen twee schema&#39;s tot stand te brengen, verwijs naar het leerprogramma op [&#x200B; bepalend B2B schemaverhoudingen &#x200B;](../../xdm/tutorials/relationship-b2b.md).

Als u een B2B bronverbinding gebruikt, kunt u een hulpmiddel gebruiken om de vereiste schema&#39;s en de verhoudingen tussen hen automatisch te produceren. Zie de gids op [&#x200B; B2B namespaces &#x200B;](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) in de brondocumentatie voor meer informatie.
