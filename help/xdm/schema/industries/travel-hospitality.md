---
solution: Experience Platform
title: Reis- en ziekenhuisgegevensmodel ERD
description: Bekijk een diagram van de entiteitverhouding (ERD) dat een gestandaardiseerd gegevensmodel voor de reis en gastvrijheid industrie beschrijft, compatibel met het Model van de Gegevens van de Ervaring (XDM) voor gebruik in Adobe Experience Platform.
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# [!UICONTROL Travel and hospitality] industrie gegevensmodel ERD

Het volgende entiteitsrelatiediagram (ERD) vertegenwoordigt een gestandaardiseerd gegevensmodel voor de reis- en gastindustrie. De ERD wordt opzettelijk op een gedenormaliseerde wijze gepresenteerd en er wordt rekening mee gehouden hoe gegevens in Adobe Experience Platform worden opgeslagen.

>[!NOTE]
>
>De ERD zoals beschreven is een aanbeveling voor hoe u uw gegevens moet modelleren voor deze branche-gebruikscase. Om van dit gegevensmodel in Platform gebruik te maken, moet u de geadviseerde schema&#39;s en hun verhoudingen zelf construeren. Zie de gidsen bij het beheren van [ schema&#39;s ](../../ui/resources/schemas.md) en [ verhoudingen ](../../tutorials/relationship-ui.md) in UI voor meer informatie.

Gebruik de volgende legenda om dit ERD te interpreteren:

* Elke entiteit die binnen wordt getoond is gebaseerd op een onderliggende [ Model van de Gegevens van de Ervaring (XDM) klasse ](../composition.md#class).
* Voor een bepaalde entiteit, vertegenwoordigt elke rij duidelijk in **gewaagd** een gebiedsgroep of een gegevenstype, met de relevante gebieden het hieronder in unbolded tekst vermeld verstrekt.
* De belangrijkste velden voor een bepaalde entiteit worden rood gemarkeerd.
* Alle eigenschappen die zouden kunnen worden gebruikt om individuele klanten te identificeren zijn duidelijk als &quot;identiteit&quot;, met één van deze eigenschappen duidelijk als &quot;primaire identiteit&quot;.
* Entiteitsrelaties zijn gemarkeerd als niet-afhankelijk, omdat op cookies gebaseerde gebeurtenissen vaak niet kunnen bepalen wie de transactie heeft uitgevoerd.

![](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>De Experience Event-entiteit bevat het veld &quot;_ID&quot;, dat het unieke id-kenmerk (`_id`) vertegenwoordigt dat door de XDM ExperienceEvent-klasse wordt verschaft. Zie het verwijzingsdocument op [ XDM ExperienceEvent ](../../classes/experienceevent.md) voor meer details over wat voor deze waarde wordt verwacht.

## [!UICONTROL Travel and hospitality] gebruik gevallen

De volgende lijst schetst de geadviseerde klassen en de groepen van het schemagebied voor verscheidene gemeenschappelijke gebruiksgevallen voor de reis en gastvrijheid industrie.

| Gebruiksscenario | Aanbevolen klassen en veldgroepen |
| --- | --- |
| Cross-sell dining en andere inwoner attracties voor gasten en gasten op de markt met komende hotelreserveringen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[ Details van de Voorbehoud ](../../field-groups/event/reservation-details.md)</li><li>[ Lodging Reservering ](../../field-groups/event/lodging-reservation.md)</li><li>[ het Dining Voorbehoud ](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM Individueel Profiel](../../classes/individual-profile.md)**:<ul><li>[ Demografische Details ](../../field-groups/profile/demographic-details.md)</li><li>[ Persoonlijke Details van het Contact ](../../field-groups/profile/personal-contact-details.md)</li><li>[ Details van het Contact van het Werk ](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| Aankoop van eetgewoonten en andere trekpleisters voor gasten en gasten die in de handel zijn en een hotelreservering krijgen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[ Details van de Voorbehoud ](../../field-groups/event/reservation-details.md)</li><li>[ het Dining Voorbehoud ](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM Individueel Profiel](../../classes/individual-profile.md)**:<ul><li>[ Demografische Details ](../../field-groups/profile/demographic-details.md)</li><li>[ Persoonlijke Details van het Contact ](../../field-groups/profile/personal-contact-details.md)</li><li>[ Details van het Contact van het Werk ](../../field-groups/profile/work-contact-details.md)</li><li>[ Details van de Loyalty ](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Hotels en andere in het land wonende attracties voor gasten en gasten op de markt met aankomende hotelreserveringen verkopen. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[ Details van de Voorbehoud ](../../field-groups/event/reservation-details.md)</li><li>[ Lodging Reservering ](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[XDM Individueel Profiel](../../classes/individual-profile.md)**:<ul><li>[ Demografische Details ](../../field-groups/profile/demographic-details.md)</li><li>[ Persoonlijke Details van het Contact ](../../field-groups/profile/personal-contact-details.md)</li><li>[ Details van het Contact van het Werk ](../../field-groups/profile/work-contact-details.md)</li><li>[ Details van de Loyalty ](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| Up-sell-vluchten en andere in het land gevestigde attracties voor gasten en gasten die in de handel zijn en binnenkort een hotelreservering hebben. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[ Details van de Voorbehoud ](../../field-groups/event/reservation-details.md)</li><li>[ Voorbehoud van de Vlucht ](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[XDM Individueel Profiel](../../classes/individual-profile.md)**:<ul><li>[ Demografische Details ](../../field-groups/profile/demographic-details.md)</li><li>[ Persoonlijke Details van het Contact ](../../field-groups/profile/personal-contact-details.md)</li><li>[ Details van het Contact van het Werk ](../../field-groups/profile/work-contact-details.md)</li><li>[ Details van de Loyalty ](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
