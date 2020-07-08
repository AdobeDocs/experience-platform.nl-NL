---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handleiding voor ontwikkelaars van Query Service
topic: query templates
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---


# Handleiding voor ontwikkelaars van Query Service

Deze ontwikkelaarsgids verstrekt stappen voor het uitvoeren van diverse verrichtingen in de Dienst API van de Vraag van het Adobe Experience Platform.

## Aan de slag

Deze gids vereist een werkend inzicht in de diverse diensten van het Adobe Experience Platform betrokken bij het gebruiken van de Dienst van de Vraag.

- [Query-service](../home.md): Verstrekt de capaciteit om datasets te vragen en de resulterende vragen als nieuwe datasets in Experience Platform te vangen.
- [XDM-systeem](../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
- [Sandboxen](../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om de Dienst van de Vraag met succes te gebruiken gebruikend API.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in deze documentatie voor steekproef API vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Experience Platform te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Experience Platform APIs te maken, moet u eerst het [authentificatieleerprogramma](../../tutorials/authentication.md)voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Platform API-aanroepen, zoals hieronder wordt getoond:

- Autorisatie: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in Experience Platform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor Platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Raadpleeg de documentatie bij het overzicht van [sandboxen voor meer informatie over het werken met sandboxen in Experience Platform](../../sandboxes/home.md).

## Voorbeeld-API-aanroepen

Nu u begrijpt welke kopballen aan gebruik, bent u bereid beginnen het richten vraag aan de Dienst API van de Vraag. De volgende documenten lopen door diverse API vraag u het gebruiken van de Dienst API van de Vraag kunt maken. Elke voorbeeldvraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen toont, en een steekproefreactie.

- [Zoekopdrachten](queries.md)
- [Verbindingsparameters](connection-parameters.md)
- [Geplande query&#39;s](scheduled-queries.md)
- [Runs voor geplande vragen](runs-scheduled-queries.md)
- [Zoeksjablonen](query-templates.md)

## Volgende stappen

Nu u hebt geleerd hoe te om vraag te maken gebruikend de Dienst API van de Vraag, kunt u uw eigen niet-interactieve vragen tot stand brengen. Lees voor meer informatie over het maken van query&#39;s de [SQL-naslaggids](../sql/overview.md).