---
keywords: Experience Platform;home;populaire onderwerpen;ingestie;ingest batchgegevens;zelfstudie;batch-opname;zelfstudie;ui-handleiding;
solution: Experience Platform
title: Gegevens in Experience Platform opnemen
topic-legacy: tutorial
type: Tutorial
description: Met Adobe Experience Platform kunt u gegevens eenvoudig importeren als batchbestanden in de vorm van Parquet-bestanden of gegevens die overeenkomen met een bekend XDM-schema (Experience Data Model).
exl-id: a4a7358d-b117-4d81-8cb0-3dbbfeccdcbd
source-git-commit: e7fc8a168a48cc6fadda62efda9ee9eb3025ab51
workflow-type: tm+mt
source-wordcount: '1261'
ht-degree: 0%

---

# Gegevens opnemen in Adobe Experience Platform

Met Adobe Experience Platform kunt u eenvoudig gegevens importeren in [!DNL Platform] als batchbestanden. Voorbeelden van gegevens die moeten worden opgenomen, kunnen profielgegevens van een vlak bestand in een CRM-systeem (zoals een Parquet-bestand) of gegevens bevatten die overeenkomen met een bekende versie [!DNL Experience Data Model] (XDM) schema in de Registratie van het Schema.

## Aan de slag

Als u deze zelfstudie wilt voltooien, moet u toegang hebben tot [!DNL Experience Platform]. Als u geen toegang hebt tot een IMS-organisatie in [!DNL Experience Platform], spreek gelieve met uw systeembeheerder alvorens te werk te gaan.

Als u gegevens liever wilt invoeren met API&#39;s voor gegevensinname, begint u met het lezen van de [Handleiding voor ontwikkelaars van batchverwerking](../batch-ingestion/api-overview.md).

## Werkruimte Gegevensbestanden

De werkruimte Datasets binnen [!DNL Experience Platform] staat u toe om alle datasets te bekijken en te beheren die uw organisatie IMS heeft gemaakt, evenals nieuwe te creëren.

De werkruimte Datasets weergeven door op **[!UICONTROL Datasets]** in de linkernavigatie. De werkruimte van Datasets bevat een lijst van datasets, met inbegrip van kolommen die naam tonen, (datum en tijd), bron, schema, en laatste partijstatus, evenals de datum en de tijd de dataset het laatst werd bijgewerkt.

>[!NOTE]
>
>Klik op het filterpictogram naast de zoekbalk om filtermogelijkheden te gebruiken om alleen die datasets weer te geven die zijn ingeschakeld voor [!DNL Profile].

![Alle gegevenssets weergeven](../images/tutorials/ingest-batch-data/datasets-overview.png)

## Een gegevensset maken

Als u een gegevensset wilt maken, klikt u op **[!UICONTROL Create Dataset]** in de rechterbovenhoek van de werkruimte Datasets.

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

Op de **[!UICONTROL Create Dataset]** scherm, selecteer of u &quot;[!UICONTROL Create Dataset from Schema]&quot; of &quot;[!UICONTROL Create Dataset from CSV File]&quot;.

Voor dit leerprogramma, zal een schema worden gebruikt om de dataset tot stand te brengen. Klikken **[!UICONTROL Create Dataset from Schema]** om door te gaan.

![Gegevensbron selecteren](../images/tutorials/ingest-batch-data/create-dataset.png)

## Gegevenssetschema selecteren

Op de **[!UICONTROL Select Schema]** , kiest u een schema door op het keuzerondje naast het schema te klikken dat u wilt gebruiken. Voor deze zelfstudie wordt de gegevensset gemaakt met het schema Loyalty-leden. Het gebruiken van de onderzoeksbar aan filterschema&#39;s is een nuttige manier om het nauwkeurige schema te vinden u zoekt.

Als u het keuzerondje hebt geselecteerd naast het schema dat u wilt gebruiken, klikt u op **[!UICONTROL Next]**.

![Schema selecteren](../images/tutorials/ingest-batch-data/select-schema.png)

## Gegevensset configureren

Op de **[!UICONTROL Configure Dataset]** scherm, zult u uw dataset een naam moeten geven en kan ook een beschrijving van de dataset ook verstrekken.

**Opmerkingen over gegevenssetnamen:**

- De namen van gegevenssets moeten kort en beschrijvend zijn, zodat de gegevensset later gemakkelijk in de bibliotheek kan worden gevonden.
- Dataset-namen moeten uniek zijn, wat betekent dat ze ook specifiek genoeg moeten zijn om in de toekomst niet opnieuw te worden gebruikt.
- Het is beste praktijken om extra informatie over de dataset te verstrekken gebruikend het beschrijvingsgebied, aangezien het andere gebruikers kan helpen tussen datasets in de toekomst differentiëren.

Als de gegevensset een naam en beschrijving heeft, klikt u op **[!UICONTROL Finish]**.

![Gegevensset configureren](../images/tutorials/ingest-batch-data/configure-dataset.png)

## Gegevensactiviteit

Er is nu een lege dataset gemaakt en u bent teruggestuurd naar de **[!UICONTROL Dataset Activity]** in de werkruimte Datasets. U zou de naam van de dataset in de upper-left hoek van de werkruimte, samen met een bericht moeten zien dat &quot;Geen partijen zijn toegevoegd.&quot; Dit moet worden verwacht aangezien u nog geen partijen aan deze dataset hebt toegevoegd.

Rechts in de werkruimte Datasets ziet u de **[!UICONTROL Info]** tabblad met informatie over uw nieuwe gegevensset, zoals id van de gegevensset, naam, beschrijving, tabelnaam, schema, streaming en bron. Het tabblad Info bevat ook informatie over het tijdstip waarop de gegevensset is gemaakt en de datum waarop deze voor het laatst is gewijzigd.

Ook op het tabblad Info is een  **[!UICONTROL Profile]** knevel dat voor het toelaten van uw dataset voor gebruik met wordt gebruikt [!DNL Real-time Customer Profile]. gebruik van deze schakeloptie, en [!DNL Real-time Customer Profile], zal nader worden toegelicht in het volgende gedeelte.

![Gegevensactiviteit](../images/tutorials/ingest-batch-data/sample-dataset.png)

## Gegevensset inschakelen voor [!DNL Real-time Customer Profile]

Datasets worden gebruikt voor het opnemen van gegevens in [!DNL Experience Platform], en die gegevens worden uiteindelijk gebruikt om individuen te identificeren en informatie uit meerdere bronnen te koppelen. Die samengevoegde informatie wordt een [!DNL Real-Time Customer Profile]. Om [!DNL Platform] te weten welke informatie in de [!DNL Real-Time Profile]kunnen gegevenssets worden gemarkeerd voor opname met behulp van de **[!UICONTROL Profile]** schakelen.

Deze schakeloptie is standaard uitgeschakeld. Als u schakelt [!DNL Profile], worden alle gegevens die in de gegevensset worden opgenomen, gebruikt om een individu te identificeren en zijn [!DNL Real-Time Profile].

Meer informatie over [!DNL Real-time Customer Profile] en werken met identiteiten, raadpleeg de [Identiteitsservice](../../identity-service/home.md) documentatie.

Om de dataset voor toe te laten [!DNL Real-time Customer Profile]klikt u op de knop **[!UICONTROL Profile]** schakelen in de **[!UICONTROL Info]** tab.

![Schakelen tussen profielen](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

Er verschijnt een dialoogvenster waarin u wordt gevraagd te bevestigen dat u de gegevensset wilt inschakelen voor [!DNL Real-time Customer Profile].

![Dialoogvenster Profiel inschakelen](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

Klikken **[!UICONTROL Enable]** en de schakeloptie wordt blauw, wat aangeeft dat de schakeloptie is ingeschakeld.

![Ingeschakeld voor profiel](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## Gegevens toevoegen aan gegevensset

Gegevens kunnen op verschillende manieren aan een gegevensset worden toegevoegd. U kunt desgewenst [!DNL Data Ingestion] API&#39;s of een ETL-partner zoals [!DNL Unifi] of [!DNL Informatica]. Voor deze zelfstudie worden gegevens toegevoegd aan de gegevensset met de **[!UICONTROL Add Data]** in de gebruikersinterface.

Als u wilt beginnen met het toevoegen van gegevens aan de gegevensset, klikt u op de knop **[!UICONTROL Add Data]** tab. U kunt nu bestanden slepen en neerzetten of op uw computer bladeren naar de bestanden die u wilt toevoegen.

>[!NOTE]
>
>Platform ondersteunt twee bestandstypen voor gegevensinvoer, Parquet of JSON. U kunt maximaal vijf bestanden tegelijk toevoegen, waarbij de maximale bestandsgrootte van elk bestand 1 GB is.

![Tabblad Gegevens toevoegen](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## Een bestand uploaden

Nadat u een Parquet- of JSON-bestand dat u wilt uploaden hebt gesleept en neergezet (of door een Parquet- of JSON-bestand hebt gebladerd en geselecteerd), [!DNL Platform] zal onmiddellijk beginnen het dossier te verwerken en **[!UICONTROL Uploading]** wordt weergegeven op het tabblad **[!UICONTROL Add Data]** tabblad met de voortgang van het uploaden van bestanden.

![Het dialoogvenster Uploaden](../images/tutorials/ingest-batch-data/uploading-file.png)

## Dataset-meetgegevens

Nadat het bestand is geüpload, wordt het **[!UICONTROL Dataset Activity]** toont niet meer dat &quot;Er zijn geen batches toegevoegd&quot;. In plaats daarvan **[!UICONTROL Dataset Activity]** op het tabblad ziet u nu de metriek van de gegevensset. Alle metriek tonen &quot;0&quot;in dit stadium aangezien de partij nog niet heeft geladen.

Onder aan het tabblad vindt u een lijst met de **[!UICONTROL Batch ID]** van de gegevens die zojuist via de [&quot;Gegevens toevoegen aan gegevensset&quot;](#add-data-to-dataset) proces. Ook wordt informatie over de batch opgenomen, zoals de datum waarop de gegevens zijn ingevoerd, het aantal records dat is ingevoerd en de huidige status van de batch.

![Dataset-meetgegevens](../images/tutorials/ingest-batch-data/batch-id.png)

## Batchgegevens

Klik op de knop **[!UICONTROL Batch ID]** om een **[!UICONTROL Batch Overview]**, met aanvullende gegevens over de partij. Zodra de batch klaar is met laden, wordt de informatie over de batch bijgewerkt om het aantal records dat wordt ingevoerd en de bestandsgrootte weer te geven. De status verandert ook in &quot;Voltooid&quot; of &quot;Mislukt&quot;. Als de batch niet in de **[!UICONTROL Error Code]** in de sectie worden details gegeven over eventuele fouten tijdens de inname.

Zie voor meer informatie en veelgestelde vragen over het innemen van batch de bijsluiter [Handleiding voor het oplossen van problemen met de inname van batterijen](../batch-ingestion/troubleshooting.md).

Als u wilt terugkeren naar de **[!UICONTROL Dataset Activity]** scherm, klik de naam van de dataset (**[!UICONTROL Loyalty Details]**) in het breadcrumb.

![Batchoverzicht](../images/tutorials/ingest-batch-data/batch-details.png)

## Gegevensset voorvertoning

Zodra de dataset klaar is, een optie aan **[!UICONTROL Preview Dataset]** boven aan het dialoogvenster **[!UICONTROL Dataset Activity]** tab.

Klikken **[!UICONTROL Preview Dataset]** om een dialoog te openen die steekproefgegevens van binnen de dataset toont. Als de dataset gebruikend een schema werd gecreeerd, zullen de details voor het datasetschema op de linkerkant van de voorproef verschijnen. U kunt het schema uitbreiden gebruikend de pijlen om de schemastructuur te zien. Elke kolomkop in de voorvertoningsgegevens vertegenwoordigt een veld in de gegevensset.

![Gegevens over gegevensset](../images/tutorials/ingest-batch-data/dataset-preview.png)

## Volgende stappen en extra bronnen

Nu u een dataset hebt gecreeerd en met succes gegevens in opgenomen [!DNL Experience Platform], kunt u deze stappen herhalen om een nieuwe dataset tot stand te brengen of meer gegevens in de bestaande dataset in te voeren.

Lees voor meer informatie over het gebruik van batches de [Overzicht van inname in batch](../batch-ingestion/overview.md) en vergroot uw leermogelijkheden door de onderstaande video te bekijken.

>[!WARNING]
>
>De [!DNL Platform] De interface die in de volgende video wordt weergegeven, is verouderd. Raadpleeg de bovenstaande documentatie voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)
