---
title: Aan de slag met de API voor auditquery
description: Met de API voor zoekopdrachten kunt u metrische gegevens voor verschillende Adobe Experience Platform-functies ophalen. Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan de Vraag API van de Vraag van de Controle te maken.
role: Developer
feature: Audits, API
exl-id: 20eab0a8-98f7-4fee-8f91-88324e54ab18
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Aan de slag met de API voor auditquery

Adobe Experience Platform staat u toe om gebruikersactiviteit voor diverse diensten en mogelijkheden in de vorm van de logboeken van controlegebeurtenissen te controleren. Elke actie die in een logboek wordt geregistreerd bevat meta-gegevens die op het actietype, datum en tijd, e-mailidentiteitskaart van de gebruiker die de actie, en extra attributen relevant voor het actietype uitvoerde.

Met de API van de auditquery kunt u gebruikersactiviteiten voor verschillende services en mogelijkheden controleren in de vorm van auditgebeurtenislogboeken. Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan de Vraag API van de Vraag van de Controle te maken.

## Vereisten

Voor het beheer van auditgebeurtenissen moet u de toegangsbeheermachtiging van **[!UICONTROL View User Activity Log]** hebben (deze kunt u vinden onder de categorie [!UICONTROL Data Governance] ). Leren hoe te om individuele toestemmingen voor de eigenschappen van Experience Platform te beheren, gelieve te verwijzen naar de [ documentatie van de toegangscontrole ](../../../../access-control/home.md).

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in de documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van Experience Platform te lezen.

### Waarden verzamelen voor vereiste koppen

Deze gids vereist u om het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) te voltooien om vraag aan Experience Platform APIs met succes te maken. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt. Voor meer informatie over zandbakken in [!DNL Experience Platform], zie de [ documentatie van het zandbakoverzicht ](../../../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een lading (POST, PUT, en PATCH) bevatten vereisen een extra kopbal:

* Inhoudstype: application/json

## Volgende stappen

Begin makend vraag gebruikend [!DNL Audit Query] API, gelieve te verwijzen naar de [ gids van het gebeurteniseindpunt ](./events.md) en de [ gids van het uitvoereindpunt ](./export.md).
