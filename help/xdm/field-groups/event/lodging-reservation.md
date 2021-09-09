---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schema-ontwerp;veldgroep;veldgroep;reservering;onderbrenging;
title: Veld groep voor reservatieschema indienen
description: Dit document biedt een overzicht van de veldgroep met het schema Opmerking overbrengen.
source-git-commit: d230cfa9e74eb96aa44e8b83ca8f2306db4ba4ec
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 2%

---


# [!UICONTROL Lodging Reservation] schemaveldgroep

[!UICONTROL Lodging Reservation] is een standaardschemagebiedgroep voor de  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) klasse die wordt gebruikt om informatie betreffende een indieningsreserve te vangen.

De veldgroep is een uitbreiding van de [!UICONTROL Reservation Details] gebiedsgroep, en bevat alle zelfde gebieden onder één enkel voorwerp-type gebied, `reservations`. Naast deze generieke velden bevat [!UICONTROL Lodging Reservation] ook `lodgingReservations`-array. Deze array met objecten wordt gebruikt om een of meer reserveringen te beschrijven met eigenschappen die uniek zijn voor het indienen van objecten.

>[!NOTE]
>
>In dit document worden de details van de array `lodgingReservations` besproken. Raadpleeg de [[!UICONTROL Reservation Details]-veldgroepreferentie](./reservation-details.md) voor informatie over de andere velden die worden opgegeven onder het `reservations`-object.

![Boekingsstructuur voor indiening](../../images/field-groups/lodging-reservation/structure.png)

## `lodgingReservations`

`lodgingReservations` is een array met objecten die een lijst met reserveringen bevat. Als een reserveringsgebeurtenis reserveringen bij meerdere verschillende hotels langs de route van een reis inhoudt, kunnen deze reserveringen bijvoorbeeld worden vermeld als afzonderlijke objecten onder `lodgingReservations` voor één gebeurtenis.

Hieronder vindt u de structuur van elk object dat onder `lodgingReservations` wordt geleverd.

![reserve-structuur](../../images/field-groups/lodging-reservation/lodgingReservations.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `averageDailyPrice` | [[!UICONTROL Currency]](../../data-types/currency.md) | De gemiddelde dagprijs van de hotelkamer. |
| `lodgingCheckIn` | Object | Een object dat het indienen van incheckgegevens beschrijft. Bevat de volgende waarden:<ul><li>`digitalKey`: (Geheel getal) Geeft aan wanneer een gast het gebruik van een digitale sleutel selecteert na het inchecken.</li><li>`earlyCheckInRequested`: (Geheel getal) Hiermee geeft u aan wanneer een gast vraagt om eerder in te checken dan de normale incheckuren.</li><li>`lateCheckInRequested`: (Geheel getal) Geeft aan wanneer een gast later dan de normale incheckuren om inchecken vraagt.</li><li>`noRoomCheckIn`: (Geheel getal) Deze waarde wordt vastgelegd wanneer een gast klaar is met inchecken als er op dat moment geen ruimten beschikbaar zijn.</li><li>`oneRoomCheckIn`: (Geheel getal) Deze waarde wordt vastgelegd wanneer een gast klaar is met inchecken wanneer er op dat moment slechts één ruimte beschikbaar is.</li><li>`roomKeys`: (Geheel getal) Het aantal standaard kamersleutels dat bij inchecken wordt aangeboden.</li><li>`userSelectedRoom`: (Boolean) Geeft aan of de gast zijn of haar ruimte heeft geselecteerd bij het inchecken.</li></ul> |
| `rackrate` | [[!UICONTROL Currency]](../../data-types/currency.md) | De kosten voor een reservering op dezelfde dag zonder voorafgaande boekingen. |
| `ID` | Tekenreeks | Het reserveringsnummer of de identificatiecode. |
| `agentID` | Tekenreeks | De agent-id die is gekoppeld aan de hotelboeking. |
| `basePrice` | Tekenreeks | De basisprijs voordat eventuele kortingen worden toegevoegd. |
| `bookingID` | Tekenreeks | De boekings-id die is gekoppeld aan de hotelboeking. |
| `cancellation` | Geheel | Deze waarde wordt vastgelegd wanneer een reservering is geannuleerd. |
| `checkInDate` | DateTime | De incheckdatum voor de reservering van de ruimte. |
| `checkOutDate` | DateTime | De uitcheckdatum voor de reservering van de ruimte. |
| `confirmationNumber` | Tekenreeks | Het bevestigingsnummer of de identificatiecode van de reservering. |
| `couponCode` | Tekenreeks | Een couponcode die is gekoppeld aan de hotelboeking. |
| `created` | Geheel | Deze waarde wordt vastgelegd wanneer een reservering is gemaakt. |
| `currencyCode` | Tekenreeks | De ISO 4217-valutacode die wordt gebruikt om de aankoop te doen. |
| `discountPercent` | Dubbel | Het disconteringspercentage dat aan de boeking is gekoppeld. |
| `freeCancelation` | Boolean | Geeft aan of de ruimte een gratis annuleringsbeleid heeft. |
| `guestID` | Tekenreeks | De gast-id die is gekoppeld aan de hotelboeking. |
| `length` | Geheel | Het totale aantal dagen voor de reservering. |
| `loyaltyID` | Tekenreeks | De id van het loyaliteitsprogramma voor de gast die in het reservaat wordt vermeld. |
| `modification` | Geheel | Deze waarde wordt vastgelegd wanneer een reservering is gewijzigd. |
| `modificationDate` | DateTime | Het tijdstip waarop de reservering voor het laatst is gewijzigd. |
| `numberOfAdults` | Geheel | Het aantal volwassenen dat met het voorbehoud verband houdt. |
| `numberOfChildren` | Geheel | Het aantal kinderen verbonden aan de reserve. |
| `numberOfRooms` | Geheel | Het aantal ruimten dat aan de reservering is gekoppeld. |
| `propertyID` | Tekenreeks | Een identificator van het hotel of het toevluchtsoord voor de boeking. |
| `propertyName` | Tekenreeks | De naam van het hotel of het toevluchtsoord voor de boeking. |
| `purpose` | Tekenreeks | Het doel van het voorbehoud, meestal zakelijk of persoonlijk. |
| `ratePlan` | Tekenreeks | De tariefovereenkomst waarop de kamer werd verkocht. |
| `refundable` | Boolean | Geeft aan of de ruimte kan worden terugbetaald. |
| `reservationStatus` | Tekenreeks | De status van het voorbehoud. |
| `roomAccessibilityType` | Tekenreeks | Het toegankelijkheidstype van de ruimte, zoals mobiliteit, gehoor of andere. |
| `roomCapacity` | Geheel | Het aantal mensen in de hotelkamer. |
| `roomType` | Tekenreeks | Het type ruimte dat wordt gereserveerd. |
| `smoking` | Boolean | Geeft aan of de ruimte roken toestaat. |
| `tripType` | Tekenreeks | Hiermee geeft u aan of de boeking betrekking heeft op een eenmalige reis, een retourvlucht of een meervoudige retourvlucht. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json)
