---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schema-ontwerp;veldgroep;field-groep;reservering;vlucht;
title: Veldgroep vluchtreservatieschema
description: Dit document bevat een overzicht van de veldgroep Vluchtreserveringsschema.
exl-id: df4bb525-c2d3-4e1d-921f-903142a570ac
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 2%

---

# [!UICONTROL Flight Reservation] schemaveldgroep

[!UICONTROL Flight Reservation] is een standaardschemagebiedgroep voor [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) gebruikt om informatie over een vluchtreservering vast te leggen.

De veldgroep is een uitbreiding van de [!UICONTROL Reservation Details] veldgroep en bevat dezelfde velden onder één veld van het objecttype, `reservations`. Naast deze generieke velden [!UICONTROL Flight Reservation] omvat ook `flightReservations` array. Deze array met objecten wordt gebruikt om een of meer reserveringen te beschrijven met eigenschappen die uniek zijn voor luchtvervoer.

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
| `flightCheckIn` | Object | Hiermee worden gegevens over de inchecken van de vlucht vastgelegd. Het object bevat de volgende eigenschappen:<ul><li>`arrivalAirportCode`: (String) De luchthavencode van de aankomststad.</li><li>`boardingGroup`: (String) De luchtvaartspecifieke indicator van instaporder.</li><li>`checkInMethod`: (Tekenreeks) De methode die de inchecken heeft gebruikt, zoals de teller, online, kiosk of zelfbediening.</li><li>`checkedBags`: (Geheel getal) Het aantal zakken dat voor de vlucht is gecontroleerd.</li><li>`checkedPassengers`: (Geheel getal) Het aantal passagiers dat voor de vlucht is ingecheckt, indien er meerdere passagiers zijn voor hetzelfde reserveringsnummer.</li><li>`confirmationNumber`: (String) Het bevestigingsnummer of de id van de reservering.</li><li>`departureAirportCode`: (String) De luchthavencode van de vertrekstad.</li><li>`flightNumber`: (String) The flight number for the flight being reserved.</li></ul> |
| `flightStatusSearch` | Object | Leg de details vast die worden teruggestuurd wanneer de status van de vlucht wordt doorzocht. Het object bevat de volgende eigenschappen:<ul><li>`arrivalAirportCode`: (String) De luchthavencode van de aankomststad.</li><li>`boardingGroup`: (String) De luchtvaartspecifieke indicator van instaporder.</li><li>`departureAirportCode`: (String) De luchthavencode van de vertrekstad.</li><li>`departureDate`: (DateTime) De vertrekdatum van de gereserveerde vlucht.</li><li>`flightNumber`: (String) The flight number for the flight being reserved.</li><li>`searchCount`: (Geheel getal) Het aantal keren dat de status van de gereserveerde vlucht is doorzocht.</li></ul> |
| `agentID` | Tekenreeks | De agent of de boekhouder die verantwoordelijk is voor de boeking van de boeking, indien van toepassing. |
| `aircraftID` | Tekenreeks | Een id voor het luchtvaartuig. |
| `aircraftType` | Tekenreeks | Het type luchtvaartuig. |
| `arrivalAirportCode` | Tekenreeks | De luchthavencode van de aankomststad. |
| `arrivalDate` | DateTime | De aankomstdatum van de gereserveerde vlucht. |
| `cancellation` | Geheel | Deze waarde wordt vastgelegd wanneer een reservering is geannuleerd. |
| `confirmationNumber` | Tekenreeks | Het bevestigingsnummer of de identificatiecode van de reservering. |
| `created` | Tekenreeks | Deze waarde wordt vastgelegd wanneer een reservering is gemaakt. |
| `currencyCode` | Tekenreeks | De ISO 4217-valutacode die wordt gebruikt om de aankoop te doen. |
| `departureAirportCode` | Tekenreeks | De luchthavencode van de vertrekstad. |
| `departureDate` | DateTime | De vertrekdatum van de gereserveerde vlucht. |
| `fareClass` | Tekenreeks | De tariefklasse van de vlucht die wordt gereserveerd. |
| `flightNumber` | Tekenreeks | Het vluchtnummer van de gereserveerde vlucht. |
| `length` | Geheel | Het totale aantal dagen voor de reservering. |
| `loyaltyID` | Tekenreeks | De programma-id voor loyaliteit of beloningen voor de in het voorbehoud vermelde passagier. |
| `modification` | Geheel | Deze waarde wordt vastgelegd wanneer een reservering is gewijzigd. |
| `modificationDate` | DateTime | Het tijdstip waarop de reservering voor het laatst is gewijzigd. |
| `numberOfAdults` | Geheel | Het aantal volwassenen dat met het voorbehoud verband houdt. |
| `numberOfChildren` | Geheel | Het aantal kinderen verbonden aan de reserve. |
| `passengerID` | Tekenreeks | Passagiersinformatie in verband met de boeking. |
| `purpose` | Tekenreeks | Het doel van het voorbehoud, meestal zakelijk of persoonlijk. |
| `salesChannel` | Tekenreeks | Het verkoopkanaal van waaruit de boeking is geboekt. |
| `securityScreening` | Tekenreeks | Het type beveiligingsonderzoek waaraan de passagier is onderworpen. |
| `status` | Tekenreeks | De status van de vluchtreservering. |
| `ticketNumber` | Tekenreeks | Het reserveringsnummer of de identificatiecode. |
| `tripType` | Tekenreeks | Hiermee geeft u aan of de boeking betrekking heeft op een eenmalige reis, een retourvlucht of een meervoudige retourvlucht. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.schema.json)
