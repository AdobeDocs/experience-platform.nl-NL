---
keywords: Experience Platform;thuis;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsdienst;api;
solution: Experience Platform
title: Aan de slag met de segmentatieservice-API
topic-legacy: developer guide
description: De volgende documentatie verstrekt extra informatie die u moet weten om met de Segmentatie API met succes te werken.
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: 8325ae6fd7d0013979e80d56eccd05b6ed6f5108
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---

# Aan de slag met de segmentatieservice-API {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] kunt u segmenten samenstellen en publiek in Adobe Experience Platform genereren op basis van uw [!DNL Real-time Customer Profile] gegevens.

De ontwikkelaarshandleiding vereist een goed begrip van de verschillende [!DNL Experience Platform] diensten in verband met het gebruik van [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): Hiermee kunt u publiekssegmenten maken op basis van [!DNL Real-time Customer Profile] gegevens.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring. Als u de segmentatie het beste wilt gebruiken, moet u ervoor zorgen dat uw gegevens als profielen en gebeurtenissen worden opgenomen volgens de [best practices voor gegevensmodellering](../../xdm/schema/best-practices.md).
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om te kunnen werken met de [!DNL Segmentation] API.

## API-voorbeeldaanroepen lezen

De [!DNL Segmentation Service] API-documentatie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw aanvragen moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

## Vereiste koppen

De API-documentatie vereist ook dat u de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) om met succes vraag te maken aan [!DNL Platform] eindpunten. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

- Autorisatie: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over het werken met sandboxen in [!DNL Experience Platform], zie de [sandboxen, overzichtsdocumentatie](../../sandboxes/home.md).

## Volgende stappen

Om vraag te maken gebruikend [!DNL Segmentation Service] API, selecteer één van de beschikbare eindpuntgidsen of gebruikend de linkernavigatie of binnen [overzicht van ontwikkelaarsgids](./overview.md)
