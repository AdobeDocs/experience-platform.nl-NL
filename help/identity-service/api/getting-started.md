---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Aan de slag
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Handleiding voor ontwikkelaars van Identity Service API

De identiteitsservice van Adobe Experience Platform beheert de identificatie van uw klanten over het hele apparaat, over het kanaal en bijna in realtime in een zogenaamde identiteitsgrafiek in het Adobe Experience Platform.

## Aan de slag

Voor deze handleiding is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

- [Identiteitsservice](../home.md): Oplost de fundamentele uitdaging die door de fragmentatie van gegevens van het klantenprofiel wordt gesteld. Het doet dit door identiteiten over apparaten en systemen te overbruggen waar de klanten met uw merk in wisselwerking staan.
- [Klantprofiel](../../profile/home.md)in realtime: Verstrekt een verenigd, consumentenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [XDM (Experience Data Model)](../../xdm/home.md): Het gestandaardiseerde kader waardoor Platform gegevens van de klantenervaring organiseert.

De volgende secties verstrekken extra informatie die u zult moeten kennen of hebben om met succes vraag aan de Dienst API van de Identiteit te maken.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

### Regionaal verpletteren

De identiteitsdienst API gebruikt regio-specifieke eindpunten die de opneming van een `{REGION}` als deel van de verzoekweg vereisen. Tijdens de provisioning van uw IMS-organisatie wordt een gebied bepaald en opgeslagen binnen uw IMS Org-profiel. Het gebruiken van het correcte gebied met elk eindpunt zorgt ervoor dat alle verzoeken die worden gemaakt gebruikend de Dienst API van de Identiteit worden verpletterd aan het aangewezen gebied.

Er zijn momenteel twee regio&#39;s die worden ondersteund door de identiteitsservice-API&#39;s: VA7 en NLD2.

In de onderstaande tabel worden voorbeeldpaden met behulp van gebieden weergegeven:

| Service | Regio: VA7 | Regio: NLD2 |
| ------ | -------- |--------- |
| Identiteitsservice-API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| Identiteitsnaamruimte-API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE] De verzoeken die zonder een gebied worden gemaakt te specificeren kunnen in vraag resulteren die aan het onjuiste gebied verplettert of vraag veroorzaken om onverwacht te ontbreken.

Als u het gebied niet kunt vinden binnen uw IMS Org-profiel, gelieve uw systeembeheerder voor steun te contacteren.

## De API voor identiteitsservice gebruiken

De identiteitsparameters die in deze diensten worden gebruikt, kunnen op twee manieren worden uitgedrukt; composiet of XID.

Samengestelde identiteiten zijn constructies die zowel de ID-waarde als de naamruimte omvatten. Wanneer u samengestelde identiteiten gebruikt, kan de naamruimte worden opgegeven met de naam (`namespace.code`) of de id (`namespace.id`).

Wanneer een identiteit wordt voortgeduurd, produceert de Dienst van de Identiteit en wijst een identiteitskaart aan die identiteit toe, genoemd inheemse identiteitskaart, of XID. Alle variaties van de API&#39;s voor clusterbeheer en toewijzing ondersteunen zowel samengestelde identiteiten als XID in hun aanvragen en antwoorden. Een van de parameters is vereist - `xid` of combinatie van [`ns` of `nsid`] en `id` om deze API&#39;s te gebruiken.

Om de lading in reacties te beperken, passen APIs hun reacties aan het type van gebruikte identiteitsconstructie aan. Als u XID doorgeeft aan uw reacties, hebben XID&#39;s als u samengestelde identiteiten doorgeeft, volgt de reactie de structuur die in de aanvraag wordt gebruikt.

De voorbeelden in dit document hebben geen betrekking op de volledige functionaliteit van de Identity Service API. Zie de [Swagger API-naslaggids](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)voor de volledige API.

>[!NOTE] Alle geretourneerde identiteiten hebben de native XID-vorm wanneer native XID wordt gebruikt in de aanvraag. Het wordt aanbevolen het formulier ID/naamruimte te gebruiken. Zie de sectie over het [ophalen van de XID voor een identiteit](./create-custom-namespace.md)voor meer informatie.

## Volgende stappen

Nu u de vereiste geloofsbrieven hebt verzameld, kunt u nu de rest gids van de ontwikkelaar blijven lezen. Elke sectie verstrekt belangrijke informatie betreffende hun eindpunten en toon voorbeeld API vraag voor het uitvoeren van verrichtingen CRUD aan. Elke vraag omvat het algemene **API formaat**, een steekproef **verzoek** die vereiste kopballen tonen en behoorlijk geformatteerde lading, en een steekproefreactie **** voor een succesvolle vraag.
