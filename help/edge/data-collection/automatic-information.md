---
title: Automatisch verzamelde gegevens
description: Een overzicht van de gegevens die SDK van het Web van Adobe Experience Platform automatisch verzamelt.
exl-id: 901df786-df36-4986-9c74-a32d29c11b71
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 1%

---

# Automatisch verzamelde gegevens

Adobe Experience Platform Web SDK verzamelt automatisch bepaalde gegevens uit het vak. Als uw organisatie deze gegevens niet automatisch wil verzamelen, kunt u de opdracht `context` in de [`configure` command](../fundamentals/configuring-the-sdk.md).

Trefwoorden die zijn uitgesloten van het dialoogvenster `context` array worden niet opgenomen in gegevensverzameling. Als de `context` array bestaat niet in de `configure` alle gegevens in de onderstaande tabel automatisch worden verzameld.

| Naam | Beschrijving | `context` arraytrefwoord | XDM-pad | Voorbeeldwaarde |
| --- | --- | --- | --- | --- |
| Schermhoogte | De hoogte van het scherm in pixels. | `device` | `events[].xdm.device.screenHeight` | `900` |
| Schermbreedte | De breedte van het scherm in pixels. | `device` | `events[].xdm.device.screenWidth` | `1440` |
| Schermoriëntatie | De oriëntatie van het scherm. | `device` | `events[].xdm.device.screenOrientation` | `landscape` of `portrait` |
| Type omgeving | Het type omgeving waardoor de ervaring optrad. Adobe Experience Platform Web SDK stelt dit veld altijd in op `browser`. | `environment` | `events[].xdm.environment.type` | `browser` |
| Viewporthoogte | De hoogte van het inhoudsgebied van de browser in pixels. | `environment` | `events[].xdm.environment.browserDetails.viewportHeight` | `679` |
| Viewportbreedte | De breedte van het inhoudsgebied van de browser in pixels. | `environment` | `events[].xdm.environment.browserDetails.viewportWidth` | `642` |
| SDK-naam | De SDK-id. In dit veld wordt een URI gebruikt om de unieke id&#39;s van verschillende softwarebibliotheken te verbeteren. Wanneer de zelfstandige bibliotheek wordt gebruikt, is de waarde `https://ns.adobe.com/experience/alloy`. Wanneer de bibliotheek wordt gebruikt als onderdeel van de tagextensie, is de waarde `https://ns.adobe.com/experience/alloy+reactor`. | | `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |
| SDK-versie | Wanneer de zelfstandige bibliotheek wordt gebruikt, is de waarde de bibliotheekversie. Wanneer de bibliotheek wordt gebruikt als onderdeel van de tagextensie, bestaat de waarde uit een samenvoeging van de versie van de bibliotheek en de versie van de tagextensie. | | `events[].xdm.implementationDetails.version` | `2.1.0+2.1.3` |
| Omgeving | De omgeving waarin de gegevens zijn verzameld. Adobe Experience Platform Web SDK stelt dit veld altijd in op `browser`. | | `events[].xdm.implementationDetails.environment` | `browser` |
| Lokale tijd | Lokale tijdstempel voor de eindgebruiker in de vereenvoudigde uitgebreide ISO-indeling [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | `placeContext` | `events[].xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Verschuiving lokale tijdzone | Aantal minuten dat de gebruiker wordt verschoven ten opzichte van GMT. | `placeContext` | `events[].xdm.placeContext.localTimezoneOffset` | `360` |
| Tijdstempel | De UTC-tijdstempel voor de eindgebruiker in de vereenvoudigde uitgebreide ISO-indeling [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | Altijd inbegrepen | `events[].xdm.timestamp` | `YYYY-08-07T22:47:17.129Z` |
| Huidige pagina-URL | De URL van de huidige pagina. | `web` | `events[].xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| Referrer-URL | De URL van de vorige bezochte pagina. | `web` | `events[].xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}
