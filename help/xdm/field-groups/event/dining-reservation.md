---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schema-ontwerp;veldgroep;field-groep;reservering;dining;
title: Veldengroep voor denningsreservatieschema
description: Meer informatie over de veldgroep Dining Reservation Schema.
exl-id: 672b7a77-c433-4502-a1ad-a17c811b253e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# [!UICONTROL Dining Reservation] schemaveldgroep

[!UICONTROL Dining Reservation] is een standaardgroep van het schemagebied voor de [[!DNL XDM ExperienceEvent]  klasse &#x200B;](../../classes/experienceevent.md) wordt gebruikt om informatie betreffende een het dineren reserve te vangen die.

De veldgroep is een extensie van de veldgroep [!UICONTROL Reservation Details] en bevat dezelfde velden onder één objecttype, `reservations` . Naast deze algemene velden bevat [!UICONTROL Dining Reservation] ook `diningReservations` array. Deze array met objecten wordt gebruikt om een of meer reserveringen met restaurantspecifieke eigenschappen te beschrijven.

>[!NOTE]
>
>In dit document worden de details van de array `diningReservations` besproken. Voor informatie over de andere gebieden die onder het `reservations` voorwerp worden verstrekt, gelieve te verwijzen naar [[!UICONTROL Reservation Details] de verwijzing van de gebiedsgroep &#x200B;](./reservation-details.md).

![&#x200B; het Dining de structuur van de Voorbehoud &#x200B;](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` is een array met objecten die een lijst met diningsreserveringen vertegenwoordigt. Als een reserveringsgebeurtenis reserveringen in meerdere verschillende restaurants op verschillende tijdstippen van de dag inhoudt, kunnen deze reserveringen bijvoorbeeld als afzonderlijke objecten onder `diningReservations` voor één gebeurtenis worden vermeld.

Hieronder vindt u de structuur van elk object dat onder `diningReservations` wordt geleverd.

![&#x200B; diningReservations structuur &#x200B;](../../images/field-groups/dining-reservation/diningReservations.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `ID` | String | Het reserveringsnummer of de identificatiecode. |
| `cancellation` | Geheel | Deze waarde wordt vastgelegd wanneer een reservering is geannuleerd. |
| `confirmationNumber` | String | Het bevestigingsnummer of de identificatiecode van de reservering. |
| `created` | Geheel | Deze waarde wordt vastgelegd wanneer een reservering is gemaakt. |
| `cuisine` | Geheel | Het type restaurantkeuken. |
| `currencyCode` | String | De ISO 4217-valutacode die wordt gebruikt om de aankoop te doen. |
| `deliveryPartners` | String | Leveringspartners beschikbaar in het restaurant. |
| `diningOptions` | String | De levering en het dineren opties beschikbaar bij het restaurant. |
| `groupReservation` | Boolean | Geeft aan of de reservering voor een groep wordt gemaakt. |
| `length` | Geheel | Het totale aantal dagen voor de reservering. |
| `loyaltyID` | String | De id van het loyaliteitsprogramma voor de gast die in het reservaat wordt vermeld. |
| `modification` | Geheel | Deze waarde wordt vastgelegd wanneer een reservering is gewijzigd. |
| `modificationDate` | DateTime | Het tijdstip waarop de reservering voor het laatst is gewijzigd. |
| `numberOfAdults` | Geheel | Het aantal volwassenen dat met het voorbehoud verband houdt. |
| `numberOfChildren` | Geheel | Het aantal kinderen verbonden aan de reserve. |
| `numberOfRooms` | Geheel | Het aantal ruimten dat aan de reservering is gekoppeld. |
| `partySize` | Geheel | Het aantal individuen in de eetpartij. |
| `priceCategory` | String | De prijscategorie voor het gemaakte voorbehoud. |
| `purpose` | String | Het doel van het voorbehoud, meestal zakelijk of persoonlijk. |
| `reservationTime` | DateTime | De tijd waarvoor de diningsreservering wordt geboekt. |
| `restaurantID` | String | Een id voor het restaurant of de eetlocatie. |
| `reservationStatus` | String | De status van het voorbehoud. |
| `specialOccasion` | Boolean | Geeft aan of het voorbehoud voor een bijzondere gelegenheid wordt gemaakt. |
| `status` | Geheel | De status van de diningsreservering. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
