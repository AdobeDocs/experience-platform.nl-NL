---
keywords: Experience Platform;home;populaire onderwerpen;DULE;module
solution: Experience Platform
title: Aan de slag met de API voor beleidsservice
description: Met de API voor beleidsservice kunt u verschillende bronnen maken en beheren die te maken hebben met Adobe Experience Platform Data Governance. Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan de Dienst API van het Beleid te maken.
role: Developer
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# Aan de slag met de [!DNL Policy Service] API

Met de API van [!DNL Policy Service] kunt u verschillende bronnen maken en beheren die te maken hebben met Adobe Experience Platform-gegevensbeheer. Dit document bevat een inleiding op de kernconcepten die u moet kennen voordat u de API van [!DNL Policy Service] aanroept.

## Vereisten

Het gebruik van de ontwikkelaarshandleiding vereist een goed begrip van de verschillende [!DNL Experience Platform] -services die betrokken zijn bij het werken met mogelijkheden voor gegevensbeheer. Voordat u met de [!DNL Policy Service API] begint te werken, raadpleegt u de documentatie voor de volgende services:

* [ Beheer van Gegevens ](../home.md): Het kader waardoor [!DNL Experience Platform] naleving van het gegevensgebruik afdwingt.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Experience Platform] gegevens voor de klantervaring indeelt.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
* [ Sandboxen ](../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

## API-voorbeeldaanroepen lezen

De API-documentatie van [!DNL Policy Service] biedt voorbeeld-API-aanroepen om aan te tonen hoe uw aanvragen moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

## Vereiste koppen

De API documentatie vereist u ook om het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) te voltooien om vraag aan [!DNL Experience Platform] eindpunten met succes te maken. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in [!DNL Experience Platform], inclusief bronnen die tot gegevensbeheer behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in [!DNL Experience Platform], zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).

Alle verzoeken die een lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* `Content-Type: application/json`

## Core vs aangepaste bronnen

Binnen de API van [!DNL Policy Service] worden alle beleidsregels en marketingacties `core` of `custom` bronnen genoemd.

`core` -bronnen zijn de bronnen die door Adobe worden gedefinieerd en onderhouden, terwijl `custom` -bronnen de bronnen zijn die door uw organisatie worden gemaakt en onderhouden en daarom uniek en alleen zichtbaar zijn voor uw organisatie. Het weergeven van lijsten en opzoekbewerkingen (`GET`) zijn daarom de enige bewerkingen die zijn toegestaan in `core` -bronnen, terwijl het weergeven, opzoeken en bijwerken van bewerkingen (`POST` , `PUT`, `PATCH` en `DELETE`) beschikbaar is voor `custom` -bronnen.

## Volgende stappen

Beginnen makend vraag gebruikend de Dienst API van het Beleid, selecteer één van de beschikbare eindpuntgidsen.
