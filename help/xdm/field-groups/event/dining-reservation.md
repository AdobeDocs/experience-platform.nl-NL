---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schema-ontwerp;veldgroep;field-groep;reservering;dining;
title: Veldengroep voor denningsreservatieschema
description: Dit document biedt een overzicht van de veldgroep met het indelingsschema voor reservaten.
source-git-commit: d230cfa9e74eb96aa44e8b83ca8f2306db4ba4ec
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 2%

---


# [!UICONTROL Dining Reservation] schemaveldgroep

[!UICONTROL Dining Reservation] is een standaardschemagebiedgroep voor de  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) klasse die wordt gebruikt om informatie betreffende een het dineren reserve te vangen.

De veldgroep is een uitbreiding van de [!UICONTROL Reservation Details] gebiedsgroep, en bevat alle zelfde gebieden onder één enkel voorwerp-type gebied, `reservations`. Naast deze generieke velden bevat [!UICONTROL Dining Reservation] ook `diningReservations`-array. Deze array met objecten wordt gebruikt om een of meer reserveringen met restaurantspecifieke eigenschappen te beschrijven.

>[!NOTE]
>
>In dit document worden de details van de array `diningReservations` besproken. Raadpleeg de [[!UICONTROL Reservation Details]-veldgroepreferentie](./reservation-details.md) voor informatie over de andere velden die worden opgegeven onder het `reservations`-object.

![Boekingsstructuur](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` is een array met objecten die een lijst met diningsreserveringen vertegenwoordigt. Als een reserveringsgebeurtenis reserveringen in meerdere verschillende restaurants op verschillende tijdstippen van de dag inhoudt, kunnen deze reserveringen bijvoorbeeld als afzonderlijke objecten onder `diningReservations` voor één gebeurtenis worden vermeld.

Hieronder vindt u de structuur van elk object dat onder `diningReservations` wordt geleverd.

![diningReservations-structuur](../../images/field-groups/dining-reservation/diningReservations.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `ID` | Tekenreeks | Het reserveringsnummer of de identificatiecode. |
| `cancellation` | Geheel | Deze waarde wordt vastgelegd wanneer een reservering is geannuleerd. |
| `confirmationNumber` | Tekenreeks | Het bevestigingsnummer of de identificatiecode van de reservering. |
| `created` | Geheel | Deze waarde wordt vastgelegd wanneer een reservering is gemaakt. |
| `cuisine` | Geheel | Het type restaurantkeuken. |
| `currencyCode` | Tekenreeks | De ISO 4217-valutacode die wordt gebruikt om de aankoop te doen. |
| `deliveryPartners` | Tekenreeks | Leveringspartners beschikbaar in het restaurant. |
| `diningOptions` | Tekenreeks | De levering en het dineren opties beschikbaar bij het restaurant. |
| `groupReservation` | Boolean | Geeft aan of de reservering voor een groep wordt gemaakt. |
| `length` | Geheel | Het totale aantal dagen voor de reservering. |
| `loyaltyID` | Tekenreeks | De id van het loyaliteitsprogramma voor de gast die in het reservaat wordt vermeld. |
| `modification` | Geheel | Deze waarde wordt vastgelegd wanneer een reservering is gewijzigd. |
| `modificationDate` | DateTime | Het tijdstip waarop de reservering voor het laatst is gewijzigd. |
| `numberOfAdults` | Geheel | Het aantal volwassenen dat met het voorbehoud verband houdt. |
| `numberOfChildren` | Geheel | Het aantal kinderen verbonden aan de reserve. |
| `numberOfRooms` | Geheel | Het aantal ruimten dat aan de reservering is gekoppeld. |
| `partySize` | Geheel | Het aantal individuen in de eetpartij. |
| `priceCategory` | Tekenreeks | De prijscategorie voor het voorbehoud dat wordt gemaakt. |
| `purpose` | Tekenreeks | Het doel van het voorbehoud, meestal zakelijk of persoonlijk. |
| `reservationTime` | DateTime | De tijd waarvoor de diningsreservering wordt geboekt. |
| `restaurantID` | Tekenreeks | Een id voor het restaurant of de eetlocatie. |
| `reservationStatus` | Tekenreeks | De status van het voorbehoud. |
| `specialOccasion` | Boolean | Geeft aan of het voorbehoud voor een bijzondere gelegenheid wordt gemaakt. |
| `status` | Geheel | De status van de diningsreservering. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
