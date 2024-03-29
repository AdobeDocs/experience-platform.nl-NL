---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schema-ontwerp;veldgroep;veldgroep;reservering;onderbrenging;
title: Veld groep voor reservatieschema indienen
description: Leer over de het gebiedsgroep van het Reserveringsschema van de Lodging.
exl-id: f0eafc83-21f1-483d-9397-1133e3777699
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 0%

---

# [!UICONTROL Lodging Reservation] schemaveldgroep

[!UICONTROL Lodging Reservation] is een standaardschemagebiedgroep voor [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) gebruikt om informatie over een boeking te verzamelen.

De veldgroep is een uitbreiding van de [!UICONTROL Reservation Details] veldgroep en bevat dezelfde velden onder één veld van het objecttype, `reservations`. Naast deze generieke velden, [!UICONTROL Lodging Reservation] omvat ook `lodgingReservations` array. Deze array met objecten wordt gebruikt om een of meer reserveringen te beschrijven met eigenschappen die uniek zijn voor het indienen van objecten.

>[!NOTE]
>
>In dit document worden de details van het `lodgingReservations` array. Voor informatie over de andere velden die in het kader van de `reservations` object, raadpleeg de [[!UICONTROL Reservation Details] veldgroepverwijzing](./reservation-details.md).

![Boekingsstructuur voor indiening](../../images/field-groups/lodging-reservation/structure.png)

## `lodgingReservations`

`lodgingReservations` is een array met objecten die een lijst met reserveringen bevat. Indien bij een reserveringsgebeurtenis reserveringen worden gemaakt bij meerdere verschillende hotels langs de route van een reis, kunnen deze reserveringen bijvoorbeeld worden vermeld als afzonderlijke objecten onder `lodgingReservations` voor één gebeurtenis.

De structuur van elk object dat wordt geleverd onder `lodgingReservations` wordt hieronder gegeven.

![reserve-structuur](../../images/field-groups/lodging-reservation/lodgingReservations.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `averageDailyPrice` | [[!UICONTROL Currency]](../../data-types/currency.md) | De gemiddelde dagprijs van de hotelkamer. |
| `lodgingCheckIn` | Object | Een object dat het indienen van incheckgegevens beschrijft. Bevat de volgende waarden:<ul><li>`digitalKey`: (Geheel getal) Geeft aan wanneer een gast het gebruik van een digitale sleutel selecteert na het inchecken.</li><li>`earlyCheckInRequested`: (Geheel getal) Geeft aan wanneer een gast vraagt om eerder in te checken dan de normale incheckuren.</li><li>`lateCheckInRequested`: (Geheel getal) Geeft aan wanneer een gast later dan de normale incheckuren om inchecken vraagt.</li><li>`noRoomCheckIn`: (Geheel getal) Deze waarde wordt vastgelegd wanneer een gast incheckt wanneer er op dat moment geen ruimten beschikbaar zijn.</li><li>`oneRoomCheckIn`: (Geheel getal) Deze waarde wordt vastgelegd wanneer een gast klaar is met inchecken wanneer er op dat moment slechts één ruimte beschikbaar is.</li><li>`roomKeys`: (Geheel getal) Het aantal standaard kamertoetsen dat bij het inchecken wordt aangeboden.</li><li>`userSelectedRoom`: (Boolean) Geeft aan of de gast zijn of haar ruimte heeft geselecteerd tijdens het inchecken.</li></ul> |
| `rackrate` | [[!UICONTROL Currency]](../../data-types/currency.md) | De kosten voor een reservering op dezelfde dag zonder voorafgaande boekingsregelingen. |
| `ID` | String | Het reserveringsnummer of de identificatiecode. |
| `agentID` | String | De agent-id die is gekoppeld aan de hotelboeking. |
| `basePrice` | String | De basisprijs voordat eventuele kortingen worden toegevoegd. |
| `bookingID` | String | De boekings-id die is gekoppeld aan de hotelboeking. |
| `cancellation` | Geheel | Deze waarde wordt vastgelegd wanneer een reservering is geannuleerd. |
| `checkInDate` | DateTime | De incheckdatum voor de reservering van de ruimte. |
| `checkOutDate` | DateTime | De uitcheckdatum voor de reservering van de ruimte. |
| `confirmationNumber` | String | Het bevestigingsnummer of de identificatiecode van de reservering. |
| `couponCode` | String | Een couponcode die is gekoppeld aan de hotelboeking. |
| `created` | Geheel | Deze waarde wordt vastgelegd wanneer een reservering is gemaakt. |
| `currencyCode` | String | De ISO 4217-valutacode die wordt gebruikt om de aankoop te doen. |
| `discountPercent` | Dubbel | Het disconteringspercentage dat aan de boeking is gekoppeld. |
| `freeCancelation` | Boolean | Geeft aan of de ruimte een beleid voor gratis annulering heeft. |
| `guestID` | String | De gast-id die is gekoppeld aan de hotelboeking. |
| `length` | Geheel | Het totale aantal dagen voor de reservering. |
| `loyaltyID` | String | De id van het loyaliteitsprogramma voor de gast die in het reservaat wordt vermeld. |
| `modification` | Geheel | Deze waarde wordt vastgelegd wanneer een reservering is gewijzigd. |
| `modificationDate` | DateTime | Het tijdstip waarop de reservering voor het laatst is gewijzigd. |
| `numberOfAdults` | Geheel | Het aantal volwassenen dat met het voorbehoud verband houdt. |
| `numberOfChildren` | Geheel | Het aantal kinderen verbonden aan de reserve. |
| `numberOfRooms` | Geheel | Het aantal ruimten dat aan de reservering is gekoppeld. |
| `propertyID` | String | Een identificator van het hotel of het toevluchtsoord voor de boeking. |
| `propertyName` | String | De naam van het hotel of het toevluchtsoord voor de boeking. |
| `purpose` | String | Het doel van het voorbehoud, meestal zakelijk of persoonlijk. |
| `ratePlan` | String | De tariefovereenkomst waarop de kamer werd verkocht. |
| `refundable` | Boolean | Geeft aan of de ruimte kan worden terugbetaald. |
| `reservationStatus` | String | De status van het voorbehoud. |
| `roomAccessibilityType` | String | Het toegankelijkheidstype van de ruimte, zoals mobiliteit, gehoor of andere. |
| `roomCapacity` | Geheel | Het aantal mensen in de hotelkamer. |
| `roomType` | String | Het type ruimte dat wordt gereserveerd. |
| `smoking` | Boolean | Geeft aan of de ruimte roken toestaat. |
| `tripType` | String | Hiermee geeft u aan of de boeking betrekking heeft op een eenmalige reis, een retourvlucht of een meervoudige retourvlucht. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json)
