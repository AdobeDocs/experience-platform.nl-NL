---
keywords: Experience Platform;home;popular topics;identity service api;identity service developer guide;region
solution: Experience Platform
title: Aan de slag
topic: API guide
description: 'De identiteitsservice van Adobe Experience Platform beheert de identificatie van uw klanten op verschillende apparaten, in verschillende kanalen en bijna realtime in een identiteitsgrafiek in Adobe Experience Platform. '
translation-type: tm+mt
source-git-commit: fa667d86c089c692f22cfd1b46f3f11b6e9a68d7
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 1%

---


# [!DNL Identity Service] Handleiding voor API-ontwikkelaars

Adobe Experience Platform [!DNL Identity Service] beheert de identificatie van uw klanten op alle apparaten, via meerdere kanalen en bijna realtime in een identiteitsgrafiek in Adobe Experience Platform.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Identity Service]](../home.md): Oplost de fundamentele uitdaging die door de fragmentatie van gegevens van het klantenprofiel wordt gesteld. Het doet dit door identiteiten over apparaten en systemen te overbruggen waar de klanten met uw merk in wisselwerking staan.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, consumentenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Platform] georganiseerd.

De volgende secties verstrekken extra informatie die u zult moeten kennen of hebben om met succes vraag aan [!DNL Identity Service] API te maken.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Zie de documentatie over het [!DNL Platform]sandboxoverzicht voor meer informatie over sandboxen in [de](../../sandboxes/home.md)sandbox.

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

### Regionaal verpletteren

De [!DNL Identity Service] API gebruikt regio-specifieke eindpunten die de opneming van een `{REGION}` als deel van de verzoekweg vereisen. Tijdens de provisioning van uw IMS-organisatie wordt een gebied bepaald en opgeslagen binnen uw IMS Org-profiel. Het gebruiken van het correcte gebied met elk eindpunt zorgt ervoor dat alle verzoeken die gebruikend API worden gemaakt aan het aangewezen gebied worden verpletterd. [!DNL Identity Service]

Er zijn momenteel twee gebieden die door API&#39; [!DNL Identity Service] s worden ondersteund: VA7 en NLD2.

In de onderstaande tabel ziet u voorbeelden van paden die gebieden gebruiken:

| Service | Regio: VA7 | Regio: NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>De verzoeken die zonder een gebied worden gemaakt te specificeren kunnen in vraag resulteren die aan het onjuiste gebied verplettert of vraag veroorzaken om onverwacht te ontbreken.

Als u het gebied niet kunt vinden binnen uw IMS Org-profiel, gelieve uw systeembeheerder voor steun te contacteren.

## De [!DNL Identity Service] API gebruiken

De identiteitsparameters die in deze diensten worden gebruikt, kunnen op twee manieren worden uitgedrukt; composiet of XID.

Samengestelde identiteiten zijn constructies die zowel de ID-waarde als de naamruimte omvatten. Wanneer u samengestelde identiteiten gebruikt, kan de naamruimte worden opgegeven met de naam (`namespace.code`) of de id (`namespace.id`).

Wanneer een identiteit wordt voortgeduurd, [!DNL Identity Service] produceert en wijst een identiteitskaart aan die identiteit toe, genoemd inheemse identiteitskaart, of XID. Alle variaties van de API&#39;s voor clusterbeheer en toewijzing ondersteunen zowel samengestelde identiteiten als XID in hun aanvragen en antwoorden. Een van de parameters is vereist - `xid` of combinatie van [`ns` of `nsid`] en `id` om deze API&#39;s te gebruiken.

Om de lading in reacties te beperken, passen APIs hun reacties aan het type van gebruikte identiteitsconstructie aan. Als u XID doorgeeft aan uw reacties, hebben XID&#39;s als u samengestelde identiteiten doorgeeft, volgt de reactie de structuur die in de aanvraag wordt gebruikt.

De voorbeelden in dit document hebben geen betrekking op de volledige functionaliteit van de [!DNL Identity Service] API. Zie de [Swagger API-naslaggids](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)voor de volledige API.

>[!NOTE]
>
>Alle geretourneerde identiteiten hebben de native XID-vorm wanneer native XID wordt gebruikt in de aanvraag. Het wordt aanbevolen het formulier ID/naamruimte te gebruiken. Zie de sectie over het [ophalen van de XID voor een identiteit](./create-custom-namespace.md)voor meer informatie.

## Volgende stappen

Nu u de vereiste geloofsbrieven hebt verzameld, kunt u nu de rest gids van de ontwikkelaar blijven lezen. Elke sectie verstrekt belangrijke informatie betreffende hun eindpunten en toon voorbeeld API vraag voor het uitvoeren van verrichtingen CRUD aan. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen en behoorlijk geformatteerde lading toont, en een steekproefreactie voor een succesvolle vraag.
