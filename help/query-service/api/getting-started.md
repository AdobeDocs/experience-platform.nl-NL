---
keywords: Experience Platform;home;popular topics;query service;Query service;query
solution: Experience Platform
title: Handleiding voor ontwikkelaars van Query Service
topic: query templates
description: Deze handleiding voor ontwikkelaars bevat stappen voor het uitvoeren van verschillende bewerkingen in de API van de Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 1%

---


# [!DNL Query Service] ontwikkelaarsgids

Deze handleiding voor ontwikkelaars bevat stappen voor het uitvoeren van verschillende bewerkingen in de Adobe Experience Platform [!DNL Query Service] API.

## Aan de slag

Deze handleiding vereist een goed begrip van de verschillende Adobe Experience Platform-services die bij het gebruik van deze handleiding betrokken zijn [!DNL Query Service].

- [[!DNL Query Service]](../home.md): Verstrekt de capaciteit om datasets te vragen en de resulterende vragen als nieuwe datasets binnen te vangen [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes te gebruiken [!DNL Query Service] API.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in deze documentatie voor steekproef API vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Experience Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Platform]

- Autorisatie: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Voor alle aanvragen voor [!DNL Platform] API&#39;s is een header nodig die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Raadpleeg de documentatie bij het overzicht van [!DNL Experience Platform]sandboxen voor meer informatie over het werken met sandboxen in [de](../../sandboxes/home.md)sandboxen.

## Voorbeeld-API-aanroepen

Nu u begrijpt welke kopballen aan gebruik, bent u bereid beginnen het voeren van vraag aan [!DNL Query Service] API. De volgende documenten gaan door de verschillende API-aanroepen die u met de [!DNL Query Service] API kunt maken. Elke voorbeeldvraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen toont, en een steekproefreactie.

- [Zoekopdrachten](queries.md)
- [Verbindingsparameters](connection-parameters.md)
- [Geplande query&#39;s](scheduled-queries.md)
- [Runs voor geplande vragen](runs-scheduled-queries.md)
- [Zoeksjablonen](query-templates.md)

## Volgende stappen

Nu u hebt geleerd hoe te om vraag te maken gebruikend [!DNL Query Service] API, kunt u uw eigen niet-interactieve vragen tot stand brengen. Lees voor meer informatie over het maken van query&#39;s de [SQL-naslaggids](../sql/overview.md).