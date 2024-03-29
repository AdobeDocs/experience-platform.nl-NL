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
>Self-Serve Sources Streaming SDK bevindt zich in bèta. Lees de [overzicht van bronnen](../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Met Self-Serve Sources (Streaming SDK) kunt u uw eigen bron integreren en streaming gegevens naar Adobe Experience Platform overbrengen. Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen vraag aan te maken [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Proces op hoog niveau

Het stapsgewijze proces voor het configureren van uw bron in Experience Platform wordt hieronder beschreven:

### Integratie

* [Een nieuwe verbindingsspecificatie maken voor de Streaming SDK](create.md).
* [Werk de streamingstroomspecificatie bij met uw nieuwe verbindingsspecificatie-id](update-flow-specs.md).
* [De streamingbron testen en verzenden](submit.md).

### Documentatie

* Als u de bron wilt documenteren, leest u de [overzicht bij het creëren van documentatie voor Zelfbediening Bronnen](../documentation/doc-overview.md).
* Lees de handleiding op [het gebruiken van de het Webinterface van GitHub](../documentation/github.md) voor stappen op hoe te om documentatie tot stand te brengen gebruikend GitHub.
* Lees de handleiding op [een teksteditor gebruiken](../documentation/text-editor.md) voor stappen voor het maken van documentatie met behulp van uw lokale computer.
* [Documentatiesjabloon van de Streaming SDK API gebruiken om uw bron in de API te documenteren](streaming-template-api.md).
* [Documentatiesjabloon van de Streaming SDK gebruiken om uw bron in de gebruikersinterface te documenteren](streaming-template-ui.md).

U kunt ook de onderstaande documentatiesjablonen downloaden:

* [API-documentatiesjabloon](../assets/streaming/streaming-template-api.zip)
* [UI-documentatiesjabloon](../assets/streaming/streaming-template-ui.zip)

## Vereisten

>[!IMPORTANT]
>
>De bron die u met Experience Platform integreert moet een webhaak kunnen steunen waaraan een eindpunt kan worden ingetekend, updates te verzenden.

Als u Self-Serve Sources (Streaming SDK) wilt gebruiken, moet u ervoor zorgen dat u toegang hebt tot een sandboxorganisatie die is ingericht met Adobe Experience Platform Sources.

Deze handleiding vereist ook een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de platformservices.
* [Sandboxen](../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één platforminstantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## API-voorbeeldaanroepen lezen

De Self-Serve Bronnen (Streaming SDK) en [!DNL Flow Service] API-documentatie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw aanvragen moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de gids voor het oplossen van problemen met Experience Platforms.

## Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar platform-API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle middelen in Platform, met inbegrip van die toebehoren aan [!DNL Flow Service], geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in Platform raadpleegt u de [sandbox-documentatie](../../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* `Content-Type: application/json`

## Volgende stappen

Als u een nieuwe bron wilt maken met Self-Serve Sources (Streaming SDK), raadpleegt u de zelfstudie op [een nieuwe bron maken](./create.md).
