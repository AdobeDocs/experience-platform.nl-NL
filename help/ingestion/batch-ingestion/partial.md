---
keywords: Experience Platform;home;populaire onderwerpen;batch-opname;Batch-opname;partiële inname;Partiële inname;Fout ophalen;Fout ophalen;Onvolledige batch-opname;gedeeltelijke batch-opname;gedeeltelijke;Inslitie;Ingestie;
solution: Experience Platform
title: Overzicht van partiële batchverwerking
topic-legacy: overview
description: Dit document bevat een zelfstudie voor het beheren van gedeeltelijke batch-opname.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: 636d6dcbe8eb73b7898fc3794f6b4567956e5618
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# Gedeeltelijke batch ingestie

Gedeeltelijke batch-opname is de mogelijkheid om gegevens met fouten in te voeren, tot een bepaalde drempel. Met deze functie kunnen gebruikers al hun juiste gegevens in Adobe Experience Platform opnemen terwijl al hun onjuiste gegevens afzonderlijk worden opgeslagen, samen met informatie over waarom de gegevens ongeldig zijn.

Dit document bevat een zelfstudie voor het beheren van gedeeltelijke batch-opname.

## Aan de slag

Deze zelfstudie vereist een praktische kennis van de verschillende Adobe Experience Platform-services die betrokken zijn bij gedeeltelijke batchopname. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [Inname in batch](./overview.md): De methode die [!DNL Platform] Hiermee worden gegevens uit gegevensbestanden, zoals CSV en Parquet, ingepakt en opgeslagen.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Platform] organiseert de gegevens van de klantenervaring.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan te maken [!DNL Platform] API&#39;s.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

### Waarden verzamelen voor vereiste koppen

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

## Een batch voor gedeeltelijke batch-opname inschakelen in de API {#enable-api}

>[!NOTE]
>
>In deze sectie wordt beschreven hoe u een batch voor gedeeltelijke batch-opname via de API inschakelt. Voor instructies over het gebruik van de interface leest u de [een batch inschakelen voor gedeeltelijke batchinvoer in de gebruikersinterface](#enable-ui) stap.

U kunt een nieuwe partij tot stand brengen met gedeeltelijke toegelaten opname.

Voer de stappen in het dialoogvenster [handleiding voor het ontwikkelen van batch-inhoud](./api-overview.md). Wanneer u de **[!UICONTROL Create batch]** Voeg in de stap het volgende veld toe in de aanvraaginstantie:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `enableErrorDiagnostics` | Een markering die [!DNL Platform] om gedetailleerde foutberichten over uw batch te genereren. |
| `partialIngestionPercent` | Het percentage van aanvaardbare fouten vóór de volledige partij zal ontbreken. In dit voorbeeld kan maximaal 5% van de batch fouten zijn voordat deze mislukt. |


## Een batch voor gedeeltelijke batch-opname inschakelen in de gebruikersinterface {#enable-ui}

>[!NOTE]
>
>In deze sectie wordt beschreven hoe u een batch voor gedeeltelijke batchinvoer via de gebruikersinterface inschakelt. Als u al een batch voor gedeeltelijke batch-opname hebt ingeschakeld met de API, kunt u verdergaan met de volgende sectie.

Om een partij voor gedeeltelijke inname door te laten [!DNL Platform] UI, kunt u een nieuwe partij door bronverbindingen tot stand brengen, een nieuwe partij in een bestaande dataset tot stand brengen of een nieuwe partij tot stand brengen door &quot;[!UICONTROL Map CSV to XDM flow]&quot;.

### Een nieuwe bronverbinding maken {#new-source}

Als u een nieuwe bronverbinding wilt maken, voert u de volgende stappen uit in het dialoogvenster [Overzicht van bronnen](../../sources/home.md). Wanneer u de **[!UICONTROL Dataflow detail]** neem nota van de **[!UICONTROL Partial ingestion]** en **[!UICONTROL Error diagnostics]** velden.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

De **[!UICONTROL Partial ingestion]** met deze optie kunt u het gebruik van gedeeltelijke batchopname in- of uitschakelen.

De **[!UICONTROL Error diagnostics]** wordt alleen weergegeven wanneer de **[!UICONTROL Partial ingestion]** schakeloptie uit. Met deze functie is [!DNL Platform] om gedetailleerde foutberichten te genereren over de batches die u hebt ingevoerd. Als de **[!UICONTROL Partial ingestion]** Schakel deze optie in, uitgebreide foutdiagnostiek wordt automatisch afgedwongen.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

De **[!UICONTROL Error threshold]** Hiermee kunt u het percentage acceptabele fouten instellen voordat de gehele batch mislukt. Deze waarde is standaard ingesteld op 5%.

### Een bestaande gegevensset gebruiken {#existing-dataset}

Om een bestaande dataset te gebruiken, begin door een dataset te selecteren. De zijbalk rechts vult informatie over de gegevensset.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

De **[!UICONTROL Partial ingestion]** met deze optie kunt u het gebruik van gedeeltelijke batchopname in- of uitschakelen.

De **[!UICONTROL Error diagnostics]** wordt alleen weergegeven wanneer de **[!UICONTROL Partial ingestion]** schakeloptie uit. Met deze functie is [!DNL Platform] om gedetailleerde foutberichten te genereren over de batches die u hebt ingevoerd. Als de **[!UICONTROL Partial ingestion]** Schakel deze optie in, uitgebreide foutdiagnostiek wordt automatisch afgedwongen.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

De **[!UICONTROL Error threshold]** Hiermee kunt u het percentage acceptabele fouten instellen voordat de gehele batch mislukt. Deze waarde is standaard ingesteld op 5%.

U kunt nu gegevens uploaden met de **Gegevens toevoegen** en wordt het gedeeltelijk ingeslikt.

### Gebruik de &quot;[!UICONTROL Map CSV to XDM schema]&quot;&quot;flow {#map-flow}

Als u &quot;[!UICONTROL Map CSV to XDM schema]&quot;, voert u de vermelde stappen uit in de [Zelfstudie Een CSV-bestand toewijzen](../tutorials/map-a-csv-file.md). Wanneer u de **[!UICONTROL Add data]** neem nota van de **[!UICONTROL Partial ingestion]** en **[!UICONTROL Error diagnostics]** velden.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

De **[!UICONTROL Partial ingestion]** met deze optie kunt u het gebruik van gedeeltelijke batchopname in- of uitschakelen.

De **[!UICONTROL Error diagnostics]** wordt alleen weergegeven wanneer de **[!UICONTROL Partial ingestion]** schakeloptie uit. Met deze functie is [!DNL Platform] om gedetailleerde foutberichten te genereren over de batches die u hebt ingevoerd. Als de **[!UICONTROL Partial ingestion]** Schakel deze optie in, uitgebreide foutdiagnostiek wordt automatisch afgedwongen.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]** Hiermee kunt u het percentage acceptabele fouten instellen voordat de gehele batch mislukt. Deze waarde is standaard ingesteld op 5%.

## Volgende stappen {#next-steps}

Dit leerprogramma behandelde hoe te om een dataset tot stand te brengen of te wijzigen om gedeeltelijke partijingestie toe te laten. Lees voor meer informatie over het gebruik van batch [handleiding voor het ontwikkelen van batch-inhoud](./api-overview.md).

Voor informatie over het controleren van fouten bij gedeeltelijke inname, lees de [diagnostische handleiding voor foutmeldingen bij batch](../quality/error-diagnostics.md).
