---
keywords: Experience Platform;home;popular topics;DULE;dule
solution: Experience Platform
title: Aan de slag met de beleidsservice-API
topic: developer guide
description: Met de API voor beleidsservice kunt u verschillende bronnen maken en beheren die te maken hebben met Adobe Experience Platform Data Governance. Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan de Dienst API van het Beleid te maken.
translation-type: tm+mt
source-git-commit: 3376d6cace9ab196f457e2bf7b84cde06693103c
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---


# Getting started with the [!DNL Policy Service] API

Met de [!DNL Policy Service] API kunt u verschillende bronnen voor Adobe Experience Platform maken en beheren [!DNL Data Governance]. Dit document biedt een inleiding tot de kernconcepten u moet kennen alvorens te proberen om vraag aan [!DNL Policy Service] API te maken.

## Vereisten

Het gebruik van de ontwikkelaarsgids vereist een werkend inzicht in de diverse [!DNL Experience Platform] diensten betrokken bij het werken met de mogelijkheden van het Beheer van Gegevens. Voordat u met de [!DNL Policy Service API]toepassing begint te werken, raadpleegt u de documentatie voor de volgende services:

* [[!DNL Data Governance]](../home.md): Het kader waarmee de naleving van het gegevensgebruik wordt [!DNL Experience Platform] afgedwongen.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## API-voorbeeldaanroepen lezen

De API-documentatie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw aanvragen moeten worden opgemaakt. [!DNL Policy Service] Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

## Vereiste koppen

De API documentatie vereist ook u om de [authentificatiezelfstudie](../../tutorials/authentication.md) te hebben voltooid om vraag aan [!DNL Platform] eindpunten met succes te maken. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief de bronnen die tot [!DNL Data Governance]behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Zie de documentatie over het [!DNL Platform]sandboxoverzicht voor meer informatie over sandboxen in [de](../../sandboxes/home.md)sandbox.

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* `Content-Type: application/json`

## Core vs aangepaste bronnen

Binnen de [!DNL Policy Service] API worden alle beleid- en marketingacties ofwel `core` ofwel `custom` bronnen genoemd.

`core` zijn de middelen die door Adobe worden bepaald en worden gehandhaafd, terwijl de `custom` middelen die worden gecreeerd en door uw organisatie worden gehandhaafd, en daarom uniek en zichtbaar slechts aan uw organisatie IMS zijn. Als dusdanig, zijn de lijst en de raadplegingsverrichtingen (`GET`) de enige verrichtingen toegestaan op `core` middelen, terwijl de lijsten, de raadpleging en de updateverrichtingen (`POST`, `PUT`, `PATCH`, en `DELETE`) voor `custom` middelen beschikbaar zijn.

## Volgende stappen

Beginnen makend vraag gebruikend de Dienst API van het Beleid, selecteer één van de beschikbare eindpuntgidsen.