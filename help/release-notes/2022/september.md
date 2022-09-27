---
title: Opmerkingen bij de release van Adobe Experience Platform, september 2022
description: In de release van september 2022 staat een opmerking voor Adobe Experience Platform.
source-git-commit: db4f04c0af98fe053fbb770b2301f7d3e9d2bb1a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 1%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 28 september 2022**

Updates voor bestaande functies in Adobe Experience Platform:

- [Identiteitsservice](#identity-service)
- [Bronnen](#sources)

## Identiteitsservice {#identity-service}

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen gefragmenteerd zijn, die elke klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen.

Met de Adobe Experience Platform Identity Service kunt u uw klant en zijn gedrag beter zien door identiteiten tussen apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor het verwijderen van gegevenssets | De Dienst van de identiteit steunt nu dataset schrapping wanneer het verzoeken door [Catalogusservice-API](https://developer.adobe.com/experience-platform-apis/references/catalog/), UI of Data Hygiene. Lees de handleiding op [het schrappen van datasets in UI](../../catalog/datasets/user-guide.md#delete-a-dataset) voor meer informatie . |

Voor meer informatie over Identiteitsservice leest u de [Overzicht van identiteitsservice](../../identity-service/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Audience Manager segmentpopulatie impact op Real-time klantprofiel | De inname van grote populaties in het Audience Manager segment heeft een directe invloed op uw totale aantal profielen wanneer u eerst een segment van de Audience Manager naar het Platform verzendt gebruikend de bron van de Audience Manager. Dit betekent dat het selecteren van alle segmenten kan leiden tot een aantal profielen dat groter is dan uw gebruiksrechten voor licenties. Lees voor meer informatie de [Overzicht van bron Audience Manager](../../sources/connectors/adobe-applications/audience-manager.md). Voor informatie over uw licentiegebruik leest u de documentatie op [het gebruiken van het dashboard van het vergunningsgebruik](../../dashboards/guides/license-usage.md). |

Voor meer informatie over bronnen leest u de [overzicht van bronnen](../../sources/home.md).