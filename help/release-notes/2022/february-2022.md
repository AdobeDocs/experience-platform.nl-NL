---
title: Opmerkingen bij de release van Adobe Experience Platform
description: De meest recente releaseopmerkingen voor Adobe Experience Platform.
source-git-commit: 762a4b7336f1c26b79883db9484d8f5fc7bff53c
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 23 februari 2022**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Identity Service]](#identity)
- [Bronnen](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [!DNL Data Prep] ondersteuning voor Adobe Analytics-bronaansluiting | De Adobe Analytics-bronaansluiting ondersteunt nu Data Prep-functies, zodat u uw Analytics-rapport-suite-gegevens kunt toewijzen aan een doel-XDM-schema wanneer u een gegevensstroom maakt. Zie de zelfstudie aan [een analytische bronaansluiting maken](../../sources/tutorials/ui/create/adobe-applications/analytics.md) voor meer informatie . |

Voor meer informatie over [!DNL Data Prep], zie de [[!DNL Data Prep] overzicht](../../data-prep/home.md).

## [!DNL Identity Service] {#identity}

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen worden gefragmenteerd, die elke individuele klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen.

Adobe Experience Platform [!DNL Identity Service] helpt u een beter inzicht te krijgen in uw klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen, zodat u in real time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe machtiging voor `view-identity-graph` | U kunt nu de opdracht `view-identity-graph` toestemming om te controleren of de gebruikers in uw organisatie de gegevens van de identiteitsgrafiek kunnen bekijken. Gebruikers zonder deze machtiging hebben geen toegang tot de viewer voor identiteitsgrafieken in de gebruikersinterface of bij toegang tot [!DNL Identity Service] API&#39;s die id&#39;s retourneren. Zie de [toegangsbeheeroverzicht](../../access-control/home.md) voor meer informatie over machtigingen. |

Meer algemene informatie over [!DNL Identity Service], verwijst u naar de [Overzicht van identiteitsservice](../../identity-service/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| --- | --- |
| Bètabronnen die naar GA gaan | De volgende bronnen zijn gepromoveerd van bèta naar GA: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
