---
title: Schemas in Real-time Customer Data Platform B2B Edition (bèta)
description: Een overzicht van de rol van de schema's van het Gegevensmodel van de Ervaring (XDM) in de Uitgave van Real-time Customer Data Platform B2B.
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 6f421a8ae77318ca2598d640cf7e27ea485ec9db
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Schemas in Real-time Customer Data Platform B2B Edition (bèta)

>[!IMPORTANT]
>
>Real-time Customer Data Platform B2B Edition is momenteel in bèta. De documentatie en functionaliteit kunnen worden gewijzigd.

Real-time Customer Data Platform B2B Edition biedt verschillende standaarden [Experience Data Model (XDM)-klassen](../../xdm/schema/composition.md#class) die gegevens bevatten over essentiële B2B-gegevensentiteiten, zoals accounts, mogelijkheden, campagnes en meer. Bovendien in real time CDP B2B Uitgave staat u toe om vele-aan-één verhoudingen tussen deze schema&#39;s te bepalen zodat kunnen zij aan de geavanceerde gevallen van het segmentatiegebruik deelnemen.

De volgende standaardklassen worden verstrekt in Echt - tijd CDP B2B Uitgave:

* [XDM Business Account](../../xdm/classes/b2b/business-account.md)
* [XDM Zakelijke account Person Relatie](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md)
* [XDM Business Campaign-leden](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM Business Opportunity](../../xdm/classes/b2b/business-opportunity.md)
* [XDM Business Opportunity Person Relatie](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list.md)
* [Leden van XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list-members.md)

Voor stappen op hoe te om een vele-aan-één verhouding tussen twee schema&#39;s tot stand te brengen, verwijs naar het leerprogramma op [B2B-schemarelaties definiëren](../../xdm/tutorials/relationship-b2b.md).

Als u een B2B bronverbinding gebruikt, kunt u een hulpmiddel gebruiken om de vereiste schema&#39;s en de verhoudingen tussen hen automatisch te produceren. Zie de handleiding op [B2B-naamruimten](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) in de documentatie bij de bronnen voor meer informatie.
