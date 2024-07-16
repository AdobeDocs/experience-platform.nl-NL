---
keywords: Experience Platform;home;populaire onderwerpen;identiteitsservice-api;handleiding voor ontwikkelaars van identiteitsservices;regio
solution: Experience Platform
title: Identiteitsservice-API
description: Met de Identiteitsservice-API kunnen ontwikkelaars de identificatie van uw klanten via verschillende apparaten, kanalen en in de buurt van realtime beheren met behulp van identiteitsgrafieken in Adobe Experience Platform. Volg deze gids voor het uitvoeren van de belangrijkste bewerkingen met de API.
role: Developer
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 2%

---

# [!DNL Identity Service] API-handleiding

Adobe Experience Platform [!DNL Identity Service] beheert de identificatie van uw klanten op alle apparaten, via meerdere kanalen en bijna realtime in een identiteitsgrafiek in Adobe Experience Platform.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Identity Service]](../home.md): lost de fundamentele uitdaging op die door de fragmentatie van de gegevens van het klantenprofiel wordt gesteld. Het doet dit door identiteiten over apparaten en systemen te overbruggen waar de klanten met uw merk in wisselwerking staan.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): biedt een uniform, consumentenprofiel in real-time op basis van geaggregeerde gegevens van meerdere bronnen.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Platform] gegevens voor de klantervaring indeelt.

De volgende secties bevatten aanvullende informatie die u moet weten of die u zelf moet hebben om aanroepen naar de [!DNL Identity Service] API te kunnen uitvoeren.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Platform] APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in [!DNL Platform], zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

### Regionaal verpletteren

De [!DNL Identity Service] API gebruikt regio-specifieke eindpunten die de opneming van een `{REGION}` als deel van de verzoekweg vereisen. Tijdens de levering van uw organisatie, wordt een gebied bepaald en opgeslagen binnen uw organisatieprofiel. Als u het juiste gebied bij elk eindpunt gebruikt, zorgt u ervoor dat alle aanvragen die met de [!DNL Identity Service] API zijn gemaakt, naar het juiste gebied worden gerouteerd.

Er zijn momenteel twee gebieden die door [!DNL Identity Service] API&#39;s worden ondersteund: VA7 en NLD2.

In de onderstaande tabel worden voorbeeldpaden met behulp van gebieden weergegeven:

| Service | Regio: VA7 | Regio: NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span> platform-va7.adobe.</span> io/data/core/identity/{ENDPOINT} | https://</span> platform-nld2.adobe.</span> io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span> platform-va7.adobe.</span> io/data/core/idnamespace/{ENDPOINT} | https://</span> platform-nld2.adobe.</span> io/data/core/idnamespace {ENDPOINT} |

>[!NOTE]
>
>De verzoeken die zonder een gebied worden gemaakt te specificeren kunnen in vraag resulteren die aan het onjuiste gebied verplettert of vraag veroorzaken om onverwacht te ontbreken.

Als u het gebied niet kunt vinden binnen uw organisatieprofiel, gelieve uw systeembeheerder voor steun te contacteren.

## De API van [!DNL Identity Service] gebruiken

De parameters van de identiteit die in deze diensten worden gebruikt kunnen op één van twee manieren worden uitgedrukt; samenstelling of XID.

Samengestelde identiteiten zijn constructies die zowel de ID-waarde als de naamruimte omvatten. Wanneer het gebruiken van samengestelde identiteiten, kan namespace door of naam (`namespace.code`) of identiteitskaart (`namespace.id`) worden geleverd.

Wanneer een identiteit wordt voortgezet, genereert [!DNL Identity Service] een id die de native id of XID wordt genoemd en wijst deze toe. Alle variaties van de API&#39;s voor clusterbeheer en toewijzing ondersteunen zowel samengestelde identiteiten als XID in hun aanvragen en antwoorden. Een van de parameters is vereist - `xid` of combinatie van [`ns` of `nsid`] en `id` om deze API&#39;s te gebruiken.

Om de lading in reacties te beperken, passen APIs hun reacties aan het type van gebruikte identiteitsconstructie aan. Als u XID doorgeeft aan uw reacties, hebben XID&#39;s als u samengestelde identiteiten doorgeeft, volgt de reactie de structuur die in de aanvraag wordt gebruikt.

De voorbeelden in dit document hebben geen betrekking op de volledige functionaliteit van de [!DNL Identity Service] API. Voor volledige API, zie de [ Verwijzing van Swagger API ](https://www.adobe.io/experience-platform-apis/references/identity-service).

>[!NOTE]
>
>Alle geretourneerde identiteiten hebben de native XID-vorm wanneer native XID wordt gebruikt in de aanvraag. Het wordt aanbevolen het formulier ID/naamruimte te gebruiken. Voor meer informatie, zie de sectie over [ het krijgen van XID voor een identiteit ](./create-custom-namespace.md).

## Volgende stappen

Nu u de vereiste geloofsbrieven hebt verzameld, kunt u nu de rest gids van de ontwikkelaar blijven lezen. Elke sectie verstrekt belangrijke informatie betreffende hun eindpunten en toon voorbeeld API vraag voor het uitvoeren van verrichtingen CRUD aan. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen en behoorlijk geformatteerde lading toont, en een steekproefreactie voor een succesvolle vraag.
