---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Gegevens opnemen in Adobe Experience Platform
topic: tutorial
translation-type: tm+mt
source-git-commit: 6e4a3ebe84c82790f58f8ec54e6f72c2aca0b7da
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 0%

---


# Gegevens opnemen in Adobe Experience Platform

Met Adobe Experience Platform kunt u gegevens eenvoudig importeren in [!DNL Platform] de vorm van batchbestanden. Voorbeelden van gegevens die moeten worden opgenomen, kunnen profielgegevens bevatten van een plat bestand in een CRM-systeem (zoals een parketbestand) of gegevens die in overeenstemming zijn met een bekend [!DNL Experience Data Model] (XDM) schema in de Schemaregistratie.

## Aan de slag

Voor het voltooien van deze zelfstudie hebt u toegang tot [!DNL Experience Platform]. Als u geen toegang hebt tot een IMS-organisatie in [!DNL Experience Platform], neemt u contact op met uw systeembeheerder voordat u verdergaat.

Als u gegevens liever met API&#39;s voor gegevensinname wilt invoeren, leest u eerst de handleiding voor [Batch Ingestie-ontwikkelaars](../batch-ingestion/api-overview.md).

## Werkruimte Gegevensbestanden

De werkruimte van Datasets binnen [!DNL Experience Platform] staat u toe om alle datasets te bekijken en te beheren die uw organisatie IMS heeft gemaakt, evenals nieuwe te creëren.

Bekijk de werkruimte Datasets door in de linkernavigatie op **[!UICONTROL Datasets]** te klikken. De werkruimte van Datasets bevat een lijst van datasets, met inbegrip van kolommen die _[!UICONTROL Naam]_, _[!UICONTROL Gemaakt]_ (datum en tijd), _[!UICONTROL Bron]_, _[!UICONTROL Schema]_, en de Status _[!UICONTROL van de]___ Laatste Partij tonen, evenals de datum en de tijd de dataset was Last Updated.

>[!NOTE]
>
>Klik op het filterpictogram naast de bar van het Onderzoek om het filtreren mogelijkheden te gebruiken om slechts die datasets te bekijken die voor worden toegelaten [!DNL Profile].

![Alle gegevenssets weergeven](../images/tutorials/ingest-batch-data/datasets_workspace.png)

## Een gegevensset maken

Als u een gegevensset wilt maken, klikt u op Gegevensset **[!UICONTROL maken]** in de rechterbovenhoek van de werkruimte Datasets.

Selecteer in het scherm Dataset **** maken of u Dataset[!UICONTROL maken van schema]of Gegevensset[!UICONTROL maken van CSV-bestand]wilt gebruiken.

Voor dit leerprogramma, zal een schema worden gebruikt om de dataset tot stand te brengen. Klik op Gegevensset **[!UICONTROL maken van schema]** om door te gaan.

![Gegevensbron selecteren](../images/tutorials/ingest-batch-data/create_dataset.png)

## Gegevenssetschema selecteren

Kies in het scherm Schema **** selecteren een schema door op het keuzerondje naast het schema te klikken dat u wilt gebruiken. Voor deze zelfstudie wordt de gegevensset gemaakt met het schema Loyalty-leden. Het gebruiken van de onderzoeksbar aan filterschema&#39;s is een nuttige manier om het nauwkeurige schema te vinden u zoekt.

Als u het keuzerondje hebt geselecteerd naast het schema dat u wilt gebruiken, klikt u op **[!UICONTROL Volgende]**.

![Schema selecteren](../images/tutorials/ingest-batch-data/select_schema.png)

## Gegevensset configureren

Op het **[!UICONTROL Configure scherm van de Dataset]** , zult u uw dataset een **[!UICONTROL Naam]** moeten geven en kan ook een **[!UICONTROL Beschrijving]** van de dataset eveneens verstrekken.

**Opmerkingen over gegevenssetnamen:**

- De namen van gegevenssets moeten kort en beschrijvend zijn, zodat de gegevensset later gemakkelijk in de bibliotheek kan worden gevonden.
- Dataset-namen moeten uniek zijn, wat betekent dat ze ook specifiek genoeg moeten zijn om in de toekomst niet opnieuw te worden gebruikt.
- Het is beste praktijken om extra informatie over de dataset te verstrekken gebruikend het beschrijvingsgebied, aangezien het andere gebruikers kan helpen tussen datasets in de toekomst differentiëren.

Als de gegevensset een naam en een beschrijving heeft, klikt u op **[!UICONTROL Voltooien]**.

![Gegevensset configureren](../images/tutorials/ingest-batch-data/configure_dataset.png)

## Gegevensactiviteit

Een lege dataset is nu gecreeerd en u bent teruggekeerd aan het lusje van de Activiteit **[!UICONTROL van de]** Dataset in de werkruimte van Datasets. U zou de naam van de dataset in de upper-left hoek van de werkruimte, samen met een bericht moeten zien dat &quot;Geen partijen zijn toegevoegd.&quot; Dit moet worden verwacht aangezien u nog geen partijen aan deze dataset hebt toegevoegd.

Rechts in de werkruimte Datasets ziet u het tabblad **[!UICONTROL Info]** met informatie over uw nieuwe gegevensset, zoals de id _[!UICONTROL van de]_ gegevensset, de _[!UICONTROL naam]_, de _[!UICONTROL beschrijving]_, de naam _[!UICONTROL van de]_ tabel, de naam ______ van deTabel, de combinatieSchema, de combinatieStreamingen deBron. Het tabblad Info bevat ook informatie over het tijdstip waarop de gegevensset is _[!UICONTROL gemaakt]_ en de datum waarop deze voor het _[!UICONTROL laatst is gewijzigd]_ .

Ook in het lusje van Info is een _[!UICONTROL knevel van het Profiel]_ die voor het toelaten van uw dataset voor gebruik met wordt gebruikt [!DNL Real-time Customer Profile]. Het gebruik van deze schakeloptie en [!DNL Real-time Customer Profile], wordt nader toegelicht in de volgende sectie.

![Gegevensactiviteit](../images/tutorials/ingest-batch-data/dataset_activity.png)

## Gegevensset inschakelen voor [!DNL Real-time Customer Profile]

Datasets worden gebruikt voor het opnemen van gegevens in [!DNL Experience Platform], en dat gegeven wordt uiteindelijk gebruikt om individuen te identificeren en informatie te binden die uit veelvoudige bronnen komt. Die samengevoegde informatie wordt een [!DNL Real-Time Customer Profile]genoemd. Om te weten [!DNL Platform] welke informatie in de [!DNL Real-Time Profile]lijst moet worden opgenomen, kunnen datasets voor opneming worden gemerkt gebruikend de **[!UICONTROL knevel van het Profiel]** .

Deze schakeloptie is standaard uitgeschakeld. Als u verkiest om op te schakelen [!DNL Profile], zullen alle gegevens die in de dataset worden opgenomen worden gebruikt helpen een individu identificeren en hen verbinden [!DNL Real-Time Profile].

Raadpleeg de documentatie bij [!DNL Real-time Customer Profile] Identiteitsservice [voor meer informatie over](../../identity-service/home.md) en het werken met identiteiten.

Als u de gegevensset wilt inschakelen voor [!DNL Real-time Customer Profile], klikt u op de schakeloptie **[!UICONTROL Profiel]** op het tabblad **[!UICONTROL Info]** .

![Schakelen tussen profielen](../images/tutorials/ingest-batch-data/enable_dataset_unified_profile.png)

Er verschijnt een dialoogvenster waarin u wordt gevraagd te bevestigen dat u de gegevensset wilt inschakelen voor [!DNL Real-time Customer Profile].

![Dialoogvenster Profiel inschakelen](../images/tutorials/ingest-batch-data/confirm_dataset_enable.png)

Klik op **[!UICONTROL Inschakelen]** en de schakeloptie wordt blauw om aan te geven dat deze is ingeschakeld.

![Ingeschakeld voor profiel](../images/tutorials/ingest-batch-data/dataset_enabled.png)

## Gegevens toevoegen aan gegevensset

Gegevens kunnen op verschillende manieren aan een gegevensset worden toegevoegd. U kunt ervoor kiezen API&#39; [!DNL Data Ingestion] s of een ETL-partner, zoals [!DNL Unifi] of [!DNL Informatica]. Voor dit leerprogramma, zullen de gegevens aan de dataset worden toegevoegd gebruikend het **[!UICONTROL Add lusje van Gegevens]** binnen UI.

Als u gegevens aan de gegevensset wilt toevoegen, klikt u op het tabblad Gegevens **** toevoegen. U kunt nu bestanden slepen en neerzetten of op uw computer bladeren naar de bestanden die u wilt toevoegen.

>[!NOTE]
>
>Platform ondersteunt twee bestandstypen voor gegevensinvoer, parket of JSON. U kunt maximaal vijf bestanden tegelijk toevoegen, waarbij de maximale bestandsgrootte van elk bestand 10 GB is.

![Tabblad Gegevens toevoegen](../images/tutorials/ingest-batch-data/add_data.png)

## Een bestand uploaden

Wanneer u een parket of JSON-bestand dat u wilt uploaden sleept en neerzet (of bladert en selecteert), [!DNL Platform] wordt direct begonnen met het verwerken van het bestand. Het dialoogvenster **[!UICONTROL Uploaden]** wordt weergegeven op het tabblad Gegevens **** toevoegen met de voortgang van het uploaden van het bestand.

![Het dialoogvenster Uploaden](../images/tutorials/ingest-batch-data/uploading.png)

## Dataset-meetgegevens

Nadat het bestand is geüpload, wordt op het tabblad **[!UICONTROL Datasetactiviteit]** niet meer aangegeven dat er geen batches zijn toegevoegd. In plaats daarvan, toont het lusje van de Activiteit *[!UICONTROL van de]* Dataset nu datasetmetriek. Alle metriek tonen &quot;0&quot;in dit stadium aangezien de partij nog niet heeft geladen.

Onder aan het tabblad vindt u een lijst met de _[!UICONTROL batch-id]_ van de gegevens die zojuist zijn opgenomen via het proces [&quot;Gegevens toevoegen aan gegevensset&quot;](#add-data-to-dataset) . Ook wordt informatie over de batch opgenomen, waaronder de datum van _[!UICONTROL Ingested]_ , het aantal _[!UICONTROL Records Ingested]_ en de huidige _[!UICONTROL status]_ van de batch.

![Dataset-meetgegevens](../images/tutorials/ingest-batch-data/batch_loading.png)

## Batchgegevens

Klik op de _[!UICONTROL Batch-id]_ om een **[!UICONTROL Batch-overzicht]** weer te geven met aanvullende gegevens over de batch. Zodra de partij klaar is met laden, zal de informatie over de partij worden bijgewerkt om het aantal _[!UICONTROL Verweven]_ Verslagen en de Grootte _[!UICONTROL van het]_ Dossier te tonen. De _[!UICONTROL status]_ wordt ook gewijzigd in &quot;Voltooid&quot; of &quot;Mislukt&quot;. Als de partij ontbreekt zal de sectie van de Code _[!UICONTROL van de]_ Fout details betreffende om het even welke fouten tijdens opname bevatten.

Raadpleeg de handleiding voor het oplossen van problemen bij [Batch-inname voor meer informatie en veelgestelde vragen over het gebruik van batch-inname](../batch-ingestion/troubleshooting.md).

Om aan het scherm van de Activiteit **[!UICONTROL van de]** Dataset terug te keren, klik de naam van de dataset (_[!UICONTROL Loyalty Details]_) in breadcrumb.

![Batchoverzicht](../images/tutorials/ingest-batch-data/batch_overview.png)

## Gegevensset voorvertoning

Zodra de dataset klaar is, verschijnt een optie om de Dataset **[!UICONTROL van de]** Voorproef bij de bovenkant van de Activiteit **[!UICONTROL van de]** Dataset.

Klik de Dataset **[!UICONTROL van de]** Voorproef om een dialoog te openen die steekproefgegevens van binnen de dataset toont. Als de dataset gebruikend een schema werd gecreeerd, zullen de details voor het datasetschema op de linkerkant van de voorproef verschijnen. U kunt het schema uitbreiden gebruikend de pijlen om de schemastructuur te zien. Elke kolomkop in de voorvertoningsgegevens vertegenwoordigt een veld in de gegevensset.

![Gegevens over gegevensset](../images/tutorials/ingest-batch-data/dataset_details.png)

## Volgende stappen en extra bronnen

Nu u een dataset hebt gecreeerd en met succes gegevens in hebt opgenomen [!DNL Experience Platform], kunt u deze stappen herhalen om een nieuwe dataset tot stand te brengen of meer gegevens in de bestaande dataset in te voeren.

Lees voor meer informatie over batch-opname het overzicht [van de](../batch-ingestion/overview.md) Batch-inname en volg de onderstaande video als aanvulling op uw studie.

>[!WARNING]
>
>De [!DNL Platform] UI die in de volgende video wordt getoond is verouderd. Raadpleeg de bovenstaande documentatie voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)
