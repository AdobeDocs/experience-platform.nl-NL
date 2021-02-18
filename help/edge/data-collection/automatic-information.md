---
title: Automatisch verzamelde informatie in de Adobe Experience Platform Web SDK
description: Een overzicht van alle informatie die de Adobe Experience Platform SDK automatisch verzamelt.
keywords: verzamel informatie;context;configure;device;screenHeight;screenHeight;screenOrientation;screenOrientation;screenWidth;screenWidth;milieu;viewportHeight;viewportHeight;viewportWidth;viewport Breedte;crowserDetails;browser details;implementatieDetails;naam;versionContext;localTime;localTimezoneOffset;local zone Offset;timestamp;web;url;webPageDetails;webPage Details;webReferrer;webReferrer;landscape;portrait;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 6%

---


# Automatisch verzamelde gegevens

De SDK van het Web van Adobe Experience Platform verzamelt automatisch een aantal stukken informatie zonder enige speciale configuratie. Deze informatie kan echter desgewenst worden uitgeschakeld met de optie `context` in de opdracht `configure`. [Zie De SDK](../fundamentals/configuring-the-sdk.md) configureren. Hieronder volgt een lijst van deze gegevens. De naam tussen haakjes geeft de tekenreeks aan die moet worden gebruikt bij het configureren van de context.

## Apparaat (`device`)

Informatie over het apparaat. Dit omvat geen gegevens die op server-kant van het koord van de gebruikersagent kunnen worden gezocht.

### Schermhoogte

| **Pad in Payload:** | **Voorbeeld:** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

De hoogte in pixels van het scherm.

### Schermoriëntatie

| **Pad in Payload:** | **Mogelijke waarden:** |
| --------------------------------------- | ------------------------- |
| `events[].xdm.device.screenOrientation` | `landscape` of `portrait` |

De oriëntatie van het scherm.

### Schermbreedte

| **Pad in Payload:** | **Voorbeeld:** |
| --------------------------------- | ------------ |
| `events[].xdm.device.screenWidth` | `1440` |

De breedte van het scherm (in pixels).

## Omgeving (`environment`)

Details over de browseromgeving.

### Type omgeving

Browser

| **Pad in Payload:** | **Voorbeeld:** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

Het type omgeving waardoor de ervaring is ontstaan. Adobe Experience Platform Web SDK stelt dit altijd in op `browser`.

### Viewporthoogte

| **Pad in Payload:** | **Voorbeeld:** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

De hoogte van het inhoudsgebied van de browser (in pixels).

### Viewportbreedte

| **Pad in Payload:** | **Voorbeeld:** |
| ------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportWidth` | `642` |

De breedte van het inhoudsgebied van de browser (in pixels).

## Implementatiedetails

Informatie over de SDK die wordt gebruikt om de gebeurtenis te verzamelen.

### Naam

| **Pad in Payload:** | **Voorbeeld:** |
| ----------------------------------------- | --------------------------------------- |
| `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |

De id van de Software Development Kit (SDK).  In dit veld wordt een URI gebruikt om de unieke id&#39;s van verschillende softwarebibliotheken te verbeteren.

### Versie

| **Pad in Payload:** | **Voorbeeld:** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

### Omgeving

| **Pad in Payload:** | **Voorbeeld:** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |


## Context plaatsen (`placeContext`)

Informatie over de locatie van de eindgebruiker.

### Lokale tijd

| **Pad in Payload:** | **Voorbeeld:** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

Lokale tijdstempel voor de eindgebruiker in de vereenvoudigde uitgebreide ISO-indeling [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

### Verschuiving lokale tijdzone

| **Pad in Payload:** | **Voorbeeld:** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

Aantal minuten dat de gebruiker wordt verschoven ten opzichte van GMT.

## Tijdstempel

| **Pad in Payload:** | **Voorbeeld:** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

Het tijdstempel van de gebeurtenis.  Dit gedeelte van context kan niet worden verwijderd.

UTC-tijdstempel voor de eindgebruiker in de vereenvoudigde uitgebreide ISO-indeling [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

## Webdetails (`web`)

Details over de pagina waarop de gebruiker staat.

### Huidige pagina-URL

| **Pad in Payload:** | **Voorbeeld:** |
| ------------------------------------- | ------------------------------------ |
| `events[].xdm.web.webPageDetails.URL` | `https://somesite.com/somepage.html` |

De URL van de huidige pagina.

### Referrer-URL

| **Pad in Payload:** | **Voorbeeld:** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

De URL van de vorige bezochte pagina.
