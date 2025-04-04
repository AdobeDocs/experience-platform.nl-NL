---
keywords: Experience Platform;home;populaire onderwerpen;queryservice;Query-service;query
solution: Experience Platform
title: API-handleiding voor query-service
description: Met de API van de Query Service kunnen ontwikkelaars hun Adobe Experience Platform-gegevens opvragen met behulp van standaard SQL. Volg deze gids voor het uitvoeren van de belangrijkste bewerkingen met de API.
role: Developer
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 3%

---

# [!DNL Query Service] API-handleiding

Deze handleiding voor ontwikkelaars bevat stappen voor het uitvoeren van verschillende bewerkingen in de Adobe Experience Platform [!DNL Query Service] API.

## Aan de slag

Deze handleiding vereist een goed begrip van de verschillende Adobe Experience Platform-services die bij het gebruik van [!DNL Query Service] betrokken zijn.

- [[!DNL Query Service]](../home.md): biedt de mogelijkheid om query&#39;s uit te voeren op gegevenssets en de resulterende query&#39;s vast te leggen als nieuwe gegevenssets in [!DNL Experience Platform] .
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Experience Platform] gegevens voor de klantervaring indeelt.
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één [!DNL Experience Platform] -instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten voordat u [!DNL Query Service] kunt gebruiken met de API.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in deze documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Experience Platform] APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

- Autorisatie: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie bij het werken met zandbakken in [!DNL Experience Platform], zie de [ documentatie van het zandbakenoverzicht ](../../sandboxes/home.md).

## Voorbeeld-API-aanroepen

Nu u begrijpt welke headers u moet gebruiken, bent u klaar om aanroepen uit te voeren naar de [!DNL Query Service] API. De volgende documenten doorlopen de verschillende API-aanroepen die u met de API [!DNL Query Service] kunt maken. Elke voorbeeldvraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen toont, en een steekproefreactie.

- [Zoekopdrachten](queries.md)
- [Verbindingsparameters](connection-parameters.md)
- [Geplande query&#39;s](scheduled-queries.md)
- [Runs voor geplande vragen](runs-scheduled-queries.md)
- [Zoeksjablonen](query-templates.md)
- [Versnelde query&#39;s](./accelerated-queries.md)
- [Waarschuwingsabonnementen](./alert-subscriptions.md)

## Volgende stappen

Nu u hebt geleerd hoe u aanroepen kunt maken met de API [!DNL Query Service] , kunt u uw eigen niet-interactieve query&#39;s maken. Voor meer informatie over hoe te om vragen tot stand te brengen, te lezen gelieve de [ SQL verwijzingsgids ](../sql/overview.md).
