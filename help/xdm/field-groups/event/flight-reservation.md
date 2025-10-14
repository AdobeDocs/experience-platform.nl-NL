---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schema-ontwerp;veldgroep;field-groep;reservering;vlucht;
title: Veldgroep vluchtreservatieschema
description: Meer informatie over de veldgroep Vluchtreserveringsschema.
exl-id: df4bb525-c2d3-4e1d-921f-903142a570ac
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# [!UICONTROL Flight Reservation] schemaveldgroep

[!UICONTROL Flight Reservation] is een standaardgroep van het schemagebied voor de [[!DNL XDM ExperienceEvent]  klasse &#x200B;](../../classes/experienceevent.md) wordt gebruikt om informatie betreffende een vluchtreserve te vangen die.

De veldgroep is een extensie van de veldgroep [!UICONTROL Reservation Details] en bevat dezelfde velden onder één objecttype, `reservations` . Naast deze algemene velden bevat [!UICONTROL Flight Reservation] ook `flightReservations` array. Deze array met objecten wordt gebruikt om een of meer reserveringen te beschrijven met eigenschappen die uniek zijn voor luchtvervoer.

>[!NOTE]
>
>In dit document worden de details van de array `flightReservations` besproken. Voor informatie over de andere gebieden die onder het `reservations` voorwerp worden verstrekt, gelieve te verwijzen naar [[!UICONTROL Reservation Details] de verwijzing van de gebiedsgroep &#x200B;](./reservation-details.md).

![&#x200B; structuur van de Reservering van de Vlucht &#x200B;](../../images/field-groups/flight-reservation/structure.png)

## `flightReservations`

`flightReservations` is een array met objecten die een lijst met vliegreserveringen vertegenwoordigt. Als een reserveringsgebeurtenis reserveringen voor meerdere aansluitende vluchten op een reis bevat, kunnen deze reserveringen bijvoorbeeld worden vermeld als afzonderlijke objecten onder `flightReservations` voor één gebeurtenis.

Hieronder vindt u de structuur van elk object dat onder `flightReservations` wordt geleverd.

![&#x200B; flightReservations structuur &#x200B;](../../images/field-groups/flight-reservation/flightReservations.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `flightCheckIn` | Object | Hiermee worden gegevens over de vluchtcontrole vastgelegd. Het object bevat de volgende eigenschappen:<ul><li>`arrivalAirportCode`: (String) De luchthavencode van de aankomststad.</li><li>`boardingGroup`: (Tekenreeks) De luchtvaartspecifieke indicator van instaporder.</li><li>`checkInMethod`: (Tekenreeks) De methode die de inchecking heeft gebruikt, zoals de teller, online, kiosk of zelfbediening.</li><li>`checkedBags`: (Geheel getal) Het aantal zakken dat op de vlucht is gecontroleerd.</li><li>`checkedPassengers`: (Geheel getal) Het aantal passagiers dat voor de vlucht is ingecheckt, indien er meerdere passagiers zijn voor hetzelfde reserveringsnummer.</li><li>`confirmationNumber`: (String) Het bevestigingsnummer of de id van de reservering.</li><li>`departureAirportCode`: (String) De luchthavencode van de vertrekstad.</li><li>`flightNumber`: (String) Het vluchtnummer voor de vlucht die wordt gereserveerd.</li></ul> |
| `flightStatusSearch` | Object | Hiermee worden de gegevens vastgelegd die worden teruggestuurd wanneer de status van de vlucht wordt doorzocht. Het object bevat de volgende eigenschappen:<ul><li>`arrivalAirportCode`: (String) De luchthavencode van de aankomststad.</li><li>`boardingGroup`: (Tekenreeks) De luchtvaartspecifieke indicator van instaporder.</li><li>`departureAirportCode`: (String) De luchthavencode van de vertrekstad.</li><li>`departureDate`: (DateTime) De vertrekdatum van de vlucht die wordt gereserveerd.</li><li>`flightNumber`: (String) Het vluchtnummer voor de vlucht die wordt gereserveerd.</li><li>`searchCount`: (Geheel getal) Het aantal keren dat de status van de gereserveerde vlucht is doorzocht.</li></ul> |
| `agentID` | String | De agent of de boekhouder die verantwoordelijk is voor de boeking van de boeking, indien van toepassing. |
| `aircraftID` | String | Een id voor het luchtvaartuig. |
| `aircraftType` | String | Het type luchtvaartuig. |
| `arrivalAirportCode` | String | De luchthavencode van de aankomststad. |
| `arrivalDate` | DateTime | De aankomstdatum van de gereserveerde vlucht. |
| `cancellation` | Geheel | Deze waarde wordt vastgelegd wanneer een reservering is geannuleerd. |
| `confirmationNumber` | String | Het bevestigingsnummer of de identificatiecode van de reservering. |
| `created` | String | Deze waarde wordt vastgelegd wanneer een reservering is gemaakt. |
| `currencyCode` | String | De ISO 4217-valutacode die wordt gebruikt om de aankoop te doen. |
| `departureAirportCode` | String | De luchthavencode van de vertrekstad. |
| `departureDate` | DateTime | De vertrekdatum van de gereserveerde vlucht. |
| `fareClass` | String | De tariefklasse van de vlucht die wordt gereserveerd. |
| `flightNumber` | String | Het vluchtnummer van de gereserveerde vlucht. |
| `length` | Geheel | Het totale aantal dagen voor de reservering. |
| `loyaltyID` | String | De programma-id voor loyaliteit of beloningen voor de in het voorbehoud vermelde passagier. |
| `modification` | Geheel | Deze waarde wordt vastgelegd wanneer een reservering is gewijzigd. |
| `modificationDate` | DateTime | Het tijdstip waarop de reservering voor het laatst is gewijzigd. |
| `numberOfAdults` | Geheel | Het aantal volwassenen dat met het voorbehoud verband houdt. |
| `numberOfChildren` | Geheel | Het aantal kinderen verbonden aan de reserve. |
| `passengerID` | String | Passagiersinformatie in verband met de boeking. |
| `purpose` | String | Het doel van het voorbehoud, meestal zakelijk of persoonlijk. |
| `salesChannel` | String | Het verkoopkanaal van waaruit de boeking is geboekt. |
| `securityScreening` | String | Het type beveiligingsonderzoek waaraan de passagier is onderworpen. |
| `status` | String | De status van de vluchtreservering. |
| `ticketNumber` | String | Het reserveringsnummer of de identificatiecode. |
| `tripType` | String | Hiermee geeft u aan of de boeking betrekking heeft op een eenmalige reis, een retourvlucht of een meervoudige retourvlucht. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.schema.json)
