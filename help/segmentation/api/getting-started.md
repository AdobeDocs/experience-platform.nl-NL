---
keywords: Experience Platform;thuis;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsdienst;api;
solution: Experience Platform
title: Aan de slag met de segmentatieservice-API
topic: developer guide
description: De volgende documentatie verstrekt extra informatie die u moet weten om met de Segmentatie API met succes te werken.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---


# Aan de slag met de segmentatieservice-API {#getting-started}

Met Adobe Experience Platform [!DNL Segmentation Service] kunt u segmenten samenstellen en in Adobe Experience Platform een publiek genereren op basis van uw [!DNL Real-time Customer Profile]-gegevens.

De ontwikkelaarsgids vereist een werkend inzicht in de diverse [!DNL Experience Platform] diensten betrokken bij het gebruiken [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): Staat u toe om publiekssegmenten van  [!DNL Real-time Customer Profile] gegevens te bouwen.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [Sandboxen](../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om te kunnen werken met de [!DNL Segmentation]-API.

## API-voorbeeldaanroepen lezen

De [!DNL Segmentation Service] API documentatie verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

## Vereiste koppen

De API documentatie vereist ook u om [authentificatieleerprogramma](https://www.adobe.com/go/platform-api-authentication-en) te hebben voltooid om vraag aan [!DNL Platform] eindpunten met succes te maken. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

- Autorisatie: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Raadpleeg de documentatie [sandboxen overzicht](../../sandboxes/home.md) voor meer informatie over het werken met sandboxen in [!DNL Experience Platform].

## Volgende stappen

Als u aanroepen wilt uitvoeren met de [!DNL Segmentation Service]-API, selecteert u een van de beschikbare eindpunthulplijnen met de linkernavigatie of in het [overzicht van de ontwikkelaarsgids](./overview.md)