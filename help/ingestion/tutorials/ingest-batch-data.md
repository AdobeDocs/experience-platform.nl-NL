---
keywords: Experience Platform;home;populaire onderwerpen;ingestie;ingest batchgegevens;zelfstudie;batch-opname;zelfstudie;ui-handleiding;
solution: Experience Platform
title: Gegevens opnemen in Experience Platform
type: Tutorial
description: Met Adobe Experience Platform kunt u gegevens eenvoudig importeren als batchbestanden in de vorm van Parquet-bestanden of gegevens die overeenkomen met een bekend XDM-schema (Experience Data Model).
exl-id: a4a7358d-b117-4d81-8cb0-3dbbfeccdcbd
source-git-commit: 31631b03b6ff1e50e55c01e948fae5c29fd618dd
workflow-type: tm+mt
source-wordcount: '1261'
ht-degree: 0%

---

# Gegevens opnemen in Adobe Experience Platform

Met Adobe Experience Platform kunt u gegevens eenvoudig als batchbestanden importeren in [!DNL Experience Platform] . Voorbeelden van gegevens die moeten worden opgenomen, kunnen profielgegevens bevatten van een plat bestand in een CRM-systeem (zoals een Parquet-bestand) of gegevens die voldoen aan een bekend [!DNL Experience Data Model] (XDM) schema in de Schema-register.

## Aan de slag

U moet toegang hebben tot [!DNL Experience Platform] om deze zelfstudie te kunnen voltooien. Als u geen toegang hebt tot een organisatie in [!DNL Experience Platform] , neemt u contact op met uw systeembeheerder voordat u verdergaat.

Als u verkiest gegevens in te voeren gebruikend de Ingestie APIs van Gegevens gelieve te beginnen door de [ gids van de ontwikkelaar van de Ingestie van de Partij van de Partij ](../batch-ingestion/api-overview.md) te lezen.

## Werkruimte Gegevensbestanden

Met de werkruimte Datasets in [!DNL Experience Platform] kunt u alle gegevenssets die uw organisatie heeft gemaakt, weergeven en beheren en nieuwe gegevenssets maken.

U kunt de werkruimte Datasets weergeven door op **[!UICONTROL Datasets]** te klikken in de linkernavigatie. De werkruimte van Datasets bevat een lijst van datasets, met inbegrip van kolommen die naam tonen, (datum en tijd), bron, schema, en laatste partijstatus, evenals de datum en de tijd de dataset het laatst werd bijgewerkt.

>[!NOTE]
>
>Klik op het filterpictogram naast de zoekbalk om filtermogelijkheden te gebruiken om alleen die datasets weer te geven die zijn ingeschakeld voor [!DNL Profile] .

![ Mening alle datasets ](../images/tutorials/ingest-batch-data/datasets-overview.png)

## Een gegevensset maken

Als u een gegevensset wilt maken, klikt u op **[!UICONTROL Create Dataset]** in de rechterbovenhoek van de werkruimte Datasets.

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

Voor het **[!UICONTROL Create Dataset]** scherm, selecteer of u &quot; [!UICONTROL Create Dataset from Schema]&quot;of &quot;[!UICONTROL Create Dataset from CSV File]&quot;zou willen.

Voor deze zelfstudie wordt een schema gebruikt om de dataset te maken. Klik op **[!UICONTROL Create Dataset from Schema]** om door te gaan.

![ Uitgezochte gegevensbron ](../images/tutorials/ingest-batch-data/create-dataset.png)

## Gegevenssetschema selecteren

Kies in het scherm **[!UICONTROL Select Schema]** een schema door op het keuzerondje naast het schema te klikken dat u wilt gebruiken. Voor deze zelfstudie wordt de gegevensset gemaakt met het schema Loyalty-leden. Het gebruiken van de onderzoeksbar aan filterschema&#39;s is een nuttige manier om het nauwkeurige schema te vinden u zoekt.

Als u het keuzerondje hebt geselecteerd naast het schema dat u wilt gebruiken, klikt u op **[!UICONTROL Next]** .

![ Uitgezochte schema ](../images/tutorials/ingest-batch-data/select-schema.png)

## Gegevensset configureren

Op het **[!UICONTROL Configure Dataset]** scherm, zult u moeten uw dataset een naam geven en kan ook een beschrijving van de dataset ook verstrekken.

**Nota&#39;s op de Namen van Dataset:**

- De namen van gegevenssets moeten kort en beschrijvend zijn, zodat de gegevensset later gemakkelijk in de bibliotheek kan worden gevonden.
- Dataset-namen moeten uniek zijn, wat betekent dat ze ook specifiek genoeg moeten zijn om in de toekomst niet opnieuw te worden gebruikt.
- Het is beste praktijken om extra informatie over de dataset te verstrekken gebruikend het beschrijvingsgebied, aangezien het andere gebruikers kan helpen tussen datasets in de toekomst differentiëren.

Als de gegevensset een naam en beschrijving heeft, klikt u op **[!UICONTROL Finish]** .

![ vorm dataset ](../images/tutorials/ingest-batch-data/configure-dataset.png)

## Gegevensactiviteit

Er is nu een lege dataset gemaakt en u bent teruggestuurd naar het tabblad **[!UICONTROL Dataset Activity]** in de werkruimte Datasets. U zou de naam van de dataset in de upper-left hoek van de werkruimte, samen met een bericht moeten zien dat &quot;Geen partijen zijn toegevoegd.&quot; Dit moet worden verwacht aangezien u nog geen partijen aan deze dataset hebt toegevoegd.

Rechts in de werkruimte Datasets ziet u het tabblad **[!UICONTROL Info]** met informatie over uw nieuwe gegevensset, zoals de id van de gegevensset, naam, beschrijving, tabelnaam, schema, streaming en bron. Het tabblad Info bevat ook informatie over het tijdstip waarop de gegevensset is gemaakt en de datum waarop deze voor het laatst is gewijzigd.

Op het tabblad Info vindt u ook een **[!UICONTROL Profile]** -schakeloptie die wordt gebruikt voor het inschakelen van uw gegevensset voor gebruik met [!DNL Real-Time Customer Profile] . Het gebruik van deze schakeloptie en [!DNL Real-Time Customer Profile] wordt nader toegelicht in de volgende sectie.

![ de activiteit van de Dataset ](../images/tutorials/ingest-batch-data/sample-dataset.png)

## Gegevensset inschakelen voor [!DNL Real-Time Customer Profile] {#enable-for-profile}

Datasets worden gebruikt voor het opnemen van gegevens in [!DNL Experience Platform] en die gegevens worden uiteindelijk gebruikt om individuen te identificeren en informatie die uit meerdere bronnen afkomstig is aan elkaar te koppelen. Deze samengevoegde informatie wordt een [!DNL Real-Time Customer Profile] genoemd. [!DNL Experience Platform] weet welke informatie moet worden opgenomen in de [!DNL Real-Time Profile] , dus gegevenssets kunnen worden gemarkeerd voor opname met de **[!UICONTROL Profile]** -schakeloptie.

Deze schakeloptie is standaard uitgeschakeld. Als u [!DNL Profile] inschakelt, worden alle gegevens die in de gegevensset worden ingevoerd, gebruikt om een individu te identificeren en de gegevens aan elkaar te koppelen [!DNL Real-Time Profile] .

Om meer over [!DNL Real-Time Customer Profile] en het werken met identiteiten te leren, te herzien gelieve de [ documentatie van de Dienst van de Identiteit ](../../identity-service/home.md).

Als u de gegevensset voor [!DNL Real-Time Customer Profile] wilt inschakelen, klikt u op de **[!UICONTROL Profile]** -schakeloptie op het tabblad **[!UICONTROL Info]** .

![ knevel van het Profiel ](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

Er verschijnt een dialoogvenster waarin u wordt gevraagd te bevestigen dat u de gegevensset wilt inschakelen voor [!DNL Real-Time Customer Profile] .

![ laat de dialoog van het Profiel ](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png) toe

Klik op **[!UICONTROL Enable]** en de schakeloptie wordt blauw om aan te geven dat deze is ingeschakeld.

![ Toegelaten voor Profiel ](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## Gegevens toevoegen aan gegevensset

Gegevens kunnen op verschillende manieren aan een gegevensset worden toegevoegd. U kunt ervoor kiezen om [!DNL Data Ingestion] API&#39;s of een ETL-partner zoals [!DNL Unifi] of [!DNL Informatica] te gebruiken. Voor deze zelfstudie worden gegevens toegevoegd aan de gegevensset met het tabblad **[!UICONTROL Add Data]** in de gebruikersinterface.

Klik op het tabblad **[!UICONTROL Add Data]** om gegevens toe te voegen aan de gegevensset. U kunt nu bestanden slepen en neerzetten of op uw computer bladeren naar de bestanden die u wilt toevoegen.

>[!NOTE]
>
>Experience Platform ondersteunt twee bestandstypen voor gegevensinvoer, Parquet of JSON. U kunt maximaal vijf bestanden tegelijk toevoegen, waarbij de maximale bestandsgrootte van elk bestand 1 GB is.

![ voeg Gegevens tabel ](../images/tutorials/ingest-batch-data/drag-and-drop.png) toe

## Een bestand uploaden {#upload-file}

Wanneer u een Parquet- of JSON-bestand dat u wilt uploaden sleept en neerzet (of bladert en selecteert), begint [!DNL Experience Platform] onmiddellijk met het verwerken van het bestand. Op het tabblad **[!UICONTROL Add Data]** wordt een dialoogvenster **[!UICONTROL Uploading]** weergegeven met de voortgang van het uploaden van het bestand.

![ Uploading dialoog ](../images/tutorials/ingest-batch-data/uploading-file.png)

## Dataset-meetgegevens

Nadat het bestand is geüpload, ziet u op het tabblad **[!UICONTROL Dataset Activity]** niet meer dat er geen batches zijn toegevoegd. In plaats daarvan bevat het tabblad **[!UICONTROL Dataset Activity]** nu gegevenssetgegevens. Alle metriek tonen &quot;0&quot;in dit stadium aangezien de partij nog niet heeft geladen.

Bij de bodem van het lusje is een lijst die **[!UICONTROL Batch ID]** van de gegevens toont die enkel door [ &quot;werden opgenomen voeg gegevens aan dataset&quot;](#add-data-to-dataset) proces toe. Ook wordt informatie over de batch opgenomen, zoals de datum waarop de gegevens zijn ingevoerd, het aantal records dat is ingevoerd en de huidige status van de batch.

![ metriek van de Dataset ](../images/tutorials/ingest-batch-data/batch-id.png)

## Batchgegevens

Klik op **[!UICONTROL Batch ID]** om een **[!UICONTROL Batch Overview]** weer te geven en aanvullende gegevens over de batch weer te geven. Zodra de batch klaar is met laden, wordt de informatie over de batch bijgewerkt om het aantal records dat wordt ingevoerd en de bestandsgrootte weer te geven. De status verandert ook in &quot;Voltooid&quot; of &quot;Mislukt&quot;. Als de batch mislukt, bevat de sectie **[!UICONTROL Error Code]** details over eventuele fouten tijdens de inname.

Voor meer informatie en vaak gestelde vragen betreffende batch-opname, zie de [ het oplossen van problemengids van de Opname van de Partij ](../batch-ingestion/troubleshooting.md).

Als u wilt terugkeren naar het scherm **[!UICONTROL Dataset Activity]** , klikt u op de naam van de gegevensset ( **[!UICONTROL Loyalty Details]** ) in de broodkruimel.

![ Overzicht van de Partij ](../images/tutorials/ingest-batch-data/batch-details.png)

## Gegevensset voorvertoning

Zodra de dataset klaar is, verschijnt een optie aan **[!UICONTROL Preview Dataset]** bij de bovenkant van **[!UICONTROL Dataset Activity]** tabel.

Klik op **[!UICONTROL Preview Dataset]** om een dialoogvenster te openen met voorbeeldgegevens uit de gegevensset. Als de dataset gebruikend een schema werd gecreeerd, zullen de details voor het datasetschema op de linkerkant van de voorproef verschijnen. U kunt het schema uitbreiden gebruikend de pijlen om de schemastructuur te zien. Elke kolomkop in de voorvertoningsgegevens vertegenwoordigt een veld in de gegevensset.

![ de details van de Dataset ](../images/tutorials/ingest-batch-data/dataset-preview.png)

## Volgende stappen en extra bronnen

Nu u een dataset hebt gecreeerd en met succes gegevens in [!DNL Experience Platform] opgenomen, kunt u deze stappen herhalen om een nieuwe dataset tot stand te brengen of meer gegevens in de bestaande dataset in te voeren.

Om meer over partijingestie te leren, te lezen gelieve het [ overzicht van de Ingestie van de Partij ](../batch-ingestion/overview.md) en uw het leren aan te vullen door de video hieronder te letten.

>[!WARNING]
>
>De gebruikersinterface van [!DNL Experience Platform] in de volgende video is verouderd. Raadpleeg de bovenstaande documentatie voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)
