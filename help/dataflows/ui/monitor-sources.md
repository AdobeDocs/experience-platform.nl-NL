---
keywords: Experience Platform;thuis;populaire onderwerpen;monitorrekeningen;monitordataflows;dataflows;bronnen
description: De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Dit leerprogramma verstrekt stappen voor het bekijken van bestaande gegevensstromen van de werkruimte van Bronnen.
solution: Experience Platform
title: De Dataflows van de monitor voor Bronnen in UI
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: f8186e467dc982003c6feb01886ed16d23572955
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---


# Dataflows controleren voor bronnen in de gebruikersinterface

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het weergeven van bestaande gegevensstromen uit de werkruimte [!UICONTROL Bronnen].

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [Bronnen](../../sources/home.md):  [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de  [!DNL Platform] diensten.
- [Sandboxen](../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Dataflows bewaken

Meld u aan bij [Experience Platform UI](https://platform.adobe.com) en selecteer **[!UICONTROL Bronnen]** in de linkernavigatie om de [!UICONTROL Bronnen] werkruimte te openen. Selecteer **[!UICONTROL Gegevensstromen]** van de hoogste kopbal om bestaande gegevensstromen te bekijken.

![catalogusgegevensstromen](../assets/ui/monitor-sources/catalog-dataflows.png)

Er wordt een lijst met bestaande gegevensstromen weergegeven. Op deze pagina vindt u een lijst met zichtbare gegevensstromen, waaronder informatie over de bron, gebruikersnaam, het aantal gegevensstromen en de status.

Zie de volgende tabel voor meer informatie over statussen:

| Status | Beschrijving |
| ------ | ----------- |
| Ingeschakeld | De status `Enabled` wijst erop dat een dataflow actief is en gegevens volgens het programma opneemt het werd verstrekt. |
| Uitgeschakeld | De status `Disabled` geeft aan dat een gegevensstroom inactief is en geen gegevens opneemt. |
| Verwerking | De status `Processing` geeft aan dat een gegevensstroom nog niet actief is. Deze status wordt vaak direct na het maken van een nieuwe gegevensstroom aangetroffen. |
| Fout | De status `Error` geeft aan dat het activeringsproces van een gegevensstroom is onderbroken. |

Selecteer het trechter-pictogram linksboven om te sorteren.

![dataflows-list](../assets/ui/monitor-sources/dataflows-list.png)

Het sorteervenster wordt weergegeven. Selecteer de bron die u wilt openen in het schuifmenu en selecteer de gegevensstroom in de lijst aan de rechterkant. U kunt ook de ellipsen (`...`) knoop selecteren om meer beschikbare opties voor uw geselecteerde gegevensstroom te verhogen.

![sortDataFlow](../assets/ui/monitor-sources/dataflows-sort.png)

De **[!UICONTROL Dataflow activity]** pagina bevat details over het aantal records dat wordt opgenomen en records die zijn mislukt, en informatie over de status en verwerkingstijd van de gegevensstroom. Selecteer het kalenderpictogram boven de gegevensstroom om het tijdkader van uw innameregisters aan te passen.

![datflow-activity](../assets/ui/monitor-sources/dataflow-activity.png)

Met de kalender kunt u de verschillende tijdframes voor opgenomen records bekijken. U kunt kiezen om een van de twee vooraf ingestelde opties &quot;[!UICONTROL Last 7 days]&quot; of &quot;[!UICONTROL Last 30 days]&quot; te selecteren. U kunt ook een aangepast tijdframe instellen met de kalender. Selecteer uw tijdkader van keus en selecteer **[!UICONTROL Apply]** om verder te gaan.

![stroomkalender](../assets/ui/monitor-sources/flow-calendar.png)

Standaard wordt met de **[!UICONTROL Dataflow-activiteit]** het deelvenster **[!UICONTROL Eigenschappen]** weergegeven dat is gekoppeld aan de dataflow. Selecteer de doorloop die in de lijst wordt uitgevoerd om de bijbehorende metagegevens weer te geven, inclusief informatie over de unieke uitvoerings-id.

Selecteer **[!UICONTROL Start Dataflow-run]** om het **[!UICONTROL Overzicht Dataflow-run te openen]**.

![run](../assets/ui/monitor-sources/run-metadata.png)

**[!UICONTROL Overzicht Dataflow run]** toont informatie over de dataflow met inbegrip van zijn meta-gegevens, gedeeltelijk ingeslipstatus, en toegewezen foutendrempel. De bovenste koptekst bevat ook een foutoverzicht. Het **[!UICONTROL foutenoverzicht]** bevat de specifieke fout op hoofdniveau die toont bij welke stap het innameproces een fout tegenkwam.

![data-run-overview](../assets/ui/monitor-sources/dataflow-run-overview.png)

Verwijs naar de volgende lijst voor fouten die in **[!UICONTROL Overzicht van de Fout]** kunnen worden gezien.

| Fout | Beschrijving |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Er is een fout opgetreden tijdens het kopiëren van gegevens uit een bron. |
| `CONNECTOR-2001-500` | Er is een fout opgetreden tijdens het verwerken van gekopieerde gegevens naar [!DNL Platform]. Deze fout kan betrekking hebben op parseren, valideren of transformeren. |

De onderste helft van het scherm bevat informatie over **[!UICONTROL Dataflow-uitvoerfouten]**. Van hier kunt u ook de opgenomen bestanden weergeven, een voorbeeld bekijken en fouten downloaden of het bestandmanifest downloaden.

In de sectie **[!UICONTROL Fouten bij uitvoering van gegevensstroom]** worden de foutcode, het aantal mislukte records en informatie over de fout weergegeven.

Selecteer **[!UICONTROL Voorvertoning van foutdiagnostiek]** om meer informatie over de innamefout weer te geven.

![Dataflow-run-fouten](../assets/ui/monitor-sources/dataflow-run-errors.png)

Het venster **[!UICONTROL Foutdiagnostische voorvertoning]** wordt weergegeven. In dit scherm wordt specifieke informatie weergegeven over de fout bij het opnemen, zoals de bestandsnaam, foutcode, de naam van de kolom waarin de fout is opgetreden en een beschrijving van de fout.

Deze sectie bevat ook een voorvertoning van de kolom die de fout bevat.

>[!IMPORTANT]
>
>Als u **[!UICONTROL Voorvertoning van foutdiagnostiek]** wilt inschakelen, moet u **[!UICONTROL Gedeeltelijke opname]** en **[!UICONTROL Foutdiagnostiek]** activeren bij het configureren van een gegevensstroom. Als u dit doet, kan het systeem alle records scannen die tijdens de flowuitvoering worden ingevoerd.

![Voorvertoning-fout-diagnostiek](../assets/ui/monitor-sources/preview-error-diagnostics.png)

Nadat u een voorvertoning van de fouten hebt weergegeven, kunt u **[!UICONTROL Download]** selecteren in het venster **[!UICONTROL DataFlow-run overzicht]** om volledige foutdiagnostiek te openen en de bestandmanifest te downloaden. Zie de documenten op [error diagnostics](../../ingestion/batch-ingestion/partial.md#retrieve-errors) en [downloading metadata](../../ingestion/batch-ingestion/partial.md#download-metadata) voor meer informatie.

![Voorvertoning-fout-diagnostiek](../assets/ui/monitor-sources/download.png)

Raadpleeg de zelfstudie over het [controleren van streaminggegevens](../../ingestion/quality/monitor-data-ingestion.md) voor meer informatie over het controleren van gegevensstromen en het opnemen van gegevens.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes bestaande rekeningen en gegevensstromen van **[!UICONTROL Bronnen]** werkruimte betreden. Binnenkomende gegevens kunnen nu worden gebruikt door downstreamservices [!DNL Platform] zoals [!DNL Real-time Customer Profile] en [!DNL Data Science Workspace]. Raadpleeg de volgende documenten voor meer informatie:

- [Overzicht van het realtime klantprofiel](../../profile/home.md)
- [Overzicht van de Data Science Workspace](../../data-science-workspace/home.md)
