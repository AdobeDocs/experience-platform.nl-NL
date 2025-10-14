---
keywords: Experience Platform;home;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsservice;api;
solution: Experience Platform
title: Aan de slag met de segmentatieservice-API
description: De volgende documentatie verstrekt extra informatie die u moet weten om met de Segmentatie API met succes te werken.
role: Developer
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Aan de slag met de segmentatieservice-API {#getting-started}

Met Adobe Experience Platform [!DNL Segmentation Service] kunt u een publiek maken aan de hand van segmentdefinities of andere bronnen in Adobe Experience Platform op basis van uw [!DNL Real-Time Customer Profile] -gegevens.

De ontwikkelaarshandleiding vereist een goed begrip van de verschillende [!DNL Experience Platform] -services die bij het gebruik van [!DNL Segmentation Service] betrokken zijn.

- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): hiermee kunt u soorten publiek maken op basis van [!DNL Real-Time Customer Profile] -gegevens.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Experience Platform] gegevens voor de klantervaring indeelt. Om het beste gebruik van Segmentatie te maken, gelieve te verzekeren uw gegevens als profielen en gebeurtenissen volgens de [&#x200B; beste praktijken voor gegevens modellering &#x200B;](../../xdm/schema/best-practices.md) worden opgenomen.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
- [&#x200B; Sandboxen &#x200B;](../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om te kunnen werken met de API van [!DNL Segmentation] .

## API-voorbeeldaanroepen lezen

De API-documentatie van [!DNL Segmentation Service] biedt voorbeeld-API-aanroepen om aan te tonen hoe uw aanvragen moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [&#x200B; hoe te om voorbeeld API vraag &#x200B;](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

## Vereiste koppen

De API documentatie vereist u ook om het [&#x200B; authentificatieleerprogramma &#x200B;](https://www.adobe.com/go/platform-api-authentication-en) te voltooien om vraag aan [!DNL Experience Platform] eindpunten met succes te maken. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

- Autorisatie: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie bij het werken met zandbakken in [!DNL Experience Platform], zie de [&#x200B; documentatie van het zandbakenoverzicht &#x200B;](../../sandboxes/home.md).

## Volgende stappen

Aan het maken vraag gebruikend [!DNL Segmentation Service] API, selecteer één van de beschikbare eindpuntgidsen of gebruikend de linkernavigatie of binnen het [&#x200B; overzicht van de ontwikkelaarsgids &#x200B;](./overview.md)
