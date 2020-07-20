---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handleiding voor ontwikkelaars van Segmentatieservice
topic: developer guide
translation-type: tm+mt
source-git-commit: aff81a4f3243ef77cbdfc776220a5de46e360084
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Getting started with [!DNL Segmentation Service] {#getting-started}

De Dienst van de Segmentatie van het Adobe Experience Platform staat u toe om segmenten te bouwen en publiek in Adobe Experience Platform van uw [!DNL Real-time Customer Profile] gegevens te produceren.

De ontwikkelaarsgids vereist een werkend inzicht in de diverse diensten van de Experience Platform betrokken bij het gebruiken [!DNL Segmentation Service].

- [!DNL Segmentation](../home.md): Staat u toe om publiekssegmenten van de gegevens van het Profiel van de Klant in real time te bouwen.
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
- [!DNL Real-time Customer Profile](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [Sandboxen](../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om te kunnen werken met de [!DNL Segmentation] API.

## API-voorbeeldaanroepen lezen

De API-documentatie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw aanvragen moeten worden opgemaakt. [!DNL Segmentation Service] Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Experience Platform te lezen.

## Vereiste koppen

De API documentatie vereist ook u om de [authentificatiezelfstudie](../../tutorials/authentication.md) te hebben voltooid om vraag aan Platform eindpunten met succes te maken. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in Experience Platform API-aanroepen, zoals hieronder wordt getoond:

- Autorisatie: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Voor alle aanvragen voor [!DNL Platform] API&#39;s is een header nodig die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Raadpleeg de documentatie bij het overzicht van [!DNL Experience Platform]sandboxen voor meer informatie over het werken met sandboxen in [de](../../sandboxes/home.md)sandboxen.

## Volgende stappen

Als u aanroepen wilt uitvoeren met de [!DNL Segmentation Service] API, selecteert u een van de beschikbare eindpunthulplijnen met behulp van de linkernavigatie of het overzicht van de [ontwikkelaarsgids](./overview.md)