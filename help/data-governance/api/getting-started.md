---
keywords: Experience Platform;thuis;populaire onderwerpen;DULE;module
solution: Experience Platform
title: Aan de slag met de API voor beleidsservice
topic-legacy: developer guide
description: Met de API voor beleidsservice kunt u verschillende bronnen maken en beheren die te maken hebben met Adobe Experience Platform Data Governance. Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan de Dienst API van het Beleid te maken.
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# Aan de slag met de [!DNL Policy Service] API

De [!DNL Policy Service] Met API kunt u verschillende bronnen maken en beheren die te maken hebben met Adobe Experience Platform Data Governance. Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen vraag aan te maken [!DNL Policy Service] API.

## Vereisten

Voor het gebruik van de handleiding voor ontwikkelaars is een goed begrip van de verschillende [!DNL Experience Platform] diensten die betrokken zijn bij het werken met mogelijkheden voor gegevensbeheer. Voordat u begint te werken met de [!DNL Policy Service API]Raadpleeg de documentatie bij de volgende services:

* [Gegevensbeheer](../home.md): Het kader waarbinnen [!DNL Experience Platform] dwingt gegevensgebruiksnaleving af.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## API-voorbeeldaanroepen lezen

De [!DNL Policy Service] API-documentatie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw aanvragen moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

## Vereiste koppen

De API-documentatie vereist ook dat u de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) om met succes vraag te maken aan [!DNL Platform] eindpunten. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in [!DNL Experience Platform], met inbegrip van de sandboxen die tot gegevensbeheer behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* `Content-Type: application/json`

## Core vs aangepaste bronnen

Binnen de [!DNL Policy Service] API, alle beleid en marketingacties worden aangeduid als `core` of `custom` middelen.

`core` de middelen zijn die welke door Adobe worden gedefinieerd en gehandhaafd, terwijl `custom` bronnen zijn bronnen die door uw organisatie worden gemaakt en onderhouden en zijn daarom uniek en alleen zichtbaar voor uw IMS-organisatie. Als dusdanig, lijst en raadplegingsverrichtingen (`GET`) zijn de enige bewerkingen die zijn toegestaan op `core` bronnen, terwijl bewerkingen voor het weergeven, opzoeken en bijwerken (`POST`, `PUT`, `PATCH`, en `DELETE`) is beschikbaar voor `custom` middelen.

## Volgende stappen

Beginnen makend vraag gebruikend de Dienst API van het Beleid, selecteer één van de beschikbare eindpuntgidsen.
