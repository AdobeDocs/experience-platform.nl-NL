---
title: Talon.One Source - Overzicht
description: Meer informatie over Talon.One-bronnen op Adobe Experience Platform
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: 558a9d6ff3222acbf77edea0a82ef50725cd6203
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 1%

---

# [!DNL Talon.One]

>[!AVAILABILITY]
>
>De bronnen van [!DNL Talon.One] zijn in bèta. Lees de [ termijnen en voorwaarden ](../../home.md#terms-and-conditions) in het bronoverzicht voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Met [!DNL Talon.One] kunt u eenvoudig op maat gemaakte marketingcampagnes maken, beheren en optimaliseren die zijn afgestemd op uw klanten. Gebruik dit krachtige platform om kortingen uit te voeren, coupons te verdelen, verwijzingsprogramma&#39;s te lanceren, loyaliteitsprogramma&#39;s op te zetten, en gamified stimuli aan te bieden - allen van één scalable systeem dat wordt ontworpen om u te helpen uw publiek in dienst nemen en belonen.

U kunt de [!DNL Talon.One] -bronnen in de Adobe Experience Platform-broncatalogus gebruiken om loyaliteitsgegevens voor batches en streaming in te voeren vanuit uw [!DNL Talon.One] -account.

* [Talon.One Streaming Events](../../tutorials/ui/create/loyalty/talon-one-streaming.md)
* [Talon.One Batch Source Connector](../../tutorials/ui/create/loyalty/talon-one-batch.md)

>[!TIP]
>
>Loyaliteitsgegevens hebben betrekking op de informatie van het loyaliteitsprogramma van uw eindgebruikers, zoals loyaliteitspunten, bestede loyaliteitspunten, huidige laag, toegekende coupons, verwijzingen, en prestaties.

## Vereisten {#prerequisites}

Geef waarden op voor de volgende referenties om de [!DNL Talon.One Batch Source Connector] te verifiëren en te verbinden.

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Domein | De unieke URL die aan de toepassingsomgeving van [!DNL Talon.One] is gekoppeld. Zorg ervoor dat u het protocol of pad niet opneemt bij het invoeren van uw domein. | `acmetalonone.us-east4` |
| [!DNL Talon.One] API-beheersleutel | De API-sleutel voor beheer is een referentie voor het verifiëren en autoriseren van toegang tot de API voor beheer van [!DNL Talon.One] . Dit behandelt bewerkingen zoals: <ul><li>coupons importeren</li><li>Campagnegegevens ophalen</li><li>Toepassingen en eindpunten beheren</li></ul> | `ManagementKey-v1 {YOUR_MANAGEMENT_KEY}` |

## Toewijzing {#mapping}

Om u te helpen elk effectobject toe te wijzen op basis van de unieke `effectType` -waarde, kunt u de functie data prep `array_to_map` gebruiken. Zo kunt u een ongeordende array van effecten eenvoudig omzetten in sleutelwaardeparen die aan uw vereisten voldoen. Zie het onderstaande voorbeeld voor hulp.

| Bron | Bestemming |
| ---- | --- |
| `array_to_map(data.effects, "effectType").addLoyaltyPoints.campaignId` | `_{TENANT_ID}.loyalty.pointsGained[0].promotionId` |
| `array_to_map(data.effects, "effectType").addLoyaltyPoints.props.value` | `_{TENANT_ID}.loyalty.pointsGained[0].value` |
| `array_to_map(data.effects, "effectType").deductLoyaltyPoints.campaignId` | `_{TENANT_ID}.loyalty.pointsRedemption[0].promotionId` |
| `array_to_map(data.effects, "effectType").acceptCoupon.campaignId` | `_{TENANT_ID}.loyalty.couponRedemption[0].campaignId` |
| `array_to_map(data.effects, "effectType").deductLoyaltyPoints.props.value` | `_{TENANT_ID}.loyalty.pointsRedemption[0].value` |
| `array_to_map(data.effects, "effectType").acceptCoupon.props.value` | `_{TENANT_ID}.loyalty.couponRedemption[0].id` |
| `array_to_map(data.effects, "effectType").setDiscount.campaignId` | `_{TENANT_ID}.loyalty.discounts[0].promotionId` |
| `array_to_map(data.effects, "effectType").setDiscount.props.value` | `_{TENANT_ID}.loyalty.discounts[0].value` |
| `data.created` | `timestamp` |
| `data.attributes.params.profileId` | `personID` |
| `data.attributes.integrationId` | `_id` |
| `data.attributes.params.cartItems[*].name` | `productListItems[*].name` |
| `data.attributes.params.cartItems[*].category` | `productListItems[*].productCategories[0].categoryID` |
| `data.attributes.params.cartItems[*].sku` | `productListItems[*].SKU` |

{style="table-layout:auto"}

## Volgende stappen

Lees de volgende documentatie voor meer informatie over hoe u uw [!DNL Talon.One] -account kunt verbinden met Experience Platform en hoe u loyaliteitsgegevens voor batches en streaming kunt invoeren.

* [Talon.One Streaming Events](../../tutorials/ui/create/loyalty/talon-one-streaming.md)
* [Talon.One Batch Source Connector](../../tutorials/ui/create/loyalty/talon-one-batch.md)