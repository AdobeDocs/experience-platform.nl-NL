---
title: Aan de slag met de API voor auditquery
description: Met de API voor zoekopdrachten kunt u metrische gegevens voor verschillende Adobe Experience Platform-functies ophalen. Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan de Vraag API van de Vraag van de Controle te maken.
source-git-commit: 5b3459711f41430977f9d7b06f8b35801739207c
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Aan de slag met de API voor auditquery

Adobe Experience Platform staat u toe om gebruikersactiviteit voor diverse diensten en mogelijkheden in de vorm van de logboeken van controlegebeurtenissen te controleren. Elke actie die in een logboek wordt geregistreerd bevat meta-gegevens die op het actietype, datum en tijd, e-mailidentiteitskaart van de gebruiker die de actie, en extra attributen relevant voor het actietype uitvoerde.

Met de API van de auditquery kunt u gebruikersactiviteiten voor verschillende services en mogelijkheden controleren in de vorm van auditgebeurtenislogboeken. Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan de Vraag API van de Vraag van de Controle te maken.

## Vereisten

Als u auditgebeurtenissen wilt beheren, moet u beschikken over **[!UICONTROL View User Activity Log]** toegangsbeheermachtiging verleend (gevonden onder [!UICONTROL Data Governance] categorie). Raadpleeg voor meer informatie over het beheren van individuele machtigingen voor functies van Platforms de [toegangsbeheerdocumentatie](../../../../access-control/home.md).

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in de documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de gids voor het oplossen van problemen met Experience Platforms.

### Waarden verzamelen voor vereiste koppen

Voor deze handleiding is het vereist dat u de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) om met succes vraag aan Platform APIs te maken. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt. Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../../../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, en PATCH) bevatten vereisen een extra kopbal:

* Inhoudstype: application/json

## Volgende stappen

Beginnen het maken vraag gebruikend [!DNL Audit Query] API, gelieve te verwijzen naar [eindgebruikershandleiding voor gebeurtenissen](./events.md) en de [eindgebruikershandleiding exporteren](./export.md).
