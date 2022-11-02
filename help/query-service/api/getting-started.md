---
keywords: Experience Platform;thuis;populaire onderwerpen;de vraagdienst;de dienst van de vraag;vraag
solution: Experience Platform
title: API-handleiding voor query-service
topic-legacy: query templates
description: Met de API van de Query Service kunnen ontwikkelaars hun Adobe Experience Platform-gegevens opvragen met behulp van standaard SQL. Volg deze handleiding voor het uitvoeren van toetsbewerkingen met de API.
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: 9f458a327c0b72a5984161f13f02d09b7a2e610e
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---

# [!DNL Query Service] API-handleiding

Deze handleiding voor ontwikkelaars bevat stappen voor het uitvoeren van verschillende bewerkingen in de Adobe Experience Platform [!DNL Query Service] API.

## Aan de slag

Deze handleiding vereist een goed begrip van de verschillende Adobe Experience Platform-services die betrokken zijn bij het gebruik van [!DNL Query Service].

- [[!DNL Query Service]](../home.md): Verstrekt de capaciteit om datasets te vragen en de resulterende vragen als nieuwe datasets in te vangen [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten om deze te kunnen gebruiken [!DNL Query Service] met de API.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die in deze documentatie worden gebruikt voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

### Waarden verzamelen voor vereiste koppen

Om vraag te maken aan [!DNL Experience Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Platform] API-aanroepen, zoals hieronder wordt getoond:

- Autorisatie: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over het werken met sandboxen in [!DNL Experience Platform], zie de [sandboxen, overzichtsdocumentatie](../../sandboxes/home.md).

## Voorbeeld-API-aanroepen

Nu u begrijpt welke kopballen aan gebruik zijn, bent u bereid beginnen het richten van vraag aan [!DNL Query Service] API. De volgende documenten doorlopen de verschillende API-aanroepen die u kunt maken met de [!DNL Query Service] API. Elke voorbeeldvraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen toont, en een steekproefreactie.

- [Zoekopdrachten](queries.md)
- [Verbindingsparameters](connection-parameters.md)
- [Geplande query&#39;s](scheduled-queries.md)
- [Runs voor geplande vragen](runs-scheduled-queries.md)
- [Zoeksjablonen](query-templates.md)
- [Versnelde query&#39;s](./accelerated-queries.md)
- [Waarschuwingsabonnementen](./alert-subscriptions.md)

## Volgende stappen

Nu hebt u geleerd hoe te om vraag te maken gebruikend [!DNL Query Service] API, kunt u uw eigen niet-interactieve vragen tot stand brengen. Lees voor meer informatie over het maken van query&#39;s de [SQL-naslaggids](../sql/overview.md).
