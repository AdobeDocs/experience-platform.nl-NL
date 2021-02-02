---
keywords: Experience Platform;thuis;populaire onderwerpen;DULE;module
solution: Experience Platform
title: Aan de slag met de beleidsservice-API
topic: developer guide
description: Met de API voor beleidsservice kunt u verschillende bronnen maken en beheren die te maken hebben met Adobe Experience Platform Data Governance. Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan de Dienst API van het Beleid te maken.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# Aan de slag met de [!DNL Policy Service]-API

Met de [!DNL Policy Service]-API kunt u verschillende bronnen maken en beheren die gerelateerd zijn aan Adobe Experience Platform [!DNL Data Governance]. Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan [!DNL Policy Service] API te maken.

## Vereisten

Het gebruik van de ontwikkelaarsgids vereist een werkend inzicht in de diverse [!DNL Experience Platform] diensten betrokken bij het werken met de mogelijkheden van het Beheer van Gegevens. Lees de documentatie voor de volgende services voordat u begint met het werken met de [!DNL Policy Service API]:

* [[!DNL Data Governance]](../home.md): Het kader waardoor de naleving van het gegevensgebruik wordt  [!DNL Experience Platform] afgedwongen.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Sandboxen](../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## API-voorbeeldaanroepen lezen

De [!DNL Policy Service] API documentatie verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

## Vereiste koppen

De API documentatie vereist ook u om [authentificatieleerprogramma](https://www.adobe.com/go/platform-api-authentication-en) te hebben voltooid om vraag aan [!DNL Platform] eindpunten met succes te maken. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief bronnen die tot [!DNL Data Governance] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Raadpleeg de documentatie [sandbox-overzicht](../../sandboxes/home.md) voor meer informatie over sandboxen in [!DNL Platform].

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* `Content-Type: application/json`

## Core vs aangepaste bronnen

Binnen de [!DNL Policy Service] API, worden alle beleid en marketing acties bedoeld als of `core` of `custom` middelen.

`core` zijn de middelen die door Adobe worden bepaald en worden gehandhaafd, terwijl de  `custom` middelen die worden gecreeerd en door uw organisatie worden gehandhaafd, en daarom uniek en zichtbaar slechts aan uw organisatie IMS zijn. Als zodanig zijn het maken van lijsten en opzoekbewerkingen (`GET`) de enige bewerkingen die zijn toegestaan op `core`-bronnen, terwijl het weergeven, opzoeken en bijwerken van lijsten (`POST`, `PUT`, `PATCH` en `DELETE`) beschikbaar is voor `custom`-bronnen.

## Volgende stappen

Beginnen makend vraag gebruikend de Dienst API van het Beleid, selecteer één van de beschikbare eindpuntgidsen.