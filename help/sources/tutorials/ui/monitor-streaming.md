---
keywords: Experience Platform;home;populaire onderwerpen;monitoraccounts;monitoren, gegevensstroom;gegevensstroom
description: Source-connectors in Adobe Experience Platform bieden de mogelijkheid om volgens een schema extern gesourceerde gegevens in te voeren. Deze zelfstudie bevat stappen voor het controleren van streaminggegevens vanuit de werkruimte Bronnen.
title: Dataflows controleren op streamingbronnen in de gebruikersinterface
exl-id: b080e398-e71f-40bd-aea1-7ea3ce86b55d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 0%

---

# Dataflows controleren op streamingbronnen in de gebruikersinterface

In deze zelfstudie worden de stappen beschreven voor het controleren van gegevensstromen voor streamingbronnen met de werkruimte van [!UICONTROL Sources] .

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [&#x200B; Dataflows &#x200B;](../../../dataflows/home.md): Dataflows zijn een vertegenwoordiging van gegevensbanen die gegevens over Experience Platform bewegen. Dataflows worden geconfigureerd op verschillende services, waardoor gegevens van bronconnectors naar doelgegevenssets worden verplaatst, naar [!DNL Identity] en [!DNL Profile] en naar [!DNL Destinations] .
   * [&#x200B; looppas Dataflow &#x200B;](../../notifications.md): De looppas van Dataflow is de terugkomende geplande banen die op de frequentieconfiguratie van geselecteerde dataflows worden gebaseerd.
* [&#x200B; Bronnen &#x200B;](../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [&#x200B; Sandboxes &#x200B;](../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

## Dataflows controleren voor streamingbronnen

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatiebalk voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

Als u bestaande gegevensstromen voor streamingbronnen wilt weergeven, selecteert u **[!UICONTROL Dataflows]** in de bovenste koptekst.

![&#x200B; catalogus &#x200B;](../../images/tutorials/monitor-streaming/catalog.png)

De pagina [!UICONTROL Dataflows] bevat een lijst met alle bestaande gegevensstromen in uw organisatie, inclusief informatie over hun brongegevens, accountnaam en status van de gegevensstroom.

Selecteer de naam van de gegevensstroom u wilt bekijken.

![&#x200B; dataflows &#x200B;](../../images/tutorials/monitor-streaming/dataflows.png)

De volgende lijst bevat meer informatie over dataflow looppas statussen:

| Status | Beschrijving |
| ------ | ----------- |
| Voltooid | De `Completed` status wijst erop dat alle verslagen voor de overeenkomstige dataflow looppas binnen de periode van één uur werden verwerkt. Een `Completed` -status kan nog steeds fouten bevatten in gegevensstroomuitvoering. |
| Succes | De `Success` status wijst erop dat alle verslagen voor de overeenkomstige dataflow looppas binnen de periode van één uur werden verwerkt en dat er geen fouten tijdens de dataflow looppas werden ontmoet. |
| Verwerking | De status `Processing` geeft aan dat een gegevensstroom nog niet actief is. Deze status wordt vaak direct na het maken van een nieuwe gegevensstroom aangetroffen. |
| Fout | De `Error` -status geeft aan dat het activeringsproces van een gegevensstroom is onderbroken. |
| Geen uitvoering | De status `No runs` geeft aan dat de gegevensstroom is gemaakt, maar dat er geen gegevensstroomuitvoering is gestart. |

Op de pagina [!UICONTROL Dataflow Activity] wordt specifieke informatie over uw streaminggegevensstroom weergegeven. De bovenste banner bevat het cumulatieve aantal records dat wordt opgenomen en records die zijn mislukt voor al uw streaming dataflow-uitvoering in het geselecteerde datumbereik.

![&#x200B; dataflow-activity &#x200B;](../../images/tutorials/monitor-streaming/dataflow-activity.png)

Standaard bevatten de weergegeven gegevens de innamesnelheden van de laatste zeven dagen. Selecteer **[!UICONTROL Last 7 days]** om het tijdkader van getoonde verslagen aan te passen.

Er wordt een kalenderpop-upvenster weergegeven met opties voor alternatieve ingstijd. U kunt het dataflow runtime kader vormen om stroomlooplooppas van de vorige zeven dagen of de laatste 30 dagen te bekijken. U kunt ook de interactieve kalender configureren om een aangepast tijdframe van uw keuze in te stellen. Selecteer **[!UICONTROL Apply]** als u klaar bent.

![&#x200B; kalender &#x200B;](../../images/tutorials/monitor-streaming/calendar.png)

In de onderste helft van de pagina wordt informatie weergegeven over het aantal records dat per flowuitvoering is ontvangen, opgenomen en mislukt. Elke stroomrun wordt opgenomen binnen een uurvenster.

![&#x200B; dataflow-run &#x200B;](../../images/tutorials/monitor-streaming/dataflow-run.png)

### Metrische gegevens voor gegevensstroomuitvoering {#dataflow-run-metrics}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_received"
>title="Ontvangen records"
>abstract="De Ontvangen metrische Verslagen wijzen op het totale aantal verslagen die in dataflow worden ontvangen."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_ingested"
>title="Opgenomen records"
>abstract="De Verslagen Geëist metrisch wijst op de totale telling van verslagen die in het gegevensmeer worden opgenomen."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_failed"
>title="Records mislukt"
>abstract="De Verslagen Mislukte metrisch wijst op de totale telling van verslagen die niet aan het gegevensmeer wegens fouten in de gegevens werden opgenomen."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_warnings"
>title="Records met waarschuwingen"
>abstract="De Verslagen met Waarschuwingen wijst op het totale aantal verslagen die met mapperomzettingswaarschuwingen worden opgenomen. Alle maptransformatiefouten worden gerapporteerd als waarschuwingen en rijen die gedeeltelijk worden ingeslikt, worden als geslaagd beschouwd met een waarschuwing"
>text="Learn more in documentation"

Elke individuele dataflow run toont de volgende details:

* **[!UICONTROL Dataflow run start]**: De tijd waarop de gegevensstroom is gestart.
* **[!UICONTROL Processing time]**: De hoeveelheid tijd die nodig was voor het verwerken van de gegevensstroom.
* **[!UICONTROL Records Received]**: Het totale aantal verslagen die in dataflow van een bronschakelaar worden ontvangen.
* **[!UICONTROL Records Ingested]**: Het totale aantal records dat in [!DNL Data Lake] wordt ingevoerd.
* **[!UICONTROL Records with Warnings]**: Het totale aantal records met waarschuwingen die zijn ingevoerd. Alle maptransformatiefouten worden gerapporteerd als waarschuwingen en rijen die gedeeltelijk worden ingeslikt, worden gelabeld als `success` met een waarschuwing. **Nota**: Steun voor het opnemen van verslagen met waarschuwingen is slechts beschikbaar aan het stromen bronnen.
* **[!UICONTROL Records Failed]**: Het aantal records dat niet in [!DNL Data Lake] is opgenomen als gevolg van fouten in de gegevens.
* **[!UICONTROL Ingestion Rate]**: De successnelheid van records die in [!DNL Data Lake] worden ingevoerd. Deze metrische waarde is van toepassing wanneer [!UICONTROL Partial Ingestion] is ingeschakeld.
* **[!UICONTROL Status]**: geeft de status aan waarin de gegevensstroom zich bevindt: [!UICONTROL Completed] of [!UICONTROL Processing] . [!UICONTROL Completed] betekent dat alle records voor de bijbehorende dataflow-run binnen een uur zijn verwerkt. [!UICONTROL Processing] betekent dat de uitvoering van de gegevensstroom nog niet is voltooid.

De [!UICONTROL Dataflow run overview] pagina bevat extra informatie over uw gegevensstroom, zoals zijn overeenkomstige dataflow looppas identiteitskaart, doeldataset, en organisatieidentiteitskaart

Een stroom met fouten bevat ook het deelvenster [!UICONTROL Dataflow run errors] , waarin de specifieke fout wordt weergegeven die tot het mislukken van de uitvoering heeft geleid, en het totale aantal records dat is mislukt.

![&#x200B; dataflow-run-overview &#x200B;](../../images/tutorials/monitor-streaming/dataflow-run-overview.png)

### Records met waarschuwingen weergeven {#warnings}

In [!UICONTROL Records with warnings] wordt een lijst weergegeven met waarschuwingen voor maptransformatie die zijn opgetreden tijdens de uitvoering van de stroom. Rijen die gedeeltelijk worden ingesloten, worden als geslaagd beschouwd en worden met waarschuwingen toegevoegd als er fouten in de maptransformatie worden gevonden.

Standaard worden alle maptransformatiefouten beschouwd als waarschuwingen, behalve als ze een van de volgende zijn:

* Syntaxisfouten
* Verwijzingen naar kenmerken die niet bestaan
* Niet-overeenkomende XDM-gegevenstypen

Selecteer **[!UICONTROL Preview error diagnostics]** om foutdiagnostiek weer te geven.

![&#x200B; verslagen-met-waarschuwingen &#x200B;](../../images/tutorials/monitor-streaming/records-with-warnings.png)

In het venster [!UICONTROL Error diagnostics preview] kunt u maximaal 100 fouten en/of waarschuwingen met betrekking tot uw gegevensstroom voorvertonen. Vanaf hier kunt u het foutmanifest voor inname ook downloaden voor meer informatie met de API [!DNL Data Access] .

![&#x200B; diagnostiek &#x200B;](../../images/tutorials/monitor-streaming/diagnostics.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u de werkruimte van [!UICONTROL Sources] gebruikt om de streaminggegevens te controleren en de fouten te identificeren die tot mislukte gegevensstromen hebben geleid. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van bronnen](../../home.md)
* [Overzicht van gegevensstromen](../../../dataflows/home.md)
