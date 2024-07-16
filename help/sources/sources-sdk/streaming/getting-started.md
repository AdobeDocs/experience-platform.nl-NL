---
title: Aan de slag met Self-Serve Bronnen (Streaming SDK)
description: Dit document biedt een inleiding op de vereiste informatie die u moet weten voordat u een nieuwe bron probeert te maken met Self-Serve Sources (Streaming SDK).
exl-id: 6cc13279-ce0b-45bc-ad25-e2e6aafc2af0
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# Aan de slag met Self-Serve Bronnen (Streaming SDK)

>[!NOTE]
>
>Self-Serve Sources Streaming SDK bevindt zich in bèta. Gelieve te lezen het [ overzicht van bronnen ](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Met Self-Serve Sources (Streaming SDK) kunt u uw eigen bron integreren en streaming gegevens naar Adobe Experience Platform overbrengen. Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan [[!DNL Flow Service]  API ](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) te maken.

## Proces op hoog niveau

Het stapsgewijze proces voor het configureren van uw bron in Experience Platform wordt hieronder beschreven:

### Integratie

* [ creeer een nieuwe verbindingsspecificatie voor het stromen SDK ](create.md).
* [ werk de het stromen stroomspecificatie met uw nieuwe identiteitskaart van de verbindingsspecificatie ](update-flow-specs.md) bij.
* [ Test en leg uw het stromen bron ](submit.md) voor.

### Documentatie

* Begin documenterend uw bron, lees het [ overzicht bij het creëren van documentatie voor Zelfbediening Bronnen ](../documentation/doc-overview.md).
* Lees de gids op [ gebruikend de het Webinterface van GitHub ](../documentation/github.md) voor stappen op hoe te om documentatie tot stand te brengen die GitHub gebruikt.
* Lees de gids op [ gebruikend een tekstredacteur ](../documentation/text-editor.md) voor stappen op hoe te om documentatie tot stand te brengen gebruikend uw lokale machine.
* [ Gebruik het Streamen SDK API documentatiesjabloon om uw bron in API ](streaming-template-api.md) te documenteren.
* [ gebruik het het stromen SDK UI documentatiemalplaatje om uw bron in UI ](streaming-template-ui.md) te documenteren.

U kunt ook de onderstaande documentatiesjablonen downloaden:

* [API-documentatiesjabloon](../assets/streaming/streaming-template-api.zip)
* [UI-documentatiesjabloon](../assets/streaming/streaming-template-ui.zip)

## Vereisten

>[!IMPORTANT]
>
>De bron die u met Experience Platform integreert moet een webhaak kunnen steunen waaraan een eindpunt kan worden ingetekend, updates te verzenden.

Als u Self-Serve Sources (Streaming SDK) wilt gebruiken, moet u ervoor zorgen dat u toegang hebt tot een sandboxorganisatie die is ingericht met Adobe Experience Platform Sources.

Deze handleiding vereist ook een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [ Sandboxes ](../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

## API-voorbeeldaanroepen lezen

De Self-Serve Bronnen (Streaming SDK) en de [!DNL Flow Service] API-documentatie bieden voorbeeld-API-aanroepen om aan te tonen hoe uw aanvragen moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Experience Platform te lezen.

## Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in het platform, inclusief die van [!DNL Flow Service], zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in Platform, zie de [ zandbakdocumentatie ](../../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* `Content-Type: application/json`

## Volgende stappen

Beginnen creërend een nieuwe bron met Zelfbediening Bronnen (het stromen SDK), zie het leerprogramma op [ creërend een nieuwe bron ](./create.md).
