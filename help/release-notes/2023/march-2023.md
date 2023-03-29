---
title: Opmerkingen bij de release van Adobe Experience Platform, februari 2023
description: In de release van maart 2023 staat Adobe Experience Platform vermeld.
source-git-commit: 44075e38664c01c64e7d09f5856353bff64becb5
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 29 maart 2023**

Updates voor bestaande functies in Adobe Experience Platform:

- [Gegevensverzameling](#data-collection)
- [Gegevensvoorbereiding](#data-prep)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe snelstartworkflow voor Meta Conversions API (Bèta) | Toegang tot nieuwe snelstartworkflows onder &quot;Aan de slag&quot; vanuit het startscherm van de gegevensverzameling. De [quick start workflow voor Meta Conversions API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) biedt klanten de mogelijkheid om gebeurtenisgegevens snel te verzamelen en door te sturen, servergegevens naar Meta voor conversie van advertenties in een paar eenvoudige stappen. |
| [!DNL Braze] extensie voor doorsturen van gebeurtenissen | De [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) Met de extensie voor het doorsturen van gebeurtenissen kunt u gegevens die zijn vastgelegd in het Adobe Experience Platform Edge-netwerk, benutten en verzenden naar [!DNL Braze] in de vorm van server-side-gebeurtenissen die de [!DNL Braze] Gebruikerstrack-API&#39;s. |
| [!DNL Mixpanel] extensie voor doorsturen van gebeurtenissen | De [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) Met de extensie kunnen klanten gebeurtenisberichten gebruiken om gebeurtenisgegevens vast te leggen in het Adobe Experience Platform Edge-netwerk en deze via de API Gebeurtenissen bijhouden naar Mixpanel te verzenden. |

{style="table-layout:auto"}

## Gegevensvoorbereiding {#data-prep}

Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model).

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe functies voor het coderen en decoderen van URL-tekenreeksen | <ul><li>De `get_url_encoded` Deze functie neemt een URL als invoer en vervangt of codeert speciale tekens door ASCII-tekens.</li><li>De `get_url_decoded` De functie neemt een URL als input en decodeert ASCII karakters in speciale karakters.</li></ul> Lees voor meer informatie de [Handleiding voor functies Data Prep](../../data-prep/functions.md). Lees de handleiding voor een uitgebreide lijst met gereserveerde tekens en de bijbehorende gecodeerde tekens [speciale tekens](../../data-prep/functions.md#special-characters). |

Voor meer informatie over Data Prep, gelieve te lezen [Overzicht van Data Prep](../../data-prep/home.md).

## Segmenteringsservice {#segmentation}

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. De segmenten kunnen op verslaggegevens (zoals demografische informatie) of tijdreeksgebeurtenissen worden gebaseerd die klanteninteractie met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Profielafmetingen | Om u een nauwkeurigere vertegenwoordiging van profielmetriek te geven, worden de lidmaatschapsuitsplitsing en de cijfers van de kroon gecombineerd en nu berekend over een periode van 24 uur. Meer informatie vindt u in de [Handleiding voor segmenteringsinterface](../../segmentation/ui/overview.md) |

{style="table-layout:auto"}

Voor meer informatie over [!DNL Segmentation Service], zie de [Overzicht van segmentatie](../../segmentation/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren en maakt het mogelijk die gegevens te structureren, te labelen en te verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Beta beschikbaarheid van [!DNL Chatlio] | De [!DNL Chatlio] De bron is nu beschikbaar in bèta. Gebruik de [!DNL Chatlio] bron om uw [!DNL Chatlio] gebeurtenisgegevens naar Experience Platform. Lees voor meer informatie de [[!DNL Chatlio] overzicht](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Beta beschikbaarheid van [!DNL Customer.io] | De [!DNL Customer.io] De bron is nu beschikbaar in bèta. Gebruik de [!DNL Customer.io] bron om gegevens van klantgebeurtenissen naar Experience Platform te streamen. Lees voor meer informatie de [[!DNL Customer.io] overzicht](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Beta beschikbaarheid van [!DNL Pendo] | De [!DNL Pendo] De bron is nu beschikbaar in bèta. Gebruik de [!DNL Pendo] bron om de analysegegevens van uw product naar het Experience Platform te streamen. Lees voor meer informatie de [[!DNL Pendo] overzicht](../../sources/connectors/analytics/pendo-webhook.md). |
| Ondersteuning voor conceptgegevensstromen | U kunt nu de Flow Service API gebruiken om uw gegevensstromen in te stellen op een conceptstatus. Tekeningen van gegevensstromen kunnen later met nieuwe informatie worden bijgewerkt en worden gepubliceerd. Lees voor meer informatie de handleiding op [gegevensstromen van bronnen instellen als concepten](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Voor meer informatie over bronnen leest u de [overzicht van bronnen](../../sources/home.md).
