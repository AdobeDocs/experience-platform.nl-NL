---
keywords: Experience Platform;home;populaire onderwerpen;batch-opname;Batch-opname;partiële inname;Partiële inname;Fout ophalen;Fout ophalen;Onvolledige batch-opname;gedeeltelijke batch-opname;gedeeltelijke;Inslitie;Ingestie;
solution: Experience Platform
title: Overzicht van partiële batchverwerking
description: Dit document bevat een zelfstudie voor het beheren van gedeeltelijke batch-opname.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 0%

---

# Gedeeltelijke batch ingestie

Gedeeltelijke batch-opname is de mogelijkheid om gegevens met fouten in te voeren, tot een bepaalde drempel. Met deze functie kunnen gebruikers al hun juiste gegevens in Adobe Experience Platform opnemen terwijl al hun onjuiste gegevens afzonderlijk worden opgeslagen, samen met informatie over waarom de gegevens ongeldig zijn.

Dit document bevat een zelfstudie voor het beheren van gedeeltelijke batch-opname.

## Aan de slag

Deze zelfstudie vereist een praktische kennis van de verschillende Adobe Experience Platform-services die betrokken zijn bij gedeeltelijke batchopname. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [ Inname van de Partij ](./overview.md): De methode die [!DNL Platform] gegevens van gegevensdossiers, zoals CSV en Parquet opneemt en opslaat.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Platform] gegevens voor de klantervaring indeelt.

De volgende secties bevatten aanvullende informatie die u moet weten om aanroepen van [!DNL Platform] API&#39;s te kunnen uitvoeren.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Platform] APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in [!DNL Platform], zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).

## Een batch voor gedeeltelijke batch-opname inschakelen in de API {#enable-api}

>[!NOTE]
>
>In deze sectie wordt beschreven hoe u een batch voor gedeeltelijke batch-opname via de API inschakelt. Voor instructies bij het gebruiken van UI, te lezen gelieve [ een partij voor gedeeltelijke partijingestitie in de UI ](#enable-ui) stap toelaten.

U kunt een nieuwe partij tot stand brengen met gedeeltelijke toegelaten opname.

Om een nieuwe partij tot stand te brengen, volg de stappen in de [ handleiding van de partijontwikkelaar ](./api-overview.md). Wanneer u de stap **[!UICONTROL Create batch]** hebt bereikt, voegt u het volgende veld toe binnen de aanvraaginstantie:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `enableErrorDiagnostics` | Een markering waarmee [!DNL Platform] gedetailleerde foutberichten over de batch kan genereren. |
| `partialIngestionPercent` | Het percentage van aanvaardbare fouten vóór de volledige partij zal ontbreken. In dit voorbeeld kan maximaal 5% van de batch fouten zijn voordat deze mislukt. |


## Een batch voor gedeeltelijke batch-opname inschakelen in de gebruikersinterface {#enable-ui}

>[!NOTE]
>
>In deze sectie wordt beschreven hoe u een batch voor gedeeltelijke batchinvoer via de gebruikersinterface inschakelt. Als u al een batch hebt ingeschakeld voor gedeeltelijke batch-opname met behulp van de API, kunt u verdergaan met de volgende sectie.

Om een partij voor gedeeltelijke opname door [!DNL Platform] UI toe te laten, kunt u een nieuwe partij door bronverbindingen tot stand brengen, een nieuwe partij in een bestaande dataset tot stand brengen, of een nieuwe partij tot stand brengen door &quot; [!UICONTROL Map CSV to XDM flow]&quot;.

### Een nieuwe bronverbinding maken {#new-source}

Om een nieuwe bronverbinding tot stand te brengen, volg de vermelde stappen in het [ Bronoverzicht ](../../sources/home.md). Wanneer u de stap **[!UICONTROL Dataflow detail]** hebt bereikt, neemt u de velden **[!UICONTROL Partial ingestion]** en **[!UICONTROL Error diagnostics]** op.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

Met de schakeloptie **[!UICONTROL Partial ingestion]** kunt u het gebruik van gedeeltelijke batchopname in- of uitschakelen.

De schakeloptie **[!UICONTROL Error diagnostics]** wordt alleen weergegeven wanneer de schakeloptie **[!UICONTROL Partial ingestion]** is uitgeschakeld. Met deze functie kan [!DNL Platform] gedetailleerde foutberichten genereren over ingesloten batches. Als de schakeloptie **[!UICONTROL Partial ingestion]** is ingeschakeld, wordt de uitgebreide foutdiagnose automatisch afgedwongen.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Met **[!UICONTROL Error threshold]** kunt u het percentage acceptabele fouten instellen voordat de volledige batch mislukt. Deze waarde is standaard ingesteld op 5%.

### Een bestaande gegevensset gebruiken {#existing-dataset}

Om een bestaande dataset te gebruiken, begin door een dataset te selecteren. De zijbalk rechts vult informatie over de gegevensset.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

Met de schakeloptie **[!UICONTROL Partial ingestion]** kunt u het gebruik van gedeeltelijke batchopname in- of uitschakelen.

De schakeloptie **[!UICONTROL Error diagnostics]** wordt alleen weergegeven wanneer de schakeloptie **[!UICONTROL Partial ingestion]** is uitgeschakeld. Met deze functie kan [!DNL Platform] gedetailleerde foutberichten genereren over ingesloten batches. Als de schakeloptie **[!UICONTROL Partial ingestion]** is ingeschakeld, wordt de uitgebreide foutdiagnose automatisch afgedwongen.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Met **[!UICONTROL Error threshold]** kunt u het percentage acceptabele fouten instellen voordat de volledige batch mislukt. Deze waarde is standaard ingesteld op 5%.

Nu, kunt u gegevens uploaden gebruikend **gegevens** knoop toevoegen, en het zal worden opgenomen gebruikend gedeeltelijke opname.

### De &quot;[!UICONTROL Map CSV to XDM schema]&quot;-stroom gebruiken {#map-flow}

Om de &quot;[!UICONTROL Map CSV to XDM schema]&quot;stroom te gebruiken, volg de vermelde stappen in [ Kaart een CSV- dossierleerprogramma ](../tutorials/map-csv/overview.md). Wanneer u de stap **[!UICONTROL Add data]** hebt bereikt, neemt u de velden **[!UICONTROL Partial ingestion]** en **[!UICONTROL Error diagnostics]** op.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

Met de schakeloptie **[!UICONTROL Partial ingestion]** kunt u het gebruik van gedeeltelijke batchopname in- of uitschakelen.

De schakeloptie **[!UICONTROL Error diagnostics]** wordt alleen weergegeven wanneer de schakeloptie **[!UICONTROL Partial ingestion]** is uitgeschakeld. Met deze functie kan [!DNL Platform] gedetailleerde foutberichten genereren over ingesloten batches. Als de schakeloptie **[!UICONTROL Partial ingestion]** is ingeschakeld, wordt de uitgebreide foutdiagnose automatisch afgedwongen.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

In **[!UICONTROL Error threshold]** kunt u het percentage acceptabele fouten instellen voordat de volledige batch mislukt. Deze waarde is standaard ingesteld op 5%.

## Volgende stappen {#next-steps}

Dit leerprogramma behandelde hoe te om een dataset tot stand te brengen of te wijzigen om gedeeltelijke partijingestie toe te laten. Voor meer informatie over partijingestie, te lezen gelieve de [ gids van de partijontwikkelaar ](./api-overview.md).

Voor informatie bij het controleren van gedeeltelijke innamefouten, te lezen gelieve de [ gids van de de foutendiagnostiek van de partijingestie ](../quality/error-diagnostics.md).
