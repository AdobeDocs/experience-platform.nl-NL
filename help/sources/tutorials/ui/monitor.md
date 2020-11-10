---
keywords: Experience Platform;home;popular topics;monitor accounts;monitor dataflows;data flows
description: De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Dit leerprogramma verstrekt stappen voor het bekijken van bestaande rekeningen en dataflows van de Bronwerkruimte.
solution: Experience Platform
title: Accounts en gegevensstromen bewaken
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 0%

---


# De rekeningen en de gegevensstromen van de monitor in UI

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Dit leerprogramma verstrekt stappen voor het bekijken van bestaande rekeningen en gegevensstromen van de [!UICONTROL werkruimte van Bronnen] .

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   - [Basisbeginselen van de schemacompositie](../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

## Accounts controleren

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Bronnen]** in de linkernavigatiebalk voor toegang tot de werkruimte **[!UICONTROL Bronnen]** . In het scherm **[!UICONTROL Catalogus]** worden diverse bronnen weergegeven waarvoor u accounts en gegevensstromen kunt maken. Elke bron toont het aantal bestaande rekeningen en gegevensstromen verbonden aan hen.

Selecteer **[!UICONTROL Accounts]** in de bovenste koptekst om bestaande accounts weer te geven.

![catalogus](../../images/tutorials/monitor/catalog-accounts.png)

De pagina&#39;s **[!UICONTROL Accounts]** worden weergegeven. Op deze pagina vindt u een lijst met weer te geven accounts, waaronder informatie over de bron, gebruikersnaam, het aantal gegevensstromen en de aanmaakdatum.

Selecteer het trechter-pictogram linksboven om het sorteervenster te openen.

![rekeningen](../../images/tutorials/monitor/accounts-list.png)

Via het sorteervenster hebt u toegang tot accounts vanuit een specifieke bron. Selecteer de bron waarmee u wilt werken en selecteer het account in de lijst aan de rechterkant.

>[!TIP]
>
> Gebruik de ![spectrum-controle](../../images/tutorials/monitor/spectrum-control.png) knoop in de kolom van de **[!UICONTROL Naam]** om een nieuwe brondataflow voor de geselecteerde rekening tot stand te brengen.

![accounts selecteren](../../images/tutorials/monitor/accounts-sort.png)

Daarnaast kunt u bestaande accountgegevens bewerken en uw accountgegevens bijwerken. Selecteer het potloodpictogram voor de accountgegevens die u wilt bewerken.

![](../../images/tutorials/monitor/click-edit.png)

Het modaal **[!UICONTROL dialoogvenster Accountdetails]** bewerken wordt weergegeven. Vanaf deze pagina kunt u uw bestaande accountgegevens en verificatiereferenties bijwerken.

>[!NOTE]
>
> Het uitgeven van rekeningsdetails is beschikbaar op alle partijbronschakelaars.

![](../../images/tutorials/monitor/edit-account.png)

Van de pagina van **[!UICONTROL Rekeningen]** , kunt u een lijst van bestaande gegevensstromen of doeldatasets bekijken verbonden aan de rekening u toegang had tot. Selecteer de ellipsen (`...`) knoop om meer beschikbare opties voor uw geselecteerde gegevensstroom te verhogen. Deze opties worden hieronder nader beschreven:

| Control | Beschrijving |
| ------- | ----------- |
| [!UICONTROL Tijdschema bewerken] | Staat u toe om het innameschema van dataflow uit te geven. |
| [!UICONTROL Gegevensstroom uitschakelen] | Hiermee kunt u gegevensinvoer uitschakelen voor de geselecteerde gegevensstroom. |
| [!UICONTROL Verwijderen] | Hiermee kunt u de geselecteerde gegevensstroom verwijderen. |

![dataflows](../../images/tutorials/monitor/dataflows.png)

## Dataflows bewaken

Dataflows zijn rechtstreeks vanuit de **[!UICONTROL Cataloguspagina]** toegankelijk zonder **[!UICONTROL accounts]** weer te geven. Selecteer **[!UICONTROL Gegevensstromen]** van de hoogste kopbal om een lijst van gegevensstromen te bekijken.

![catalogusgegevensstromen](../../images/tutorials/monitor/catalog-dataflows.png)

Er wordt een lijst met bestaande gegevensstromen weergegeven. Op deze pagina vindt u een lijst met zichtbare gegevensstromen, waaronder informatie over de bron, gebruikersnaam, het aantal gegevensstromen en de status.

Zie de volgende tabel voor meer informatie over statussen:

| Status | Beschrijving |
| ------ | ----------- |
| Ingeschakeld | De `Enabled` status wijst erop dat een dataflow actief is en gegevens volgens het programma opneemt het werd verstrekt. |
| Uitgeschakeld | De `Disabled` status geeft aan dat een gegevensstroom inactief is en geen gegevens opneemt. |
| Verwerking | De `Processing` status geeft aan dat een gegevensstroom nog niet actief is. Deze status wordt vaak direct na het maken van een nieuwe gegevensstroom aangetroffen. |
| Fout | De `Error` status geeft aan dat het activeringsproces van een gegevensstroom is onderbroken. |

Selecteer het trechter-pictogram linksboven om te sorteren.

![dataflows-list](../../images/tutorials/monitor/dataflows-list.png)

Het sorteervenster wordt weergegeven. Selecteer de bron die u wilt openen in het schuifmenu en selecteer de gegevensstroom in de lijst aan de rechterkant. U kunt ook de ellipsen (`...`) knoop selecteren om meer beschikbare opties voor uw geselecteerde gegevensstroom te verhogen.

![sortDataFlow](../../images/tutorials/monitor/dataflows-sort.png)

De **[!UICONTROL Dataflow-activiteitenpagina]** bevat details over het aantal records dat wordt opgenomen en records die zijn mislukt, en informatie over de status van de gegevensstroom en de verwerkingstijd. Selecteer het kalenderpictogram boven de gegevensstroom om het tijdkader van uw innameregisters aan te passen.

![datflow-activity](../../images/tutorials/monitor/dataflow-activity.png)

Met de kalender kunt u de verschillende tijdframes voor opgenomen records bekijken. U kunt kiezen tussen een van de twee vooraf ingestelde opties &quot;[!UICONTROL Laatste 7 dagen]&quot; of &quot;[!UICONTROL Laatste 30 dagen]&quot;. U kunt ook een aangepast tijdframe instellen met de kalender. Selecteer het gewenste tijdkader en selecteer **[!UICONTROL Toepassen]** om door te gaan.

![stroomkalender](../../images/tutorials/monitor/flow-calendar.png)

Standaard geeft de activiteit **[!UICONTROL Dataflow]** het deelvenster **[!UICONTROL Eigenschappen]** weer dat is gekoppeld aan de dataflow. Selecteer de doorloop die in de lijst wordt uitgevoerd om de bijbehorende metagegevens weer te geven, inclusief informatie over de unieke uitvoerings-id.

Selecteer **[!UICONTROL Dataflow run start]** om het **[!UICONTROL Dataflow run overzicht]** te openen.

![run](../../images/tutorials/monitor/run-metadata.png)

Het **[!UICONTROL Dataflow looppas overzicht]** toont informatie over de dataflow met inbegrip van zijn meta-gegevens, gedeeltelijke innamestatus, en toegewezen foutendrempel. De bovenste koptekst bevat ook een foutoverzicht. De **[!UICONTROL foutensamenvatting]** bevat de specifieke fout op hoofdniveau die toont bij welke stap het innameproces een fout tegenkwam.

![data-run-overview](../../images/tutorials/monitor/dataflow-run-overview.png)

Raadpleeg de volgende tabel voor fouten die u kunt zien in het overzicht **** Fout.

| Fout | Beschrijving |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Er is een fout opgetreden tijdens het kopiëren van gegevens uit een bron. |
| `CONNECTOR-2001-500` | Er is een fout opgetreden tijdens het verwerken van gekopieerde gegevens naar [!DNL Platform]. Deze fout kan betrekking hebben op parseren, valideren of transformeren. |

De onderste helft van het scherm bevat informatie over **[!UICONTROL Dataflow-uitvoerfouten]**. Van hier kunt u ook de opgenomen bestanden weergeven, een voorbeeld bekijken en fouten downloaden of het bestandmanifest downloaden.

In de **[!UICONTROL sectie met uitvoerfouten]** in DataFlow worden de foutcode, het aantal mislukte records en informatie over de fout weergegeven.

Selecteer **[!UICONTROL Voorvertoning van foutdiagnostiek]** voor meer informatie over de innamefout.

![Dataflow-run-fouten](../../images/tutorials/monitor/dataflow-run-errors.png)

Het voorvertoningsvenster voor **[!UICONTROL foutdiagnostiek]** wordt weergegeven. In dit scherm wordt specifieke informatie weergegeven over de fout bij het opnemen, zoals de bestandsnaam, foutcode, de naam van de kolom waarin de fout is opgetreden en een beschrijving van de fout.

Deze sectie bevat ook een voorvertoning van de kolom die de fout bevat.

>[!IMPORTANT]
>
>Als u de voorvertoning van **[!UICONTROL foutdiagnostiek]** wilt inschakelen, moet u **[!UICONTROL Gedeeltelijke inname]** en **[!UICONTROL foutdiagnose]** activeren bij het configureren van een gegevensstroom. Als u dit doet, kan het systeem alle records scannen die tijdens de flowuitvoering worden ingevoerd.

![Voorvertoning-fout-diagnostiek](../../images/tutorials/monitor/preview-error-diagnostics.png)

Nadat u een voorbeeld van de fouten hebt weergegeven, kunt u **[!UICONTROL Downloaden]** vanuit het **[!UICONTROL venster Overzicht]** van de gegevensstroomuitvoering selecteren voor toegang tot volledige diagnostische foutmeldingen en het bestandmanifest downloaden. Zie de documenten over [foutdiagnose](../../../ingestion/batch-ingestion/partial.md#retrieve-errors) en het [downloaden van metagegevens](../../../ingestion/batch-ingestion/partial.md#download-metadata) voor meer informatie.

![Voorvertoning-fout-diagnostiek](../../images/tutorials/monitor/download.png)

Raadpleeg de zelfstudie over het [controleren van streaming dataflows voor meer informatie over het controleren van gegevensstromen](../../../ingestion/quality/monitor-data-flows.md)en het opnemen van gegevens.

## Volgende stappen

Door dit leerprogramma te volgen, hebt u met succes bestaande rekeningen en gegevensstromen van de **[!UICONTROL werkruimte van Bronnen]** betreden. Inkomende gegevens kunnen nu worden gebruikt door downstreamdiensten [!DNL Platform] zoals [!DNL Real-time Customer Profile] en [!DNL Data Science Workspace]. Raadpleeg de volgende documenten voor meer informatie:

- [Overzicht van het realtime klantprofiel](../../../profile/home.md)
- [Overzicht van de Data Science Workspace](../../../data-science-workspace/home.md)
