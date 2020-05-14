---
title: Automatisch verzamelde informatie
seo-title: Gegevens die automatisch worden verzameld door de Adobe Experience Platform Web SDK
description: Beschrijving van alle informatie die de Adobe Experience Cloud SDK automatisch verzamelt
seo-description: Beschrijving van alle informatie die de Adobe Experience Cloud SDK automatisch verzamelt
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 3%

---


# Automatisch verzamelde informatie

De Adobe Experience Cloud SDK verzamelt automatisch een aantal gegevens zonder een speciale configuratie. Deze informatie kan echter desgewenst worden uitgeschakeld met de `context` optie in de `configure` opdracht. [Zie De SDK](../fundamentals/configuring-the-sdk.md)configureren. Hieronder volgt een lijst van deze gegevens. De naam tussen haakjes geeft de tekenreeks aan die moet worden gebruikt bij het configureren van de context.

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

Het type omgeving dat de ervaring heeft doorgemaakt. De Adobe Experience Platform SDK voor JavaScript wordt altijd ingesteld `browser`.

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
