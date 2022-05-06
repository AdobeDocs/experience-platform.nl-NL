---
keywords: Experience Platform;home;populaire onderwerpen;identiteitsservice-api;handleiding voor ontwikkelaars van identiteitsservices;regio
solution: Experience Platform
title: Identiteitsservice-API-handleiding
topic-legacy: API guide
description: Met de Identiteitsservice-API kunnen ontwikkelaars de identificatie van uw klanten via verschillende apparaten, kanalen en in de buurt van realtime beheren met behulp van identiteitsgrafieken in Adobe Experience Platform. Volg deze handleiding voor het uitvoeren van toetsbewerkingen met de API.
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# [!DNL Identity Service] API-handleiding

Adobe Experience Platform [!DNL Identity Service] beheert de cross-device, cross-channel en bijna real-time identificatie van uw klanten in een zogenaamde identiteitsgrafiek in Adobe Experience Platform.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Identity Service]](../home.md): Oplost de fundamentele uitdaging die door de fragmentatie van gegevens van het klantenprofiel wordt gesteld. Het doet dit door identiteiten over apparaten en systemen te overbruggen waar de klanten met uw merk in wisselwerking staan.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, consumentenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Platform] organiseert de gegevens van de klantenervaring.

De volgende secties verstrekken extra informatie die u zult moeten kennen of hebben aan met succes vraag aan [!DNL Identity Service] API.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

### Waarden verzamelen voor vereiste koppen

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

### Regionaal verpletteren

De [!DNL Identity Service] API gebruikt regio-specifieke eindpunten die de opname van een `{REGION}` als onderdeel van het aanvraagpad. Tijdens de provisioning van uw IMS-organisatie wordt een gebied bepaald en opgeslagen binnen uw IMS Org-profiel. Het gebruiken van het correcte gebied met elk eindpunt zorgt ervoor dat alle die verzoeken gebruikend worden gemaakt [!DNL Identity Service] API worden naar het juiste gebied gerouteerd.

Er zijn momenteel twee gebieden die worden ondersteund door [!DNL Identity Service] API&#39;s: VA7 en NLD2.

In de onderstaande tabel worden voorbeeldpaden met behulp van gebieden weergegeven:

| Service | Regio: VA7 | Regio: NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>De verzoeken die zonder een gebied worden gemaakt te specificeren kunnen in vraag resulteren die aan het onjuiste gebied verplettert of vraag veroorzaken om onverwacht te ontbreken.

Als u het gebied niet kunt vinden binnen uw IMS Org-profiel, gelieve uw systeembeheerder voor steun te contacteren.

## Met de [!DNL Identity Service] API

De identiteitsparameters die in deze diensten worden gebruikt, kunnen op twee manieren worden uitgedrukt; composiet of XID.

Samengestelde identiteiten zijn constructies die zowel de ID-waarde als de naamruimte omvatten. Wanneer u samengestelde identiteiten gebruikt, kan de naamruimte worden opgegeven door een van de volgende namen (`namespace.code`) of ID (`namespace.id`).

Wanneer een identiteit wordt voortgeduurd, [!DNL Identity Service] Hiermee genereert en wijst u een id toe aan die identiteit, de native id of XID. Alle variaties van de API&#39;s voor clusterbeheer en toewijzing ondersteunen zowel samengestelde identiteiten als XID in hun aanvragen en antwoorden. Een van de parameters is vereist - `xid` of combinatie van [`ns` of `nsid`] en `id` om deze API&#39;s te gebruiken.

Om de lading in reacties te beperken, passen APIs hun reacties aan het type van gebruikte identiteitsconstructie aan. Als u XID doorgeeft aan uw reacties, hebben XID&#39;s als u samengestelde identiteiten doorgeeft, volgt de reactie de structuur die in de aanvraag wordt gebruikt.

In de voorbeelden in dit document wordt niet ingegaan op de volledige functionaliteit van de [!DNL Identity Service] API. Voor de volledige API raadpleegt u de [Referentie voor Tagger-API](https://www.adobe.io/experience-platform-apis/references/identity-service).

>[!NOTE]
>
>Alle geretourneerde identiteiten hebben de native XID-vorm wanneer native XID wordt gebruikt in de aanvraag. Het wordt aanbevolen het formulier ID/naamruimte te gebruiken. Zie de sectie over [XID ophalen voor een identiteit](./create-custom-namespace.md).

## Volgende stappen

Nu u de vereiste geloofsbrieven hebt verzameld, kunt u nu de rest gids van de ontwikkelaar blijven lezen. Elke sectie verstrekt belangrijke informatie betreffende hun eindpunten en toon voorbeeld API vraag voor het uitvoeren van verrichtingen CRUD aan. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen en behoorlijk geformatteerde lading toont, en een steekproefreactie voor een succesvolle vraag.
