---
keywords: Experience Platform;home;populaire onderwerpen;identiteitsservice-api;handleiding voor ontwikkelaars van identiteitsservices;regio
solution: Experience Platform
title: Identiteitsservice-API-handleiding
topic: API-handleiding
description: Met de Identiteitsservice-API kunnen ontwikkelaars de identificatie van uw klanten via verschillende apparaten, kanalen en in de buurt van realtime beheren met behulp van identiteitsgrafieken Adobe Experience Platform. Volg deze handleiding voor het uitvoeren van toetsbewerkingen met de API.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---


# [!DNL Identity Service] API-handleiding

Adobe Experience Platform [!DNL Identity Service] beheert de cross-device, cross-channel en bijna real-time identificatie van uw klanten in wat bekend staat als een identiteitsgrafiek binnen Adobe Experience Platform.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Identity Service]](../home.md): Oplost de fundamentele uitdaging die door de fragmentatie van gegevens van het klantenprofiel wordt gesteld. Het doet dit door identiteiten over apparaten en systemen te overbruggen waar de klanten met uw merk in wisselwerking staan.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, consumentenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Platform] klantenervaring worden georganiseerd.

De volgende secties verstrekken extra informatie die u zult moeten kennen of hebben aan hand om met succes vraag aan [!DNL Identity Service] API te maken.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u [!DNL Platform] API&#39;s wilt aanroepen, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Raadpleeg de documentatie [sandbox-overzicht](../../sandboxes/home.md) voor meer informatie over sandboxen in [!DNL Platform].

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

### Regionaal verpletteren

De [!DNL Identity Service] API gebruikt regio-specifieke eindpunten die de opneming van `{REGION}` als deel van de verzoekweg vereisen. Tijdens de provisioning van uw IMS-organisatie wordt een gebied bepaald en opgeslagen binnen uw IMS Org-profiel. Het gebruiken van het correcte gebied met elk eindpunt zorgt ervoor dat alle verzoeken die worden gemaakt gebruikend [!DNL Identity Service] API aan het aangewezen gebied worden verpletterd.

Er zijn momenteel twee gebieden die worden ondersteund door API&#39;s van [!DNL Identity Service]: VA7 en NLD2.

In de onderstaande tabel ziet u voorbeelden van paden die gebieden gebruiken:

| Service | Regio: VA7 | Regio: NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>De verzoeken die zonder een gebied worden gemaakt te specificeren kunnen in vraag resulteren die aan het onjuiste gebied verplettert of vraag veroorzaken om onverwacht te ontbreken.

Als u het gebied niet kunt vinden binnen uw IMS Org-profiel, gelieve uw systeembeheerder voor steun te contacteren.

## De API [!DNL Identity Service] gebruiken

De identiteitsparameters die in deze diensten worden gebruikt, kunnen op twee manieren worden uitgedrukt; composiet of XID.

Samengestelde identiteiten zijn constructies die zowel de ID-waarde als de naamruimte omvatten. Wanneer het gebruiken van samengestelde identiteiten, kan namespace door of naam (`namespace.code`) of identiteitskaart (`namespace.id`) worden geleverd.

Wanneer een identiteit wordt voortgeduurd, [!DNL Identity Service] produceert en wijst een identiteitskaart aan die identiteit toe, genoemd inheemse identiteitskaart, of XID. Alle variaties van de API&#39;s voor clusterbeheer en toewijzing ondersteunen zowel samengestelde identiteiten als XID in hun aanvragen en antwoorden. Een van de parameters is vereist - `xid` of combinatie van [`ns` of `nsid`] en `id` om deze API&#39;s te gebruiken.

Om de lading in reacties te beperken, passen APIs hun reacties aan het type van gebruikte identiteitsconstructie aan. Als u XID doorgeeft aan uw reacties, hebben XID&#39;s als u samengestelde identiteiten doorgeeft, volgt de reactie de structuur die in de aanvraag wordt gebruikt.

De voorbeelden in dit document hebben geen betrekking op de volledige functionaliteit van de [!DNL Identity Service]-API. Zie [Bron voor de volledige API.](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)

>[!NOTE]
>
>Alle geretourneerde identiteiten hebben de native XID-vorm wanneer native XID wordt gebruikt in de aanvraag. Het wordt aanbevolen het formulier ID/naamruimte te gebruiken. Zie de sectie over [het ophalen van de XID voor een identiteit](./create-custom-namespace.md) voor meer informatie.

## Volgende stappen

Nu u de vereiste geloofsbrieven hebt verzameld, kunt u nu de rest gids van de ontwikkelaar blijven lezen. Elke sectie verstrekt belangrijke informatie betreffende hun eindpunten en toon voorbeeld API vraag voor het uitvoeren van verrichtingen CRUD aan. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen en behoorlijk geformatteerde lading toont, en een steekproefreactie voor een succesvolle vraag.
