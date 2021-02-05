---
keywords: Experience Platform;home;populaire onderwerpen;batch-opname;Batch-opname;partiële inname;Partiële inname;Fout ophalen;Fout ophalen;Onvolledige batch-opname;gedeeltelijke batch-opname;gedeeltelijke;Inslitie;Ingestie;
solution: Experience Platform
title: Overzicht van partiële batchverwerking
topic: overview
description: Dit document bevat een zelfstudie voor het beheren van gedeeltelijke batch-opname.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 0%

---


# Gedeeltelijke batch ingestie

Gedeeltelijke batch-opname is de mogelijkheid om gegevens met fouten in te voeren, tot een bepaalde drempel. Met deze functie kunnen gebruikers al hun juiste gegevens in Adobe Experience Platform opnemen terwijl al hun onjuiste gegevens afzonderlijk worden opgeslagen, samen met informatie over waarom de gegevens ongeldig zijn.

Dit document bevat een zelfstudie voor het beheren van gedeeltelijke batch-opname.

## Aan de slag

Deze zelfstudie vereist een praktische kennis van de verschillende Adobe Experience Platform-services die betrokken zijn bij gedeeltelijke batchopname. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [Inname](./overview.md) in batch: De methode die gegevens uit gegevensbestanden, zoals CSV en Parquet,  [!DNL Platform] opneemt en opslaat.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Platform] klantenervaring worden georganiseerd.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan [!DNL Platform] APIs te maken.

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

## Een batch inschakelen voor gedeeltelijke batchinvoer in de API {#enable-api}

>[!NOTE]
>
>In deze sectie wordt beschreven hoe u een batch voor gedeeltelijke batch-opname via de API inschakelt. Voor instructies over het gebruiken van UI, te lezen gelieve [een partij voor gedeeltelijke partijopname in de stap UI](#enable-ui) toelaten.

U kunt een nieuwe partij tot stand brengen met gedeeltelijke toegelaten opname.

Om een nieuwe partij tot stand te brengen, volg de stappen in [batch ingestion developer guide](./api-overview.md). Als u de stap **[!UICONTROL Batch maken]** hebt bereikt, voegt u het volgende veld toe aan de hoofdtekst van de aanvraag:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `enableErrorDiagnostics` | Een vlag die [!DNL Platform] toestaat om gedetailleerde foutenmeldingen over uw partij te produceren. |
| `partialIngestionPercentage` | Het percentage van aanvaardbare fouten vóór de volledige partij zal ontbreken. In dit voorbeeld kan maximaal 5% van de batch fouten zijn voordat deze mislukt. |


## Een batch voor gedeeltelijke batchinvoer inschakelen in de gebruikersinterface {#enable-ui}

>[!NOTE]
>
>In deze sectie wordt beschreven hoe u een batch voor gedeeltelijke batchinvoer via de gebruikersinterface inschakelt. Als u al een batch voor gedeeltelijke batch-opname hebt ingeschakeld met de API, kunt u verdergaan met de volgende sectie.

Om een partij voor gedeeltelijke opname door [!DNL Platform] UI toe te laten, kunt u een nieuwe partij door bronverbindingen tot stand brengen, een nieuwe partij in een bestaande dataset tot stand brengen, of een nieuwe partij door &quot;[!UICONTROL Kaart CSV aan XDM stroom]&quot;tot stand brengen.

### Nieuwe bronverbinding maken {#new-source}

Om een nieuwe bronverbinding tot stand te brengen, volg de vermelde stappen in [Bronoverzicht](../../sources/home.md). Wanneer u de **[!UICONTROL Dataflow detail]** stap bereikt, neem nota van **[!UICONTROL Gedeeltelijke opname]** en **[!UICONTROL Error diagnostics]** gebieden.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

Met de schakeloptie **[!UICONTROL Gedeeltelijke opname]** kunt u het gebruik van gedeeltelijke batch-opname in- of uitschakelen.

De **[!UICONTROL Foutdiagnostiek]** schakelt alleen in wanneer de **[!UICONTROL Partiële opname]** schakelt uit. Met deze functie kan [!DNL Platform] gedetailleerde foutberichten genereren over ingesloten batches. Als **[!UICONTROL Gedeeltelijke opname]** schakelt, wordt de verbeterde foutdiagnostiek automatisch afgedwongen.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Met de **[!UICONTROL Foutdrempel]** kunt u het percentage acceptabele fouten instellen voordat de gehele batch mislukt. Deze waarde is standaard ingesteld op 5%.

### Een bestaande gegevensset {#existing-dataset} gebruiken

Om een bestaande dataset te gebruiken, begin door een dataset te selecteren. De zijbalk rechts vult informatie over de gegevensset.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

Met de schakeloptie **[!UICONTROL Gedeeltelijke opname]** kunt u het gebruik van gedeeltelijke batch-opname in- of uitschakelen.

De **[!UICONTROL Foutdiagnostiek]** schakelt alleen in wanneer de **[!UICONTROL Partiële opname]** schakelt uit. Met deze functie kan [!DNL Platform] gedetailleerde foutberichten genereren over ingesloten batches. Als **[!UICONTROL Gedeeltelijke opname]** schakelt, wordt de verbeterde foutdiagnostiek automatisch afgedwongen.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Met de **[!UICONTROL Foutdrempel]** kunt u het percentage acceptabele fouten instellen voordat de gehele batch mislukt. Deze waarde is standaard ingesteld op 5%.

Nu, kunt u gegevens uploaden gebruikend **voeg gegevens** knoop toe, en het zal worden opgenomen gebruikend gedeeltelijke opname.

### Gebruik &quot;[!UICONTROL CSV aan XDM schema]&quot;stroom {#map-flow}

Als u de stroom &quot;[!UICONTROL CSV toewijzen aan XDM-schema]&quot; wilt gebruiken, voert u de vermelde stappen uit in de zelfstudie [Een CSV-bestand toewijzen](../tutorials/map-a-csv-file.md). Als u de stap **[!UICONTROL Gegevens toevoegen]** hebt bereikt, neemt u nota van de velden **[!UICONTROL Gedeeltelijke opname]** en **[!UICONTROL Foutdiagnose]**.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

Met de schakeloptie **[!UICONTROL Gedeeltelijke opname]** kunt u het gebruik van gedeeltelijke batch-opname in- of uitschakelen.

De **[!UICONTROL Foutdiagnostiek]** schakelt alleen in wanneer de **[!UICONTROL Partiële opname]** schakelt uit. Met deze functie kan [!DNL Platform] gedetailleerde foutberichten genereren over ingesloten batches. Als **[!UICONTROL Gedeeltelijke opname]** schakelt, wordt de verbeterde foutdiagnostiek automatisch afgedwongen.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL De]** drempelwaarde van de fout staat u toe om het percentage aanvaardbare fouten te plaatsen alvorens de volledige partij zal ontbreken. Deze waarde is standaard ingesteld op 5%.

## Volgende stappen {#next-steps}

Dit leerprogramma behandelde hoe te om een dataset tot stand te brengen of te wijzigen om gedeeltelijke partijingestie toe te laten. Lees de [Handleiding voor ontwikkelaars van batch-inname](./api-overview.md) voor meer informatie over batch-inname.

Lees voor meer informatie over het controleren van fouten bij gedeeltelijke inname de [Diagnostics guide](../quality/error-diagnostics.md).
