---
title: Schemas in Real-time Customer Data Platform B2B Edition
description: Een overzicht van de rol van de schema's van het Gegevensmodel van de Ervaring (XDM) in de Uitgave van Adobe Real-time Customer Data Platform B2B.
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Schemas in Real-time Customer Data Platform B2B Edition

Adobe Real-time Customer Data Platform B2B Edition biedt verschillende standaarden [Experience Data Model (XDM)-klassen](../../xdm/schema/composition.md#class) die gegevens bevatten over essentiële B2B-gegevensentiteiten, zoals accounts, mogelijkheden, campagnes en meer. Bovendien staat de Uitgave van Real-Time CDP B2B u toe om vele-aan-één verhoudingen tussen deze schema&#39;s te bepalen zodat kunnen zij aan de geavanceerde gevallen van het segmentatiegebruik deelnemen.

>[!IMPORTANT]
>
>U moet toegang hebben tot Real-Time CDP B2B Edition om B2B-schema&#39;s te kunnen gebruiken [Klantprofiel in realtime](../../profile/home.md).

De volgende standaardklassen zijn beschikbaar in Real-Time CDP B2B Edition:

* [XDM Business Account](../../xdm/classes/b2b/business-account.md)
* [XDM Zakelijke account Person Relatie](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md)
* [XDM Business Campaign-leden](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM Business Opportunity](../../xdm/classes/b2b/business-opportunity.md)
* [XDM Business Opportunity Person Relatie](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list.md)
* [Leden van XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list-members.md)

Als u wilt weten hoe schema&#39;s in uw B2B-workflow passen, raadpleegt u de [end-to-end zelfstudie](../b2b-tutorial.md).

Voor stappen op hoe te om een vele-aan-één verhouding tussen twee schema&#39;s tot stand te brengen, verwijs naar het leerprogramma op [B2B-schemarelaties definiëren](../../xdm/tutorials/relationship-b2b.md).

Als u een B2B bronverbinding gebruikt, kunt u een hulpmiddel gebruiken om de vereiste schema&#39;s en de verhoudingen tussen hen automatisch te produceren. Zie de handleiding op [B2B-naamruimten](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) in de documentatie bij de bronnen voor meer informatie.
