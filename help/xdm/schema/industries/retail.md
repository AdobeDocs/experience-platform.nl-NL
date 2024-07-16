---
solution: Experience Platform
title: Gegevensmodel detailhandel
description: Bekijk een gestandaardiseerd gegevensmodel voor de detailhandel, compatibel met het Model van de Gegevens van de Ervaring (XDM) voor gebruik in Adobe Experience Platform.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 5ceb261dbf1cac58d0cfe620875b8fa7c761abf2
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# [!UICONTROL Retail] industriecomputer

Het volgende entiteitsrelatiediagram (ERD) vertegenwoordigt een gestandaardiseerd gegevensmodel voor de detailhandel. De ERD wordt opzettelijk op een gedenormaliseerde wijze gepresenteerd en er wordt rekening mee gehouden hoe gegevens in Adobe Experience Platform worden opgeslagen.

>[!NOTE]
>
>De ERD zoals beschreven is een aanbeveling voor hoe u uw gegevens moet modelleren voor deze branche-gebruikscase. Om van dit gegevensmodel in Platform gebruik te maken, moet u de geadviseerde schema&#39;s en hun verhoudingen zelf construeren. Zie de gidsen bij het beheren van [ schema&#39;s ](../../ui/resources/schemas.md) en [ verhoudingen ](../../tutorials/relationship-ui.md) in UI voor meer informatie.

Gebruik de volgende legenda om dit ERD te interpreteren:

* Elke entiteit die binnen wordt getoond is gebaseerd op een onderliggende [ Model van de Gegevens van de Ervaring (XDM) klasse ](../composition.md#class).
* Voor een bepaalde entiteit, vertegenwoordigt elke rij duidelijk in **gewaagd** een gebiedsgroep of een gegevenstype, met de relevante gebieden het hieronder in unbolded tekst vermeld verstrekt.
* De belangrijkste velden voor een bepaalde entiteit worden rood gemarkeerd.
* Alle eigenschappen die zouden kunnen worden gebruikt om individuele klanten te identificeren zijn duidelijk als &quot;identiteit&quot;, met één van deze eigenschappen duidelijk als &quot;primaire identiteit&quot;.
* Entiteitsrelaties zijn gemarkeerd als niet-afhankelijk, omdat op cookies gebaseerde gebeurtenissen vaak niet kunnen bepalen wie de transactie heeft uitgevoerd.

![](../../images/industries/retail.png)

>[!NOTE]
>
>De Experience Event-entiteit bevat het veld &quot;_ID&quot;, dat het unieke id-kenmerk (`_id`) vertegenwoordigt dat door de XDM ExperienceEvent-klasse wordt verschaft. Zie het verwijzingsdocument op [ XDM ExperienceEvent ](../../classes/experienceevent.md) voor meer details over wat voor deze waarde wordt verwacht.

## [!UICONTROL Retail] gebruik gevallen

De volgende lijst schetst de geadviseerde klassen en de groepen van het schemagebied voor verscheidene gemeenschappelijke detailhandel gebruiksgevallen.

| Gebruiksscenario | Aanbevolen klassen en veldgroepen |
| --- | --- |
| Combineer online en offline gegevensbronnen en los apparaatoverschrijdende en online/offline identiteit op voor holistische rapportage van kanaaloverschrijdende en apparaatoverschrijdende toewijzing. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[ de Details van Commerce ](../../field-groups/event/commerce-details.md)</li><li>[ Details van het Web ](../../field-groups/event/web-details.md)</li></ul></li><li>**[Product](../../classes/product.md)**:<ul><li>[ Catalogus van het Product ](../../field-groups/product/product-catalog.md)</li><li>[ Categorie van het Product ](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Verstrek gerichte en gepersonaliseerde ervaringen voor diverse segmenten om opbrengst te verhogen en het platform in omnichannel orchestratie te helpen verbeteren. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[ de Marketing Details van de Campagne ](../../field-groups/event/campaign-marketing-details.md)</li><li>[ Details van het Kanaal ](../../field-groups/event/channel-details.md)</li><li>[ de Details van Commerce ](../../field-groups/event/commerce-details.md)</li><li>[ Details van het Milieu ](../../field-groups/event/environment-details.md)</li><li>[ Details van het Web ](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM Individueel Profiel](../../classes/individual-profile.md)**:<ul><li>[ Demografische Details ](../../field-groups/profile/demographic-details.md)</li><li>[ Persoonlijke Details van het Contact ](../../field-groups/profile/personal-contact-details.md)</li><li>[ Details van het Contact van het Werk ](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Analyseer multitouch-kenmerk om de marketingefficiëntie te verbeteren. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[ de Marketing Details van de Campagne ](../../field-groups/event/campaign-marketing-details.md)</li><li>[ Details van het Kanaal ](../../field-groups/event/channel-details.md)</li><li>[ de Details van Commerce ](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM Individueel Profiel](../../classes/individual-profile.md)**:<ul><li>[ Demografische Details ](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| Verbeter e-mailrelevantie door betere segmentering van mannen en vrouwen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[ de Details van Commerce ](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM Individueel Profiel](../../classes/individual-profile.md)**:<ul><li>[ Demografische Details ](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**[Product](../../classes/product.md)**:<ul><li>[ Catalogus van het Product ](../../field-groups/product/product-catalog.md)</li><li>[ Categorie van het Product ](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Verhoog loyaliteitsgegevens (partner) om relevante productinformatie over Web, e-mail, en digitale marketing kanalen te verhogen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[ Details van het Web ](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM Individueel Profiel](../../classes/individual-profile.md)**:<ul><li>[ Demografische Details ](../../field-groups/profile/demographic-details.md)</li><li>[ Details van de Loyalty ](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**[Product](../../classes/product.md)**:<ul><li>[ Catalogus van het Product ](../../field-groups/product/product-catalog.md)</li><li>[ Categorie van het Product ](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| Retarget winkelwagentjes verlaten via geautomatiseerde en persoonlijke e-mails. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[ de Details van Commerce ](../../field-groups/event/commerce-details.md)</li><li>[ Details van het Web ](../../field-groups/event/web-details.md)</li></ul></li><li>**[Product](../../classes/product.md)**:<ul><li>[ Catalogus van het Product ](../../field-groups/product/product-catalog.md)</li><li>[ Categorie van het Product ](../../field-groups/product/product-category.md)</li></ul></li></ul> |

{style="table-layout:auto"}
