---
keywords: Experience Platform;home;populaire onderwerpen;ingestie;ingest batchgegevens;zelfstudie;batch-opname;zelfstudie;ui-handleiding;
solution: Experience Platform
title: Gegevens opnemen in Adobe Experience Platform
topic: tutorial
type: Tutorial
description: Met Adobe Experience Platform kunt u gegevens eenvoudig importeren als batchbestanden in de vorm van Parquet-bestanden of gegevens die overeenkomen met een bekend XDM-schema (Experience Data Model).
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 0%

---


# Gegevens opnemen in Adobe Experience Platform

Met Adobe Experience Platform kunt u gegevens eenvoudig als batchbestanden importeren in [!DNL Platform]. Voorbeelden van gegevens die moeten worden opgenomen kunnen profielgegevens van een vlak dossier in een systeem van CRM (zoals een dossier van het Pakket) of gegevens omvatten die aan een bekend [!DNL Experience Data Model] (XDM) schema in de Registratie van het Schema in overeenstemming zijn.

## Aan de slag

Als u deze zelfstudie wilt voltooien, moet u toegang hebben tot [!DNL Experience Platform]. Als u geen toegang tot een Organisatie IMS in [!DNL Experience Platform] hebt, gelieve met uw systeembeheerder te spreken alvorens te werk te gaan.

Als u gegevens liever wilt inslikken met API&#39;s voor gegevensinname, begint u met het lezen van de [Handleiding voor ontwikkelaars van batchinkt](../batch-ingestion/api-overview.md).

## Werkruimte Gegevensbestanden

Met de werkruimte Datasets in [!DNL Experience Platform] kunt u alle gegevenssets die uw IMS-organisatie heeft gemaakt, weergeven en beheren en nieuwe gegevenssets maken.

Bekijk de werkruimte Datasets door in de linkernavigatie op **[!UICONTROL Datasets]** te klikken. De werkruimte van Datasets bevat een lijst van datasets, met inbegrip van kolommen die naam tonen, (datum en tijd), bron, schema, en laatste partijstatus, evenals de datum en de tijd de dataset het laatst werd bijgewerkt.

>[!NOTE]
>
>Klik op het filterpictogram naast de bar van het Onderzoek om het filtreren mogelijkheden te gebruiken om slechts die datasets te bekijken die voor [!DNL Profile] worden toegelaten.

![Alle gegevenssets weergeven](../images/tutorials/ingest-batch-data/datasets-overview.png)

## Een gegevensset maken

Als u een gegevensset wilt maken, klikt u op **[!UICONTROL Gegevensset maken]** rechtsboven in de werkruimte Datasets.

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

Selecteer in het scherm **[!UICONTROL Dataset maken]** of u &quot;[!UICONTROL Gegevensset maken van schema]&quot; of &quot;[!UICONTROL Gegevensset maken van CSV-bestand]&quot; wilt gebruiken.

Voor dit leerprogramma, zal een schema worden gebruikt om de dataset tot stand te brengen. Klik **[!UICONTROL Gegevensset maken van schema]** om door te gaan.

![Gegevensbron selecteren](../images/tutorials/ingest-batch-data/create-dataset.png)

## Gegevenssetschema selecteren

Kies in het scherm **[!UICONTROL Selecteer Schema]** een schema door op het keuzerondje naast het schema te klikken dat u wilt gebruiken. Voor deze zelfstudie wordt de gegevensset gemaakt met het schema Loyalty-leden. Het gebruiken van de onderzoeksbar aan filterschema&#39;s is een nuttige manier om het nauwkeurige schema te vinden u zoekt.

Nadat u het keuzerondje naast het schema hebt geselecteerd dat u wilt gebruiken, klikt u op **[!UICONTROL Volgende]**.

![Schema selecteren](../images/tutorials/ingest-batch-data/select-schema.png)

## Gegevensset configureren

Op **[!UICONTROL vorm het scherm Dataset]**, zult u uw dataset een naam moeten geven en kan ook een beschrijving van de dataset eveneens verstrekken.

**Opmerkingen over gegevenssetnamen:**

- De namen van gegevenssets moeten kort en beschrijvend zijn, zodat de gegevensset later gemakkelijk in de bibliotheek kan worden gevonden.
- Dataset-namen moeten uniek zijn, wat betekent dat ze ook specifiek genoeg moeten zijn om in de toekomst niet opnieuw te worden gebruikt.
- Het is beste praktijken om extra informatie over de dataset te verstrekken gebruikend het beschrijvingsgebied, aangezien het andere gebruikers kan helpen tussen datasets in de toekomst differentiëren.

Als de gegevensset een naam en een beschrijving heeft, klikt u op **[!UICONTROL Voltooien]**.

![Gegevensset configureren](../images/tutorials/ingest-batch-data/configure-dataset.png)

## Gegevensactiviteit

Er is nu een lege dataset gemaakt en u bent teruggestuurd naar het tabblad Dataset Activity ]**in de werkruimte Datasets.**[!UICONTROL  U zou de naam van de dataset in de upper-left hoek van de werkruimte, samen met een bericht moeten zien dat &quot;Geen partijen zijn toegevoegd.&quot; Dit moet worden verwacht aangezien u nog geen partijen aan deze dataset hebt toegevoegd.

Rechts in de werkruimte Datasets ziet u het tabblad **[!UICONTROL Info]** met informatie over uw nieuwe gegevensset, zoals id, naam, beschrijving, tabelnaam, schema, streaming en bron. Het tabblad Info bevat ook informatie over het tijdstip waarop de gegevensset is gemaakt en de datum waarop deze voor het laatst is gewijzigd.

Ook in het lusje van Info is een **[!UICONTROL Profiel]** knevel die voor het toelaten van uw dataset voor gebruik met [!DNL Real-time Customer Profile] wordt gebruikt. Het gebruik van deze schakeloptie en [!DNL Real-time Customer Profile] worden nader toegelicht in de volgende sectie.

![Gegevensactiviteit](../images/tutorials/ingest-batch-data/sample-dataset.png)

## Gegevensset inschakelen voor [!DNL Real-time Customer Profile]

Datasets worden gebruikt voor het opnemen van gegevens in [!DNL Experience Platform], en die gegevens worden uiteindelijk gebruikt om individuen te identificeren en informatie te verbinden die uit veelvoudige bronnen komt. Deze samengevoegde informatie wordt een [!DNL Real-Time Customer Profile] genoemd. Om [!DNL Platform] te weten welke informatie in [!DNL Real-Time Profile] zou moeten worden omvat, kunnen datasets voor opneming worden gemerkt gebruikend **[!UICONTROL Profiel]** knevel.

Deze schakeloptie is standaard uitgeschakeld. Als u ervoor kiest om [!DNL Profile] in te schakelen, worden alle gegevens die in de dataset worden opgenomen gebruikt om een individu te identificeren en de [!DNL Real-Time Profile] aan elkaar te koppelen.

Raadpleeg de [Identity Service](../../identity-service/home.md)-documentatie voor meer informatie over [!DNL Real-time Customer Profile] en het werken met identiteiten.

Om de dataset voor [!DNL Real-time Customer Profile] toe te laten, klik **[!UICONTROL Profiel]** knevel in **[!UICONTROL Info]** tabel.

![Schakelen tussen profielen](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

Er verschijnt een dialoogvenster waarin u wordt gevraagd te bevestigen dat u de gegevensset wilt inschakelen voor [!DNL Real-time Customer Profile].

![Dialoogvenster Profiel inschakelen](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

Klik **[!UICONTROL Enable]** en de knevel zal blauw draaien, erop wijzend het is ingeschakeld.

![Ingeschakeld voor profiel](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## Gegevens toevoegen aan gegevensset

Gegevens kunnen op verschillende manieren aan een gegevensset worden toegevoegd. U zou kunnen verkiezen om [!DNL Data Ingestion] APIs of een partner van ETL zoals [!DNL Unifi] of [!DNL Informatica] te gebruiken. Voor deze zelfstudie worden gegevens toegevoegd aan de gegevensset met het tabblad **[!UICONTROL Gegevens toevoegen]** in de gebruikersinterface.

Als u gegevens aan de gegevensset wilt toevoegen, klikt u op het tabblad **[!UICONTROL Gegevens toevoegen]**. U kunt nu bestanden slepen en neerzetten of op uw computer bladeren naar de bestanden die u wilt toevoegen.

>[!NOTE]
>
>Platform ondersteunt twee bestandstypen voor gegevensinvoer, Parquet of JSON. U kunt maximaal vijf bestanden tegelijk toevoegen, waarbij de maximale bestandsgrootte van elk bestand 10 GB is.

![Tabblad Gegevens toevoegen](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## Een bestand uploaden

Als u een Parquet- of JSON-bestand dat u wilt uploaden sleept en neerzet (of bladert en selecteert), begint [!DNL Platform] direct met het verwerken van het bestand. Het dialoogvenster **[!UICONTROL Uploaden]** wordt weergegeven op het tabblad **[!UICONTROL Gegevens toevoegen]**, waarin de voortgang van het uploaden van het bestand wordt weergegeven.

![Het dialoogvenster Uploaden](../images/tutorials/ingest-batch-data/uploading-file.png)

## Dataset-meetgegevens

Nadat het bestand is geüpload, wordt op het tabblad **[!UICONTROL Datasetactiviteit]** niet meer aangegeven dat er geen batches zijn toegevoegd. In plaats daarvan bevat het tabblad **[!UICONTROL Dataset Activity]** nu gegevenssetmeetgegevens. Alle metriek tonen &quot;0&quot;in dit stadium aangezien de partij nog niet heeft geladen.

Onder aan het tabblad vindt u een lijst met de **[!UICONTROL Batch-id]** van de gegevens die zojuist zijn opgenomen via het proces [&quot;Gegevens toevoegen aan gegevensset&quot;](#add-data-to-dataset). Ook wordt informatie over de batch opgenomen, zoals de datum waarop de gegevens zijn ingevoerd, het aantal records dat is ingevoerd en de huidige status van de batch.

![Dataset-meetgegevens](../images/tutorials/ingest-batch-data/batch-id.png)

## Batchgegevens

Klik op **[!UICONTROL Batch-id]** om een **[!UICONTROL Batch-overzicht]** weer te geven en aanvullende gegevens over de batch weer te geven. Zodra de batch klaar is met laden, wordt de informatie over de batch bijgewerkt om het aantal records dat wordt ingevoerd en de bestandsgrootte weer te geven. De status verandert ook in &quot;Voltooid&quot; of &quot;Mislukt&quot;. Als de batch mislukt, bevat de sectie **[!UICONTROL Foutcode]** details over eventuele fouten tijdens de opname.

Raadpleeg de [Handleiding voor het oplossen van problemen bij inname in batch](../batch-ingestion/troubleshooting.md) voor meer informatie en veelgestelde vragen over het inslikken in batch.

Als u wilt terugkeren naar het scherm **[!UICONTROL Dataset Activity]**, klikt u op de naam van de gegevensset (**[!UICONTROL Loyalty Details]**) in de breadcrumb.

![Batchoverzicht](../images/tutorials/ingest-batch-data/batch-details.png)

## Gegevensset voorvertoning

Zodra de dataset klaar is, verschijnt een optie aan **[!UICONTROL Voorproef Dataset]** bij de bovenkant van **[!UICONTROL Dataset Activiteit]** tabel.

Klik **[!UICONTROL Gegevensset voorvertonen]** om een dialoogvenster te openen met voorbeeldgegevens uit de gegevensset. Als de dataset gebruikend een schema werd gecreeerd, zullen de details voor het datasetschema op de linkerkant van de voorproef verschijnen. U kunt het schema uitbreiden gebruikend de pijlen om de schemastructuur te zien. Elke kolomkop in de voorvertoningsgegevens vertegenwoordigt een veld in de gegevensset.

![Gegevens over gegevensset](../images/tutorials/ingest-batch-data/dataset-preview.png)

## Volgende stappen en extra bronnen

Nu u een dataset hebt gecreeerd en met succes gegevens in [!DNL Experience Platform] opgenomen, kunt u deze stappen herhalen om een nieuwe dataset tot stand te brengen of meer gegevens in de bestaande dataset in te voeren.

Lees voor meer informatie over batch-opname het [Batch Ingestieoverzicht](../batch-ingestion/overview.md) en volg de onderstaande video als aanvulling op uw training.

>[!WARNING]
>
>De interface [!DNL Platform] die in de volgende video wordt getoond is verouderd. Raadpleeg de bovenstaande documentatie voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)