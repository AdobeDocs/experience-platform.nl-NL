---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schema-ontwerp;veldgroep;veldgroep;reservering;reserveringsgegevens;
title: Reserveringsdetails schema veldgroep
description: Meer informatie over de veldgroep Reserveringsdetails.
exl-id: 06f9ee37-9879-4db2-af68-9336366f7521
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# [!UICONTROL Reservation Details] schemaveldgroep

[!UICONTROL Reservation Details] is een standaardgroep van het schemagebied voor de [[!DNL XDM ExperienceEvent]  klasse ](../../classes/experienceevent.md) wordt gebruikt om informatie betreffende een reserve, met inbegrip van lengte, wijziging, terugvorderbare status, en aantal ruimten te vangen die.

De veldgroep bevat één objecttype veld, `reservations` . De eigenschappen in dit object worden hieronder uitgelegd.

![ structuur van de Details van de Voorbehoud ](../../images/field-groups/reservation-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `nonRefundableAmount` | [ Valuta ](../../data-types/currency.md) | Het bedrag van de reserveringsprijs dat als niet-terugvorderbaar is gemarkeerd. |
| `transaction` | [ Transactie ](../../data-types/transaction.md) | Beschrijft de valutatransactie voor de reservering. |
| `id` | String | Een unieke id voor de reservering. |
| `cancellation` | Geheel | Deze waarde wordt vastgelegd wanneer een reservering is geannuleerd. |
| `confirmationNumber` | String | Het bevestigingsnummer of de identificatiecode van de boeking. |
| `created` | Geheel | Deze waarde wordt vastgelegd wanneer de reservering is gemaakt. |
| `currencyCode` | String | De ISO 4217-valutacode die wordt gebruikt om de aankoop te doen. |
| `endDate` | DateTime | De einddatum voor de reservering, de geretourneerde datum of de uitcheckdatum. |
| `length` | Geheel | Het totale aantal dagen voor de reservering. |
| `modification` | Geheel | Deze waarde wordt vastgelegd wanneer een reservering is gewijzigd. |
| `modificationDate` | DateTime | Het tijdstip waarop de reservering voor het laatst is gewijzigd. |
| `numberOfAdults` | Geheel | Het aantal volwassenen dat met het voorbehoud verband houdt. |
| `numberOfChildren` | Geheel | Het aantal kinderen verbonden aan de reserve. |
| `purpose` | String | Het doel van het voorbehoud, meestal zakelijk of persoonlijk. |
| `startDate` | DateTime | De beginophaaldatum, de uitgaande datum of de incheckdatum voor de reservering. |
| `triptype` | String | Hiermee geeft u aan of de boeking betrekking heeft op een eenmalige reis, een retourvlucht of een meervoudige retourvlucht. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.schema.json)

## Industriespecifieke reserveringsgroepen

Er zijn verscheidene andere standaardgebiedsgroepen die het [!UICONTROL Reservation Details] schema voor industrie-specifieke gebruiksgevallen uitbreiden. Raadpleeg de volgende documentatie voor meer informatie:

* [[!UICONTROL Dining Reservation]](./dining-reservation.md)
* [[!UICONTROL Flight Reservation]](./flight-reservation.md)
* [[!UICONTROL Lodging Reservation]](./lodging-reservation.md)
