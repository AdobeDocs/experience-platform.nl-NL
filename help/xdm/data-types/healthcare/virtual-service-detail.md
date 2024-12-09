---
title: Gegevenstype van virtuele servicedetails
description: Leer over het Virtuele Model van de Gegevens van de Ervaring van de Dienst van het Detail (XDM) gegevenstype.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# [!UICONTROL Virtual Service Detail] gegevenstype

[!UICONTROL Virtual Service Detail] is een standaard gegevenstype van het Model van de Gegevens van de Ervaring (XDM) dat de details van het virtuele de dienstcontact beschrijft. Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![ Virtuele het gegevenstype van de Dienst van het Detail structuur ](../../images/data-types/healthcare/virtual-service-detail.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Address Contact Point] | `addressContactPoint` | [[!UICONTROL Contact Point]](../healthcare/contact-point.md) | De details van een technologie gemedieerd contactpunt zoals een telefoon, fax, of e-mail. |
| [!UICONTROL Address Extended Contact Detail] | `addressExtendedContactDetail` | [[!UICONTROL Extended Contact Detail]](../healthcare/extended-contact-detail.md) | Uitgebreide contactgegevens. |
| [!UICONTROL Channel Type] | `channelType` | [[!UICONTROL Coding]](../healthcare/coding.md) | Het type virtuele service waarmee verbinding moet worden gemaakt, zoals Teams, Zoom of WhatsApp. |
| [!UICONTROL Additional Info] | `additionalInfo` | Array van tekenreeksen | Het adres om alternatieve verbindingsdetails te zien, die als URI wordt vertegenwoordigd. |
| [!UICONTROL Address String] | `addressString` | String | Het adres dat moet worden gebruikt om met de virtuele dienst te verbinden. |
| [!UICONTROL Address Url] | `addressUrl` | String | De URL die moet worden gebruikt om verbinding te maken met de virtuele service, weergegeven als een URI. |
| [!UICONTROL Max Participants] | `maxParticipants` | Geheel | Het maximumaantal deelnemers dat wordt ondersteund, met een minimumwaarde van `0`. |
| [!UICONTROL Session Key] | `sessionKey` | String | De sessiesleutel die door de virtuele service wordt vereist. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.schema.json)
