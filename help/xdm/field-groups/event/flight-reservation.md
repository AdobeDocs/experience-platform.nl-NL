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

[!UICONTROL Flight Reservation] is een standaardschemagebiedgroep voor [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) gebruikt om informatie over een vluchtreservering vast te leggen.

De veldgroep is een uitbreiding van de [!UICONTROL Reservation Details] veldgroep en bevat dezelfde velden onder één veld van het objecttype, `reservations`. Naast deze generieke velden, [!UICONTROL Flight Reservation] omvat ook `flightReservations` array. Deze array met objecten wordt gebruikt om een of meer reserveringen te beschrijven met eigenschappen die uniek zijn voor luchtvervoer.

>[!NOTE]
>
>In dit document worden de details van het `flightReservations` array. Voor informatie over de andere velden die in het kader van de `reservations` object, raadpleeg de [[!UICONTROL Reservation Details] veldgroepverwijzing](./reservation-details.md).

![Vluchtreserveringsstructuur](../../images/field-groups/flight-reservation/structure.png)

## `flightReservations`

`flightReservations` is een array met objecten die een lijst met vluchtreserveringen vertegenwoordigt. Als een reserveringsgebeurtenis reserveringen voor meerdere aansluitende vluchten op een reis inhoudt, kunnen deze reserveringen bijvoorbeeld als afzonderlijke objecten worden vermeld onder `flightReservations` voor één gebeurtenis.

De structuur van elk object dat wordt geleverd onder `flightReservations` wordt hieronder gegeven.

![flightReservations-structuur](../../images/field-groups/flight-reservation/flightReservations.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `flightCheckIn` | Object | Hiermee worden gegevens over de vluchtcontrole vastgelegd. Het object bevat de volgende eigenschappen:<ul><li>`arrivalAirportCode`: (String) De luchthavencode van de aankomststad.</li><li>`boardingGroup`: (String) De luchtvaartspecifieke indicator van instaporder.</li><li>`checkInMethod`: (String) De methode die de inchecken heeft gebruikt, zoals de teller, online, kiosk of zelfbediening.</li><li>`checkedBags`: (Geheel getal) Het aantal zakken dat voor de vlucht is gecontroleerd.</li><li>`checkedPassengers`: (Geheel getal) Het aantal passagiers dat voor de vlucht is ingecheckt, indien er meerdere passagiers zijn voor hetzelfde reserveringsnummer.</li><li>`confirmationNumber`: (String) Het bevestigingsnummer of de id van de reservering.</li><li>`departureAirportCode`: (String) De luchthavencode van de vertrekstad.</li><li>`flightNumber`: (String) The flight number for the flight being reserved.</li></ul> |
| `flightStatusSearch` | Object | Hiermee worden de gegevens vastgelegd die worden teruggestuurd wanneer de status van de vlucht wordt doorzocht. Het object bevat de volgende eigenschappen:<ul><li>`arrivalAirportCode`: (String) De luchthavencode van de aankomststad.</li><li>`boardingGroup`: (String) De luchtvaartspecifieke indicator van instaporder.</li><li>`departureAirportCode`: (String) De luchthavencode van de vertrekstad.</li><li>`departureDate`: (DateTime) De vertrekdatum van de gereserveerde vlucht.</li><li>`flightNumber`: (String) The flight number for the flight being reserved.</li><li>`searchCount`: (Geheel getal) Het aantal keren dat de status van de gereserveerde vlucht is doorzocht.</li></ul> |
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

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.schema.json)
