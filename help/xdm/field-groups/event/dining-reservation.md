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

[!UICONTROL Dining Reservation] is een standaardschemagebiedgroep voor [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) gebruikt om informatie over een diningsreservering vast te leggen.

De veldgroep is een uitbreiding van de [!UICONTROL Reservation Details] veldgroep en bevat dezelfde velden onder één veld van het objecttype, `reservations`. Naast deze generieke velden, [!UICONTROL Dining Reservation] omvat ook `diningReservations` array. Deze array met objecten wordt gebruikt om een of meer reserveringen met restaurantspecifieke eigenschappen te beschrijven.

>[!NOTE]
>
>In dit document worden de details van het `diningReservations` array. Voor informatie over de andere velden die in het kader van de `reservations` object, raadpleeg de [[!UICONTROL Reservation Details] veldgroepverwijzing](./reservation-details.md).

![Boekingsstructuur voor mijnbouw](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` is een array met objecten die een lijst met diningsreserveringen vertegenwoordigt. Als bij een reserveringsgebeurtenis reserveringen worden gemaakt in meerdere verschillende restaurants op verschillende tijdstippen van de dag, kunnen deze reserveringen bijvoorbeeld als afzonderlijke objecten worden vermeld onder `diningReservations` voor één gebeurtenis.

De structuur van elk object dat wordt geleverd onder `diningReservations` wordt hieronder gegeven.

![diningReservations-structuur](../../images/field-groups/dining-reservation/diningReservations.png)

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

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
