---
solution: Experience Platform
title: Gegevensmodel detailhandel
topic-legacy: overview
description: Bekijk een gestandaardiseerd gegevensmodel voor de detailhandel, compatibel met het Model van de Gegevens van de Ervaring (XDM) voor gebruik in Adobe Experience Platform.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 9c5a4e064af0b46ff30b41afef71ca2fd3503a82
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# [!UICONTROL Retail] bedrijfsgegevensmodel

Het volgende entiteitsrelatiediagram (ERD) vertegenwoordigt een gestandaardiseerd gegevensmodel voor de detailhandel. De ERD wordt opzettelijk op een gedenormaliseerde wijze gepresenteerd en er wordt rekening mee gehouden hoe gegevens in Adobe Experience Platform worden opgeslagen.

Gebruik de volgende legenda om dit ERD te interpreteren:

* Elke entiteit die in wordt getoond is gebaseerd op een onderliggende [Klasse van het Gegevensmodel van de Ervaring (XDM)](../composition.md#class).
* Voor een bepaalde entiteit vertegenwoordigt elke rij die in **bold** wordt gemarkeerd, een veldgroep of een gegevenstype, met de relevante velden die hieronder in onbolle tekst worden weergegeven.
* De belangrijkste velden voor een bepaalde entiteit worden rood gemarkeerd.
* Alle eigenschappen die zouden kunnen worden gebruikt om individuele klanten te identificeren zijn duidelijk als &quot;identiteit&quot;, met één van deze eigenschappen duidelijk als &quot;primaire identiteit&quot;.
* Entiteitsrelaties zijn gemarkeerd als niet-afhankelijk, omdat op cookies gebaseerde gebeurtenissen vaak niet kunnen bepalen wie de transactie heeft uitgevoerd.

![](../../images/industries/retail.png)

>[!NOTE]
>
>De Experience Event-entiteit bevat het veld &quot;_ID&quot;, dat het unieke id-kenmerk (`_id`) vertegenwoordigt dat door de XDM ExperienceEvent-klasse wordt verschaft. Zie het referentiedocument op [XDM ExperienceEvent](../../classes/experienceevent.md) voor meer details over wat voor deze waarde wordt verwacht.

## [!UICONTROL Retail] use cases

De volgende lijst schetst de geadviseerde klassen en de groepen van het schemagebied voor verscheidene gemeenschappelijke detailhandel gebruiksgevallen.

| Gebruiksscenario | Aanbevolen klassen en veldgroepen |
| --- | --- |
| Combineer online en offline gegevensbronnen en los apparaatoverschrijdende en online/offline identiteit op voor holistische rapportage van kanaaloverschrijdende en apparaatoverschrijdende toewijzing. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Handelsgegevens](../../field-groups/event/commerce-details.md)</li><li>[Webdetails](../../field-groups/event/web-details.md)</li></ul></li><li>**Product**  (aangepaste klasse)\*:<ul><li>Product (aangepaste veldgroep)\*</li></ul></li></ul> |
| Verstrek gerichte en gepersonaliseerde ervaringen voor diverse segmenten om opbrengst te verhogen en het platform in omnichannel orchestratie te helpen verbeteren. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Campagne marketing details](../../field-groups/event/campaign-marketing-details.md)</li><li>[Kanaaldetails](../../field-groups/event/channel-details.md)</li><li>[Handelsgegevens](../../field-groups/event/commerce-details.md)</li><li>[Omgevingsdetails](../../field-groups/event/environment-details.md)</li><li>[Webdetails](../../field-groups/event/web-details.md)</li></ul></li><li>**[Afzonderlijk XDM-profiel](../../classes/individual-profile.md)**:<ul><li>[Demografische details](../../field-groups/profile/demographic-details.md)</li><li>[Persoonlijke contactgegevens](../../field-groups/profile/personal-contact-details.md)</li><li>[Contactgegevens werken](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Analyseer multitouch-kenmerk om de marketingefficiëntie te verbeteren. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Campagne marketing details](../../field-groups/event/campaign-marketing-details.md)</li><li>[Kanaaldetails](../../field-groups/event/channel-details.md)</li><li>[Handelsgegevens](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Afzonderlijk XDM-profiel](../../classes/individual-profile.md)**:<ul><li>[Demografische details](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| Verbeter e-mailrelevantie door betere segmentering van mannen en vrouwen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Handelsgegevens](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[Afzonderlijk XDM-profiel](../../classes/individual-profile.md)**:<ul><li>[Demografische details](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**Product**  (aangepaste klasse)\*:<ul><li>Product (aangepaste veldgroep)\*</li></ul></li></ul> |
| Verhoog loyaliteitsgegevens (partner) om relevante productinformatie over Web, e-mail, en digitale marketing kanalen te verhogen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Webdetails](../../field-groups/event/web-details.md)</li></ul></li><li>**[Afzonderlijk XDM-profiel](../../classes/individual-profile.md)**:<ul><li>[Demografische details](../../field-groups/profile/demographic-details.md)</li><li>[Loyalty-details](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**Product**  (aangepaste klasse)\*:<ul><li>Product (aangepaste veldgroep)\*</li></ul></li></ul> |
| Retarget winkelwagentjes verlaten via geautomatiseerde en persoonlijke e-mails. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Handelsgegevens](../../field-groups/event/commerce-details.md)</li><li>[Webdetails](../../field-groups/event/web-details.md)</li></ul></li><li>**Product**  (aangepaste klasse)\*:<ul><li>Product (aangepaste veldgroep)\*</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}

*\*Hoewel een standaardproductklasse voor een toekomstige versie gepland is, moeten de productschema&#39;s momenteel worden gebouwd gebruikend een douaneklasse in plaats daarvan. Daarom moet u de structuur van de klasse van het schema, evenals die van om het even welke gebiedsgroepen manueel bouwen u aan het toevoegt. Zie de sectie over [het creëren van een douaneklasse](../../ui/resources/classes.md#create) in de gids XDM UI voor meer informatie.*
