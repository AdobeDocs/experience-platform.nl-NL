---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;api;
solution: Experience Platform
title: Handleiding voor ontwikkelaars van Segmentatieservice
topic: developer guide
description: De volgende documentatie verstrekt extra informatie die u moet weten om met de Segmentatie API met succes te werken.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# Aan de slag met [!DNL Segmentation Service] {#getting-started}

Met Adobe Experience Platform [!DNL Segmentation Service] kunt u segmenten maken en in Adobe Experience Platform publiek maken op basis van uw [!DNL Real-time Customer Profile] gegevens.

De ontwikkelaarsgids vereist een werkend inzicht in de diverse [!DNL Experience Platform] diensten betrokken bij het gebruiken [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): Staat u toe om publiekssegmenten van [!DNL Real-time Customer Profile] gegevens te bouwen.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om te kunnen werken met de [!DNL Segmentation] API.

## API-voorbeeldaanroepen lezen

De API-documentatie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw aanvragen moeten worden opgemaakt. [!DNL Segmentation Service] Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

## Vereiste koppen

De API documentatie vereist ook u om de [authentificatiezelfstudie](../../tutorials/authentication.md) te hebben voltooid om vraag aan [!DNL Platform] eindpunten met succes te maken. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

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