---
solution: Experience Platform
title: Reis- en ziekenhuisgegevensmodel ERD
description: Bekijk een diagram van de entiteitverhouding (ERD) dat een gestandaardiseerd gegevensmodel voor de reis en gastvrijheid industrie beschrijft, compatibel met het Model van de Gegevens van de Ervaring (XDM) voor gebruik in Adobe Experience Platform.
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# [!UICONTROL Travel and hospitality] bedrijfsgegevensmodel ERD

Het volgende entiteitsrelatiediagram (ERD) vertegenwoordigt een gestandaardiseerd gegevensmodel voor de reis- en gastindustrie. De ERD wordt opzettelijk op een gedenormaliseerde wijze gepresenteerd en er wordt rekening mee gehouden hoe gegevens in Adobe Experience Platform worden opgeslagen.

>[!NOTE]
>
>De ERD zoals beschreven is een aanbeveling voor hoe u uw gegevens moet modelleren voor deze branche-gebruikscase. Om van dit gegevensmodel in Platform gebruik te maken, moet u de geadviseerde schema&#39;s en hun verhoudingen zelf construeren. Zie de handleidingen over het beheer [schema&#39;s](../../ui/resources/schemas.md) en [relaties](../../tutorials/relationship-ui.md) in UI voor meer informatie.

Gebruik de volgende legenda om dit ERD te interpreteren:

* Elke entiteit die wordt vermeld in is gebaseerd op een onderliggende waarde [Experience Data Model (XDM)-klasse](../composition.md#class).
* Voor een bepaalde entiteit wordt elke in **vet** vertegenwoordigt een veldgroep of een gegevenstype, waarvan de relevante velden hieronder in onbolde tekst worden vermeld.
* De belangrijkste velden voor een bepaalde entiteit worden rood gemarkeerd.
* Alle eigenschappen die zouden kunnen worden gebruikt om individuele klanten te identificeren zijn duidelijk als &quot;identiteit&quot;, met één van deze eigenschappen duidelijk als &quot;primaire identiteit&quot;.
* Entiteitsrelaties zijn gemarkeerd als niet-afhankelijk, omdat op cookies gebaseerde gebeurtenissen vaak niet kunnen bepalen wie de transactie heeft uitgevoerd.

![](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>De Experience Event-entiteit bevat het veld &quot;_ID&quot;, dat de unieke id vertegenwoordigt (`_id`), opgegeven door de klasse XDM ExperienceEvent. Zie het referentiedocument op [XDM ExperienceEvent](../../classes/experienceevent.md) voor meer informatie over wat er voor deze waarde wordt verwacht.

## [!UICONTROL Travel and hospitality] use cases

De volgende lijst schetst de geadviseerde klassen en de groepen van het schemagebied voor verscheidene gemeenschappelijke gebruiksgevallen voor de reis en gastvrijheid industrie.

| Gebruiksscenario | Aanbevolen klassen en veldgroepen |
| --- | --- |
| Cross-sell dining en andere inwoner attracties voor gasten en gasten op de markt met komende hotelreserveringen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Reserveringsdetails](../../field-groups/event/reservation-details.md)</li><li>[Voorbehoud voor indiening](../../field-groups/event/lodging-reservation.md)</li><li>[Mijnreservering](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[Afzonderlijk XDM-profiel](../../classes/individual-profile.md)**:<ul><li>[Demografische details](../../field-groups/profile/demographic-details.md)</li><li>[Persoonlijke contactgegevens](../../field-groups/profile/personal-contact-details.md)</li><li>[Contactgegevens werken](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Aankoop van eetgewoonten en andere trekpleisters voor gasten en gasten die in de handel zijn en een hotelreservering krijgen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Reserveringsdetails](../../field-groups/event/reservation-details.md)</li><li>[Mijnreservering](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[Afzonderlijk XDM-profiel](../../classes/individual-profile.md)**:<ul><li>[Demografische details](../../field-groups/profile/demographic-details.md)</li><li>[Persoonlijke contactgegevens](../../field-groups/profile/personal-contact-details.md)</li><li>[Contactgegevens werken](../../field-groups/profile/work-contact-details.md)</li><li>[Loyalty-details](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Hotels en andere in het land wonende attracties voor gasten en gasten op de markt met aankomende hotelreserveringen verkopen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Reserveringsdetails](../../field-groups/event/reservation-details.md)</li><li>[Voorbehoud voor indiening](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[Afzonderlijk XDM-profiel](../../classes/individual-profile.md)**:<ul><li>[Demografische details](../../field-groups/profile/demographic-details.md)</li><li>[Persoonlijke contactgegevens](../../field-groups/profile/personal-contact-details.md)</li><li>[Contactgegevens werken](../../field-groups/profile/work-contact-details.md)</li><li>[Loyalty-details](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Up-sell-vluchten en andere in het land gevestigde attracties voor gasten en gasten die in de handel zijn en binnenkort een hotelreservering hebben. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Reserveringsdetails](../../field-groups/event/reservation-details.md)</li><li>[Vluchtreservering](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[Afzonderlijk XDM-profiel](../../classes/individual-profile.md)**:<ul><li>[Demografische details](../../field-groups/profile/demographic-details.md)</li><li>[Persoonlijke contactgegevens](../../field-groups/profile/personal-contact-details.md)</li><li>[Contactgegevens werken](../../field-groups/profile/work-contact-details.md)</li><li>[Loyalty-details](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}
