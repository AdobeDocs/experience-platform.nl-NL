---
keywords: Experience Platform;thuis;populaire onderwerpen;monitorrekeningen;monitordataflows;dataflows
description: De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het controleren van streaminggegevens vanuit de werkruimte Bronnen.
title: Dataflows controleren op streamingbronnen in de gebruikersinterface
exl-id: b080e398-e71f-40bd-aea1-7ea3ce86b55d
source-git-commit: 647f2780798dcf55a68e156af3318924c352a442
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Dataflows controleren op streamingbronnen in de gebruikersinterface

In deze zelfstudie worden de stappen beschreven voor het controleren van gegevensstromen voor streamingbronnen met behulp van de [!UICONTROL Sources] werkruimte.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Gegevensstromen](../../../dataflows/home.md): Dataflows zijn een voorstelling van gegevenstaken die gegevens over het Platform verplaatsen. Dataflows worden gevormd over verschillende diensten, die gegevens van bronschakelaars aan doeldatasets helpen bewegen, aan [!DNL Identity] en [!DNL Profile]en [!DNL Destinations].
   * [Dataflow-uitvoering](../../notifications.md): De looppas van Dataflow is de terugkomende geplande banen die op de frequentieconfiguratie van geselecteerde dataflows worden gebaseerd.
* [Bronnen](../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Dataflows controleren voor streamingbronnen

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

Selecteer **[!UICONTROL Dataflows]** in de bovenste koptekst.

![catalogus](../../images/tutorials/monitor-streaming/catalog.png)

De [!UICONTROL Dataflows] Deze pagina bevat een lijst met alle bestaande gegevensstromen in uw organisatie, inclusief informatie over de brongegevens, de accountnaam en de uitvoerstatus van de gegevensstroom.

Selecteer de naam van de gegevensstroom u wilt bekijken.

![dataflows](../../images/tutorials/monitor-streaming/dataflows.png)

De volgende lijst bevat meer informatie over dataflow looppas statussen:

| Status | Beschrijving |
| ------ | ----------- |
| Voltooid | De `Completed` status wijst erop dat alle verslagen voor de overeenkomstige dataflow looppas binnen de periode van één uur werden verwerkt. A `Completed` status kan nog steeds fouten bevatten in dataflow-uitvoering. |
| Succes | De `Success` status wijst erop dat alle verslagen voor de overeenkomstige dataflow looppas binnen de periode van één uur werden verwerkt en dat er geen fouten tijdens de dataflow looppas werden ontmoet. |
| Verwerking | De `Processing` status geeft aan dat een gegevensstroom nog niet actief is. Deze status wordt vaak direct na het maken van een nieuwe gegevensstroom aangetroffen. |
| Fout | De `Error` status geeft aan dat het activeringsproces van een gegevensstroom is onderbroken. |
| Geen uitvoering | De `No runs` status geeft aan dat de gegevensstroom is gemaakt, maar dat er geen dataflow-run is gestart. |

De [!UICONTROL Dataflow Activity] Deze pagina bevat specifieke informatie over uw streaminggegevensstroom. De bovenste banner bevat het cumulatieve aantal records dat wordt opgenomen en records die zijn mislukt voor al uw streaming dataflow-uitvoering in het geselecteerde datumbereik.

![dataflow-activity](../../images/tutorials/monitor-streaming/dataflow-activity.png)

Standaard bevatten de weergegeven gegevens de innamesnelheden van de laatste zeven dagen. Selecteren **[!UICONTROL Last 7 days]** om het tijdkader van getoonde verslagen aan te passen.

Er wordt een kalenderpop-upvenster weergegeven met opties voor alternatieve ingstijd. U kunt het dataflow runtime kader vormen om stroomlooplooppas van de vorige zeven dagen of de laatste 30 dagen te bekijken. U kunt ook de interactieve kalender configureren om een aangepast tijdframe van uw keuze in te stellen. Als u klaar bent, selecteert u **[!UICONTROL Apply]**.

![kalender](../../images/tutorials/monitor-streaming/calendar.png)

In de onderste helft van de pagina wordt informatie weergegeven over het aantal records dat per flowuitvoering is ontvangen, opgenomen en mislukt. Elke stroomrun wordt opgenomen binnen een uurvenster.

![dataflow-run](../../images/tutorials/monitor-streaming/dataflow-run.png)

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
>abstract="De Verslagen met Waarschuwingen wijst op het totale aantal verslagen die met mapperomzettingswaarschuwingen worden opgenomen. Alle maptransformatiefouten worden gerapporteerd als waarschuwingen en rijen die gedeeltelijk worden ingesloten, worden als geslaagd beschouwd met een waarschuwing"
>text="Learn more in documentation"

Elke individuele dataflow run toont de volgende details:

* **[!UICONTROL Dataflow run start]**: De tijd dat dataflow begon bij.
* **[!UICONTROL Processing time]**: De hoeveelheid tijd die het voor dataflow aan proces nam.
* **[!UICONTROL Records Received]**: Het totale aantal verslagen die in dataflow van een bronschakelaar worden ontvangen.
* **[!UICONTROL Records Ingested]**: Het totale aantal records dat wordt ingevoerd in [!DNL Data Lake].
* **[!UICONTROL Records with Warnings]**: Het totale aantal records met waarschuwingen die zijn opgenomen. Alle maptransformatiefouten worden gerapporteerd als waarschuwingen en rijen die gedeeltelijk worden ingepakt, worden als `success` met een waarschuwing. **Opmerking**: Ondersteuning voor het opnemen van records met waarschuwingen is alleen beschikbaar voor streamingbronnen.
* **[!UICONTROL Records Failed]**: Het aantal records waarin geen records zijn opgenomen [!DNL Data Lake] als gevolg van fouten in de gegevens.
* **[!UICONTROL Ingestion Rate]**: Het succespercentage records die worden opgenomen in [!DNL Data Lake]. Deze maatstaf is van toepassing wanneer [!UICONTROL Partial Ingestion] is ingeschakeld.
* **[!UICONTROL Status]**: Vertegenwoordigt de staat de dataflow is in: ofwel [!UICONTROL Completed] of [!UICONTROL Processing]. [!UICONTROL Completed] betekent dat alle verslagen voor de overeenkomstige dataflow looppas binnen de periode van één uur werden verwerkt. [!UICONTROL Processing] betekent dat de dataflow run nog niet is voltooid.

De [!UICONTROL Dataflow run overview] De pagina bevat extra informatie over uw dataflow, zoals zijn overeenkomstige dataflow looppas identiteitskaart, doeldataset, en organisatieidentiteitskaart

Een stroom die met fouten wordt uitgevoerd bevat ook [!UICONTROL Dataflow run errors] , waarin de specifieke fout wordt weergegeven die tot de fout van de uitvoering heeft geleid, en het totale aantal records dat is mislukt.

![data-run-overview](../../images/tutorials/monitor-streaming/dataflow-run-overview.png)

### Records met waarschuwingen weergeven {#warnings}

[!UICONTROL Records with warnings] geeft een lijst weer met maptransformatiewaarschuwingen die zijn opgetreden tijdens de uitvoering van de stroom. Rijen die gedeeltelijk worden ingesloten, worden als geslaagd beschouwd en worden met waarschuwingen toegevoegd als er fouten in de maptransformatie worden gevonden.

Standaard worden alle maptransformatiefouten beschouwd als waarschuwingen, behalve als ze een van de volgende zijn:

* Syntaxisfouten
* Verwijzingen naar kenmerken die niet bestaan
* Niet-overeenkomende XDM-gegevenstypen

Selecteer **[!UICONTROL Preview error diagnostics]**.

![records-met-waarschuwingen](../../images/tutorials/monitor-streaming/records-with-warnings.png)

De [!UICONTROL Error diagnostics preview] kunt u een voorvertoning weergeven van maximaal 100 fouten en/of waarschuwingen met betrekking tot uw gegevensstroom. Van hier, kunt u ook het de mislukkingsmanifest van de inname voor meer informatie downloaden, gebruikend [!DNL Data Access] API.

![diagnostiek](../../images/tutorials/monitor-streaming/diagnostics.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de opdracht [!UICONTROL Sources] werkruimte om de streaminggegevens te controleren en de fouten te identificeren die tot mislukte gegevensstromen hebben geleid. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van bronnen](../../home.md)
* [Overzicht van gegevensstromen](../../../dataflows/home.md)
