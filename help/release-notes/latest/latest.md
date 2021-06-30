---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform voor 30 juni 2021.
doc-type: release notes
last-update: June 30, 2021
author: ens60013
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: fc916f87bf07e5eabf7d1681059406e2fea362e0
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 2%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 30 juni 2021**

Updates voor bestaande functies in Adobe Experience Platform:

- [Klantprofiel in realtime](#profile)
- [Sandboxen](#sandboxes)
- [Bronnen](#sources)

## Klantprofiel in realtime {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. [!DNL Profile] staat u toe om klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

| Functie | Beschrijving |
| ------- | ----------- |
| Workflowupdates voor samenvoegen | Wanneer het creëren van en het bijwerken van fusiebeleid in UI, kunnen de gebruikers nu voorproef 20 steekproefprofielen die op het unieschema worden gebaseerd. Op deze manier kunnen gebruikers een voorvertoning weergeven van de profielen van klanten voordat ze configuraties met samenvoegbeleid opslaan. Voor meer informatie, zie [de gids UI van het samenvoegbeleid](../../profile/merge-policies/ui-guide.md). |
| Rapport voor overlappen van identiteit | Het rapport voor identiteitsoverlap maakt deel uit van de Real-Time Customer Profile API en biedt zichtbaarheid in de samenstelling van de Profile Store. Gebruikend het `/previewsamplestatus` eindpunt, blootlegt het identiteitsoverlap rapport de identiteiten die het meest aan adresseerbare publiek bijdragen. Voor meer informatie gaat u naar de [voorbeeldstatus API-eindpuntgids](../../profile/api/preview-sample-status.md). |

Voor meer informatie over het profiel van de Klant in real time, met inbegrip van leerprogramma&#39;s en beste praktijken voor het werken met [!DNL Profile] gegevens, gelieve te beginnen door [Overzicht van het Profiel van de Klant in real time](../../profile/home.md) te lezen.

## Sandboxen {#sandboxes}

Adobe Experience Platform is ontworpen om toepassingen voor digitale beleving wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen. Om aan deze behoefte tegemoet te komen, biedt Experience Platform sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

| Functie | Beschrijving |
| ------- | ----------- |
| Verbeteringen voor het opnieuw instellen van de productiessandbox | U kunt nu productiesandboxen herstellen die voor bidirectioneel segment delen met Adobe Audience Manager of de Dienst van de Kern van de Audience worden gebruikt. Dit kan of van UI, of door de nieuwe `validationOnly` en `ignoreWarnings` parameters in API te gebruiken worden gedaan. Zie de zelfstudies over het opnieuw instellen van een sandbox in de UI](../../sandboxes/ui/user-guide.md) en [het opnieuw instellen van een sandbox in de API](../../sandboxes/api/sandboxes.md) voor meer informatie.[ |

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| ------- | ----------- |
| [!DNL Veeva CRM] (bèta) | U kunt [!DNL Veeva CRM] nu met Experience Platform verbinden gebruikend [!DNL Flow Service] API of UI. Zie [[!DNL Veeva CRM] connectoroverzicht](../../sources/connectors/crm/veeva.md) voor meer informatie. |
| Ondersteuning voor het controleren van streaming-gegevensstromen | U kunt de werkruimte van bronUI nu gebruiken om de activiteiten van de gegevensopname van het stromen bronnen met overeenkomstige metriek en status te controleren. Zie de zelfstudie over het [controleren van streaminggegevens](../../sources/tutorials/ui/monitor-streaming.md) voor meer informatie. |

Meer over bronnen leren, zie [bronnen overzicht](../../sources/home.md).
