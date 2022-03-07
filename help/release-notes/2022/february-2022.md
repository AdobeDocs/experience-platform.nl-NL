---
title: Opmerkingen bij de release van Adobe Experience Platform
description: De meest recente releaseopmerkingen voor Adobe Experience Platform.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: d407d6bedbe0eb9b4dde229d990160c114fad472
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 23 februari 2022**

Updates voor bestaande functies in Adobe Experience Platform:

- [Gegevensverzameling](#data-collection)
- [[!DNL Identity Service]](#identity)
- [Bronnen](#sources)

## Gegevensverzameling {#data-collection}

Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden waar het kan worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeterde UI-workflow voor configuratie gegevensstroom | De workflow voor het maken van een nieuwe gegevensstroom in de gebruikersinterface voor gegevensverzameling is bijgewerkt. Wanneer u services toevoegt aan een gegevensstroom, worden alleen de services waartoe u toegang hebt, opgenomen in de lijst met opties. Zie de handleiding op [configureren van een gegevensstroom](../../edge/fundamentals/datastreams.md) voor meer informatie . |
| Gegevensvoorvoegsel voor gegevensverzameling | Als u de SDK van het Web van Adobe Experience Platform gebruikt, kunt u de mogelijkheden van de Prep van Gegevens nu hefboomwerking om uw gegevens aan de server van het Model van de Gegevens van de Ervaring (XDM) in kaart te brengen. Zie de sectie over [Gegevensvoorvoegsel voor gegevensverzameling](../../edge/fundamentals/datastreams.md#data-prep) in de gids voor gegevensstromen voor meer informatie. |
| Apparaat-id&#39;s van eerste partij | U kunt nu uw eigen apparaat-id&#39;s naar het Adobe Experience Platform Edge Network sturen wanneer u klantgegevens verzamelt met de SDK van het Web Platform, waarmee u een oplossing kunt vinden voor recente browserbeperkingen met betrekking tot de levensduur van cookies van derden. Zie de handleiding op [apparaat-id&#39;s van eerste partij](../../edge/identity/first-party-device-ids.md) voor meer informatie . |

Voor meer informatie over gegevensverzameling in Platform raadpleegt u de [overzicht van gegevensverzameling](../../collection/home.md).

## [!DNL Identity Service] {#identity}

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen worden gefragmenteerd, die elke individuele klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen.

Adobe Experience Platform [!DNL Identity Service] helpt u een beter inzicht te krijgen in uw klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen, zodat u in real time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe machtiging voor `view-identity-graph` | U kunt nu de opdracht `view-identity-graph` toestemming om te controleren of de gebruikers in uw organisatie de gegevens van de identiteitsgrafiek kunnen bekijken. Gebruikers zonder deze machtiging hebben geen toegang tot de viewer voor identiteitsgrafieken in de gebruikersinterface of bij toegang tot [!DNL Identity Service] API&#39;s die id&#39;s retourneren. Zie de [toegangsbeheeroverzicht](../../access-control/home.md) voor meer informatie over machtigingen. |

Meer algemene informatie over [!DNL Identity Service], verwijst u naar de [Overzicht van identiteitsservice](../../identity-service/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Bètabronnen die naar GA gaan | De volgende bronnen zijn gepromoveerd van bèta naar GA: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
