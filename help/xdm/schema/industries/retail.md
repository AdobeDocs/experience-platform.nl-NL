---
solution: Experience Platform
title: Gegevensmodel detailhandel
topic-legacy: overview
description: Bekijk een gestandaardiseerd gegevensmodel voor de detailhandel, compatibel met het Model van de Gegevens van de Ervaring (XDM) voor gebruik in Adobe Experience Platform.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 2d7314f11837ca5c5ca1411553f20f58c4cad1ec
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 1%

---

# [!UICONTROL Retail] bedrijfsgegevensmodel

Het volgende entiteitsrelatiediagram (ERD) vertegenwoordigt een gestandaardiseerd gegevensmodel voor de detailhandel. De ERD wordt opzettelijk op een gedenormaliseerde wijze gepresenteerd en er wordt rekening mee gehouden hoe gegevens in Adobe Experience Platform worden opgeslagen.

>[!NOTE]
>
>De ERD zoals beschreven is een aanbeveling voor hoe u uw gegevens moet modelleren voor deze branche-gebruikscase. Om van dit gegevensmodel in Platform gebruik te maken, moet u de geadviseerde schema&#39;s en hun verhoudingen zelf construeren. Zie de handleidingen over het beheer [schema&#39;s](../../ui/resources/schemas.md) en [relaties](../../tutorials/relationship-ui.md) in UI voor meer informatie.

Gebruik de volgende legenda om dit ERD te interpreteren:

* Elke entiteit die wordt vermeld in is gebaseerd op een onderliggende waarde [Experience Data Model (XDM)-klasse](../composition.md#class).
* Voor een bepaalde entiteit wordt elke in **vet** vertegenwoordigt een veldgroep of een gegevenstype, waarvan de relevante velden hieronder in onbolde tekst worden vermeld.
* De belangrijkste velden voor een bepaalde entiteit worden rood gemarkeerd.
* Alle eigenschappen die zouden kunnen worden gebruikt om individuele klanten te identificeren zijn duidelijk als &quot;identiteit&quot;, met één van deze eigenschappen duidelijk als &quot;primaire identiteit&quot;.
* Entiteitsrelaties zijn gemarkeerd als niet-afhankelijk, omdat op cookies gebaseerde gebeurtenissen vaak niet kunnen bepalen wie de transactie heeft uitgevoerd.

![](../../images/industries/retail.png)

>[!NOTE]
>
>De Experience Event-entiteit bevat het veld &quot;_ID&quot;, dat de unieke id vertegenwoordigt (`_id`), opgegeven door de klasse XDM ExperienceEvent. Zie het referentiedocument op [XDM ExperienceEvent](../../classes/experienceevent.md) voor meer informatie over wat er voor deze waarde wordt verwacht.

## [!UICONTROL Retail] use cases

De volgende lijst schetst de geadviseerde klassen en de groepen van het schemagebied voor verscheidene gemeenschappelijke detailhandel gebruiksgevallen.

| Gebruiksscenario | Aanbevolen klassen en veldgroepen |
| --- | --- |
| Combineer online en offline gegevensbronnen en los apparaatoverschrijdende en online/offline identiteit op voor holistische rapportage van kanaaloverschrijdende en apparaatoverschrijdende toewijzing. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Handelsgegevens](../../field-groups/event/commerce-details.md)</li><li>[Webdetails](../../field-groups/event/web-details.md)</li></ul></li><li>**[Product](../../classes/product.md)**:<ul><li>[Productcatalogus](../../field-groups/product/product-catalog.md)</li><li>[Productcategorie](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Verstrek gerichte en gepersonaliseerde ervaringen voor diverse segmenten om opbrengst te verhogen en het platform in omnichannel orchestratie te helpen verbeteren. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Campagne marketing details](../../field-groups/event/campaign-marketing-details.md)</li><li>[Kanaaldetails](../../field-groups/event/channel-details.md)</li><li>[Handelsgegevens](../../field-groups/event/commerce-details.md)</li><li>[Omgevingsdetails](../../field-groups/event/environment-details.md)</li><li>[Webdetails](../../field-groups/event/web-details.md)</li></ul></li><li>**[Afzonderlijk XDM-profiel](../../classes/individual-profile.md)**:<ul><li>[Demografische details](../../field-groups/profile/demographic-details.md)</li><li>[Persoonlijke contactgegevens](../../field-groups/profile/personal-contact-details.md)</li><li>[Contactgegevens werken](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Analyseer multitouch-kenmerk om de marketingefficiëntie te verbeteren. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Campagne marketing details](../../field-groups/event/campaign-marketing-details.md)</li><li>[Kanaaldetails](../../field-groups/event/channel-details.md)</li><li>[Handelsgegevens](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Afzonderlijk XDM-profiel](../../classes/individual-profile.md)**:<ul><li>[Demografische details](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| Verbeter e-mailrelevantie door betere segmentering van mannen en vrouwen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Handelsgegevens](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Afzonderlijk XDM-profiel](../../classes/individual-profile.md)**:<ul><li>[Demografische details](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**[Product](../../classes/product.md)**:<ul><li>[Productcatalogus](../../field-groups/product/product-catalog.md)</li><li>[Productcategorie](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Verhoog loyaliteitsgegevens (partner) om relevante productinformatie over Web, e-mail, en digitale marketing kanalen te verhogen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Webdetails](../../field-groups/event/web-details.md)</li></ul></li><li>**[Afzonderlijk XDM-profiel](../../classes/individual-profile.md)**:<ul><li>[Demografische details](../../field-groups/profile/demographic-details.md)</li><li>[Loyalty-details](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**[Product](../../classes/product.md)**:<ul><li>[Productcatalogus](../../field-groups/product/product-catalog.md)</li><li>[Productcategorie](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Retarget winkelwagentjes verlaten via geautomatiseerde en persoonlijke e-mails. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Handelsgegevens](../../field-groups/event/commerce-details.md)</li><li>[Webdetails](../../field-groups/event/web-details.md)</li></ul></li><li>**[Product](../../classes/product.md)**:<ul><li>[Productcatalogus](../../field-groups/product/product-catalog.md)</li><li>[Productcategorie](../../field-groups/product/product-category.md)</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}

*\*Hoewel een standaardproductklasse voor een toekomstige versie gepland is, moeten de productschema&#39;s momenteel worden gebouwd gebruikend een douaneklasse in plaats daarvan. Daarom moet u de structuur van de klasse van het schema, evenals die van om het even welke gebiedsgroepen manueel bouwen u aan het toevoegt. Zie de sectie over [een aangepaste klasse maken](../../ui/resources/classes.md#create) in de XDM UI-handleiding voor meer informatie.*
