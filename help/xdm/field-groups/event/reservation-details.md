---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schema-ontwerp;veldgroep;veldgroep;reservering;reserveringsgegevens;
title: Reserveringsdetails schema veldgroep
description: Dit document biedt een overzicht van de veldgroep Reserveringsdetails.
source-git-commit: 295dc040f3af7342226e3d78d0ae21e73db58d57
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 1%

---


# [!UICONTROL Reservation Details] schemaveldgroep

[!UICONTROL Reservation Details] is een standaardschemaveldgroep voor de  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) klasse die wordt gebruikt om informatie over een reserve, met inbegrip van lengte, wijziging, terugvorderbare status, en aantal ruimten te vangen.

De veldgroep bevat één objecttype veld, `reservations`. De eigenschappen in dit object worden hieronder uitgelegd.

![Structuur reserveringsdetails](../../images/field-groups/reservation-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `nonRefundableAmount` | [Valuta](../../data-types/currency.md) | Het bedrag van de reserveringsprijs dat als niet-terugvorderbaar is gemarkeerd. |
| `transaction` | [Transactie](../../data-types/transaction.md) | Beschrijft de valutatransactie voor de reservering. |
| `id` | Tekenreeks | Een unieke id voor de reservering. |
| `cancellation` | Geheel | Deze waarde wordt vastgelegd wanneer een reservering is geannuleerd. |
| `confirmationNumber` | Tekenreeks | Het bevestigingsnummer of de identificatiecode van de boeking. |
| `created` | Geheel | Deze waarde wordt vastgelegd wanneer de reservering is gemaakt. |
| `currencyCode` | Tekenreeks | De ISO 4217-valutacode die wordt gebruikt om de aankoop te doen. |
| `endDate` | DateTime | De einddatum voor de reservering, de geretourneerde datum of de uitcheckdatum. |
| `length` | Geheel | Het totale aantal dagen voor de reservering. |
| `modification` | Geheel | Deze waarde wordt vastgelegd wanneer een reservering is gewijzigd. |
| `modificationDate` | DateTime | Het tijdstip waarop de reservering voor het laatst is gewijzigd. |
| `numberOfAdults` | Geheel | Het aantal volwassenen dat met het voorbehoud verband houdt. |
| `numberOfChildren` | Geheel | Het aantal kinderen verbonden aan de reserve. |
| `purpose` | Tekenreeks | Het doel van het voorbehoud, meestal zakelijk of persoonlijk. |
| `startDate` | DateTime | De begindatum voor de reservatie, de uitgaande of incheckdatum. |
| `triptype` | Tekenreeks | Hiermee geeft u aan of de boeking betrekking heeft op een eenmalige reis, een retourvlucht of een meervoudige retourvlucht. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.schema.json)

## Industriespecifieke reserveringsgroepen

Er zijn verscheidene andere standaardgebiedsgroepen die het [!UICONTROL Reservation Details] schema voor industrie-specifieke gebruiksgevallen uitbreiden. Raadpleeg de volgende documentatie voor meer informatie:

* [[!UICONTROL Dining Reservation]](./dining-reservation.md)
* [[!UICONTROL Flight Reservation]](./flight-reservation.md)
* [[!UICONTROL Lodging Reservation]](./lodging-reservation.md)