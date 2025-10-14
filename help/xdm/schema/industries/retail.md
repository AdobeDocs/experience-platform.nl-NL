---
solution: Experience Platform
title: Gegevensmodel detailhandel
description: Bekijk een gestandaardiseerd gegevensmodel voor de detailhandel, compatibel met het Model van de Gegevens van de Ervaring (XDM) voor gebruik in Adobe Experience Platform.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# [!UICONTROL Retail] industriecomputer

Het volgende entiteitsrelatiediagram (ERD) vertegenwoordigt een gestandaardiseerd gegevensmodel voor de detailhandel. De ERD wordt opzettelijk op een gedenormaliseerde wijze gepresenteerd en er wordt rekening mee gehouden hoe gegevens in Adobe Experience Platform worden opgeslagen.

>[!NOTE]
>
>De ERD zoals beschreven is een aanbeveling voor hoe u uw gegevens moet modelleren voor deze branche-gebruikscase. Om van dit gegevensmodel in Experience Platform gebruik te maken, moet u de geadviseerde schema&#39;s en hun verhoudingen zelf construeren. Zie de gidsen bij het beheren van [&#x200B; schema&#39;s &#x200B;](../../ui/resources/schemas.md) en [&#x200B; verhoudingen &#x200B;](../../tutorials/relationship-ui.md) in UI voor meer informatie.

Gebruik de volgende legenda om dit ERD te interpreteren:

* Elke entiteit die binnen wordt getoond is gebaseerd op een onderliggende [&#x200B; Model van de Gegevens van de Ervaring (XDM) klasse &#x200B;](../composition.md#class).
* Velden die onder een bovenliggend veld zijn ingesprongen, vertegenwoordigen een onderliggend veld, of subveld, dat tot de veldgroep van het bovenliggende veld behoort.
* De belangrijkste velden voor een bepaalde entiteit worden rood gemarkeerd.
* Alle eigenschappen die zouden kunnen worden gebruikt om individuele klanten te identificeren zijn duidelijk als &quot;identiteit&quot;, met één van deze eigenschappen duidelijk als &quot;primaire identiteit&quot;.
* Entiteitsrelaties zijn gemarkeerd als niet-afhankelijk, omdat op cookies gebaseerde gebeurtenissen vaak niet kunnen bepalen wie de transactie heeft uitgevoerd.

![&#x200B; een voorbeeldERD voor een model van de detailhandelindustrie gegevens &#x200B;](../../images/industries/retail.png)

>[!NOTE]
>
>De Experience Event-entiteit bevat het veld &quot;_ID&quot;, dat het unieke id-kenmerk (`_id`) vertegenwoordigt dat door de XDM ExperienceEvent-klasse wordt verschaft. Zie het verwijzingsdocument op [&#x200B; XDM ExperienceEvent &#x200B;](../../classes/experienceevent.md) voor meer details over wat voor deze waarde wordt verwacht.

## [!UICONTROL Retail] gebruik gevallen

De volgende lijst schetst de geadviseerde klassen en de groepen van het schemagebied voor verscheidene gemeenschappelijke detailhandel gebruiksgevallen.

| Gebruiksscenario | Aanbevolen klassen en veldgroepen |
| --- | --- |
| Combineer online en offline gegevensbronnen en los apparaatoverschrijdende en online/offline identiteit op voor holistische rapportage van kanaaloverschrijdende en apparaatoverschrijdende toewijzing. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[&#x200B; de Details van Commerce &#x200B;](../../field-groups/event/commerce-details.md)</li><li>[&#x200B; Details van het Web &#x200B;](../../field-groups/event/web-details.md)</li></ul></li><li>**[Product](../../classes/product.md)**:<ul><li>[&#x200B; Catalogus van het Product &#x200B;](../../field-groups/product/product-catalog.md)</li><li>[&#x200B; Categorie van het Product &#x200B;](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Verstrek gerichte en gepersonaliseerde ervaringen voor diverse segmenten om opbrengst te verhogen en het platform in omnichannel orchestratie te helpen verbeteren. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[&#x200B; de Marketing Details van de Campagne &#x200B;](../../field-groups/event/campaign-marketing-details.md)</li><li>[&#x200B; Details van het Kanaal &#x200B;](../../field-groups/event/channel-details.md)</li><li>[&#x200B; de Details van Commerce &#x200B;](../../field-groups/event/commerce-details.md)</li><li>[&#x200B; Details van het Milieu &#x200B;](../../field-groups/event/environment-details.md)</li><li>[&#x200B; Details van het Web &#x200B;](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM Individueel Profiel](../../classes/individual-profile.md)**:<ul><li>[&#x200B; Demografische Details &#x200B;](../../field-groups/profile/demographic-details.md)</li><li>[&#x200B; Persoonlijke Details van het Contact &#x200B;](../../field-groups/profile/personal-contact-details.md)</li><li>[&#x200B; Details van het Contact van het Werk &#x200B;](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Analyseer multitouch-kenmerk om de marketingefficiëntie te verbeteren. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[&#x200B; de Marketing Details van de Campagne &#x200B;](../../field-groups/event/campaign-marketing-details.md)</li><li>[&#x200B; Details van het Kanaal &#x200B;](../../field-groups/event/channel-details.md)</li><li>[&#x200B; de Details van Commerce &#x200B;](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM Individueel Profiel](../../classes/individual-profile.md)**:<ul><li>[&#x200B; Demografische Details &#x200B;](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| Verbeter e-mailrelevantie door betere segmentering van mannen en vrouwen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[&#x200B; de Details van Commerce &#x200B;](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM Individueel Profiel](../../classes/individual-profile.md)**:<ul><li>[&#x200B; Demografische Details &#x200B;](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**[Product](../../classes/product.md)**:<ul><li>[&#x200B; Catalogus van het Product &#x200B;](../../field-groups/product/product-catalog.md)</li><li>[&#x200B; Categorie van het Product &#x200B;](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Verhoog loyaliteitsgegevens (partner) om relevante productinformatie over Web, e-mail, en digitale marketing kanalen te verhogen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[&#x200B; Details van het Web &#x200B;](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM Individueel Profiel](../../classes/individual-profile.md)**:<ul><li>[&#x200B; Demografische Details &#x200B;](../../field-groups/profile/demographic-details.md)</li><li>[&#x200B; Details van de Loyalty &#x200B;](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**[Product](../../classes/product.md)**:<ul><li>[&#x200B; Catalogus van het Product &#x200B;](../../field-groups/product/product-catalog.md)</li><li>[&#x200B; Categorie van het Product &#x200B;](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Retarget winkelwagentjes verlaten via geautomatiseerde en persoonlijke e-mails. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[&#x200B; de Details van Commerce &#x200B;](../../field-groups/event/commerce-details.md)</li><li>[&#x200B; Details van het Web &#x200B;](../../field-groups/event/web-details.md)</li></ul></li><li>**[Product](../../classes/product.md)**:<ul><li>[&#x200B; Catalogus van het Product &#x200B;](../../field-groups/product/product-catalog.md)</li><li>[&#x200B; Categorie van het Product &#x200B;](../../field-groups/product/product-category.md)</li></ul></li></ul> |

{style="table-layout:auto"}
