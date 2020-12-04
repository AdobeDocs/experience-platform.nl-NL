---
keywords: Experience Platform;machine learning model;Data Science Workspace;Real-time Customer Profile;popular topics;machine learning insights
solution: Experience Platform
title: Klantprofiel in realtime verrijken met kennis van machinaal leren
topic: tutorial
type: Tutorial
description: Dit document verstrekt een geleidelijke zelfstudie om het Profiel van de Klant in real time met machine het leren inzichten te verrijken, zijn de stappen gebroken in de volgende secties, tot een outputschema/dataset leiden, een outputschema/dataset vormen, en segmenten creëren gebruikend de Bouwer van het Segment.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 0%

---


# Verrijken [!DNL Real-time Customer Profile] met kennis van machine

[!DNL Adobe Experience Platform] [!DNL Data Science Workspace] biedt de tools en bronnen om modellen voor machinaal leren te maken, te evalueren en te gebruiken om gegevensvoorspellingen en inzichten te genereren. Wanneer de machinaal het leren inzichten in een [!DNL Profile]-toegelaten dataset worden opgenomen, worden die zelfde gegevens ook opgenomen als [!DNL Profile] verslagen die dan in ondergroepen van verwante elementen kunnen worden gesegmenteerd door te gebruiken [!DNL Experience Platform Segmentation Service].

Dit document biedt een stapsgewijze zelfstudie om meer inzicht te krijgen in het leren van machines. De stappen zijn onderverdeeld in de volgende secties: [!DNL Real-time Customer Profile]

1. [Een uitvoerschema en gegevensset maken](#create-an-output-schema-and-dataset)
2. [Een uitvoerschema en gegevensset configureren](#configure-an-output-schema-and-dataset)
3. [Segmenten maken met de Segment Builder](#create-segments-using-the-segment-builder)

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende aspecten van [!DNL Adobe Experience Platform] het opnemen van [!DNL Profile] gegevens en het maken van segmenten. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

* [[!DNL Real-time Customer Profile]](../../rtcdp/overview.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Identity Service]](../../identity-service/home.md): Schakelt [!DNL Real-time Customer Profile] het overbruggen van identiteiten uit verschillende gegevensbronnen die in Platform worden opgenomen.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.

Naast de bovengenoemde documenten, wordt het ten zeerste geadviseerd dat u ook de volgende gidsen op schema&#39;s en de Redacteur van het Schema bekijkt:

* [Basisbeginselen van de schemacompositie](../../xdm/schema/composition.md): Beschrijft schema&#39;s XDM, bouwstenen, principes, en beste praktijken voor het samenstellen van schema&#39;s die binnen moeten worden gebruikt [!DNL Experience Platform].
* [Zelfstudie](../../xdm/tutorials/create-schema-ui.md)Schema-editor: Verstrekt gedetailleerde instructies voor het creëren van schema&#39;s gebruikend de Redacteur van het Schema binnen [!DNL Experience Platform].

## Een uitvoerschema en gegevensset maken {#create-an-output-schema-and-dataset}

De eerste stap naar verrijking [!DNL Real-time Customer Profile] met inzichten in scoring is te weten welk object in de praktijk (zoals een persoon) uw gegevens definiëren. Dankzij een goed begrip van uw gegevens kunt u een structuur beschrijven en ontwerpen die betekenis heeft voor uw gegevens, vergelijkbaar met het ontwerpen van een relationele database.

Het samenstellen van een schema begint door een klasse toe te wijzen. De klassen bepalen de gedragsaspecten van de gegevens het schema (verslag of tijdreeks) zal bevatten. Deze sectie verstrekt basisinstructies om een schema tot stand te brengen gebruikend de schemabouwer. Voor een meer diepgaande zelfstudie raadpleegt u de zelfstudie over het [maken van een schema met de Schema-editor](../../xdm/tutorials/create-schema-ui.md).

1. Klik in Adobe Experience Platform op het tabblad **[!UICONTROL Schema]** om de schemabrowser te openen. Klik **[!UICONTROL creëren Schema]** toegang tot de Redacteur **van het**Schema, waar u schema&#39;s op elkaar inwerkend kunt bouwen en creëren.
   ![](../images/models-recipes/enrich-rtcdp/schema_browser.png)

2. Klik in het venster **Compositie** op **[!UICONTROL Toewijzen]** om door de beschikbare klassen te bladeren.
   * Als u een bestaande klasse wilt toewijzen, klikt u op de gewenste klasse en markeert u deze. Klik vervolgens op Klasse ****toewijzen.
      ![](../images/models-recipes/enrich-rtcdp/existing_class.png)

   * Als u een aangepaste klasse wilt maken, klikt u op Nieuwe klasse **** maken in het midden van het browservenster. Geef een klassenaam, beschrijving en kies het gedrag van de klasse. Klik op Klasse **** toewijzen als u klaar bent.
      ![](../images/models-recipes/enrich-rtcdp/create_new_class.png)

   Op dit punt moet de structuur van uw schema enkele klassevelden bevatten en u kunt nu mixen toewijzen. Een mix is een groep van één of meerdere gebieden die een bepaald concept beschrijven.

3. Klik in het venster **Compositie** op **[!UICONTROL Toevoegen]** in de subsectie **Mixins** .
   * Als u een bestaande mix wilt toewijzen, klikt u op de gewenste mix en markeert u deze. Klik vervolgens op **[!UICONTROL Mixin]**toevoegen. In tegenstelling tot klassen, kunnen de veelvoudige mengen aan één enkel schema worden toegewezen zolang het aangewezen is om dit te doen.
      ![](../images/models-recipes/enrich-rtcdp/existing_mixin.png)

   * Als u een nieuwe mix wilt maken, klikt u op Nieuwe **[!UICONTROL mixin]** maken in het midden van het browservenster. Geef een naam en beschrijving voor de mix op en klik vervolgens op **[!UICONTROL Mixin]** toewijzen als u klaar bent.
      ![](../images/models-recipes/enrich-rtcdp/create_new_mixin.png)

   * Als u mengvelden wilt toevoegen, klikt u op de naam van de mix in het venster *Compositie* . Vervolgens kunt u mengvelden toevoegen door in het venster **[!UICONTROL Structuur]** op Veld ** toevoegen te klikken. Zorg ervoor dat u de eigenschappen voor mixen op basis hiervan opgeeft.
      ![](../images/models-recipes/enrich-rtcdp/mixin_properties.png)

4. Zodra u klaar bent met het bouwen van uw schema, klik het hoogste niveaugebied van uw schema binnen het venster van de *Structuur* om de eigenschappen van het schema in het juiste bezitsvenster te tonen. Geef een naam en een beschrijving op en klik op **[!UICONTROL Opslaan]** om het schema te maken.
   ![](../images/models-recipes/enrich-rtcdp/save_schema.png)

5. Creeer een outputdataset gebruikend uw onlangs gecreeerd schema door **[!UICONTROL Datasets]** van de linkernavigatiekolom te klikken, dan de klik **[!UICONTROL leidt dataset]**. Kies in het volgende scherm de optie Gegevensset **[!UICONTROL maken van schema]**.
   ![](../images/models-recipes/enrich-rtcdp/dataset_overview.png)

6. Zoek en selecteer het nieuwe schema met de schemabrowser en klik op **[!UICONTROL Volgende]**.
   ![](../images/models-recipes/enrich-rtcdp/choose_schema.png)

7. Geef een naam en een optionele beschrijving op en klik vervolgens op **[!UICONTROL Voltooien]** om de gegevensset te maken.
   ![](../images/models-recipes/enrich-rtcdp/configure_dataset.png)

Nu u een gecreeerd dataset van het outputschema hebt, bent u klaar aan de volgende sectie verder om hen voor de verrijking van het Profiel te vormen en toe te laten.

## Een uitvoerschema en gegevensset configureren {#configure-an-output-schema-and-dataset}

Alvorens u een dataset voor kunt toelaten [!DNL Profile], moet u het schema van de dataset aan het hebben van een primair identiteitsgebied vormen en dan het schema voor toelaten [!DNL Profile]. Als u een nieuw schema wilt creëren en toelaten, kunt u naar het leerprogramma verwijzen bij het [creëren van een schema gebruikend de Redacteur](../../xdm/tutorials/create-schema-ui.md)van het Schema. Volg anders de instructies hieronder om een bestaand schema en een dataset toe te laten.

1. Op Adobe Experience Platform, gebruik schemabrowser om het outputschema te vinden u wenst om toe te laten [!DNL Profile] en zijn naam te klikken om zijn samenstelling te bekijken.
   ![](../images/models-recipes/enrich-rtcdp/schemas.png)

2. Breid de schemastructuur uit en vind een aangewezen gebied om als primaire herkenningsteken te plaatsen. Klik op het gewenste veld om de eigenschappen ervan weer te geven.
   ![](../images/models-recipes/enrich-rtcdp/schema_structure.png)

3. Stel het veld in als de primaire identiteit door de eigenschap **[!UICONTROL Identiteit]** van het veld, de eigenschap **[!UICONTROL Primaire identiteit]** en vervolgens een geschikte **[!UICONTROL identiteitsnaamruimte]** in te schakelen. Klik op **[!UICONTROL Toepassen]** als u de wijzigingen hebt aangebracht.
   ![](../images/models-recipes/enrich-rtcdp/set_identity.png)

4. Klik op het bovenste object van de schemastructuur om de schemaeigenschappen weer te geven en schakel het schema voor Profiel in door de **[!UICONTROL profielschakelaar]** in en uit te schakelen. Klik **[!UICONTROL sparen]** om uw veranderingen te voltooien, dataset die gebruikend dit schema werd gecreeerd kan nu voor Profiel worden toegelaten.
   ![](../images/models-recipes/enrich-rtcdp/enable_schema.png)

5. Gebruik datasetbrowser om de dataset te vinden u wenst om toe te laten [!DNL Profile] en zijn naam te klikken om tot zijn details toegang te hebben.
   ![](../images/models-recipes/enrich-rtcdp/datasets.png)

6. Laat de dataset voor toe [!DNL Profile] door de schakelaar van het **[!UICONTROL Profiel]** in de juiste informatiekolom van een knevel te voorzien.
   ![](../images/models-recipes/enrich-rtcdp/enable_dataset.png)

Wanneer het gegeven in een [!DNL Profile]-Toegelaten dataset wordt opgenomen, worden die zelfde gegevens ook opgenomen als [!DNL Profile] verslagen. Nu uw schema en dataset wordt voorbereid, produceer sommige gegevens in de dataset door het uitvoeren van het scoren looppas gebruikend een aangewezen model, en ga met dit leerprogramma verder om inzicht tot segmenten te leiden gebruikend de Bouwer van het Segment.

## Segmenten maken met de Segment Builder {#create-segments-using-the-segment-builder}

Nu u inzichten in uw [!DNL Profile]-Toegelaten dataset hebt geproduceerd en opgenomen, kunt u die gegevens beheren door ondergroepen van verwante elementen te identificeren gebruikend de Bouwer van het Segment. Volg de onderstaande stappen om uw eigen segmenten te maken.

1. In Adobe Experience Platform klikt u op het tabblad **[!UICONTROL Segmenten]** gevolgd door Segment **** maken voor toegang tot de Segment Builder.
   ![](../images/models-recipes/enrich-rtcdp/segments_overview.png)

2. Binnen de Bouwer van het Segment, verleent de linkerspoorlijn toegang tot de kernbouwstenen van segmenten: kenmerken, gebeurtenissen en bestaande segmenten. Elke bouwsteen verschijnt in zijn eigen respectieve lusje. Selecteer de klasse tot waar uw [!DNL Profile]-toegelaten schema zich dan uitbreidt doorblader en vind de bouwstenen voor uw segment.
   ![](../images/models-recipes/enrich-rtcdp/segment_builder.png)

3. De belemmering en laat vallen bouwstenen op het canvas van de regelbouwer, voltooit hen door vergelijkende verklaringen te verstrekken.
   ![](../images/models-recipes/enrich-rtcdp/drag_fill.gif)

4. Terwijl u uw segment bouwt, kunt u geschatte segmentresultaten voorvertonen door het deelvenster *Segmenteigenschappen* te observeren.
   ![](../images/models-recipes/enrich-rtcdp/preview_segment.gif)

5. Selecteer een geschikt **[!UICONTROL samenvoegbeleid]**, geef een naam en een optionele beschrijving op en klik vervolgens op **[!UICONTROL Opslaan]** om het nieuwe segment te voltooien.
   ![](../images/models-recipes/enrich-rtcdp/save_segment.png)


## Volgende stappen {#next-steps}

Dit document liep u door de stappen die worden vereist om een schema en dataset voor toe te laten [!DNL Profile], en toonde kort het werkschema voor het creëren van inzicht segmenten gebruikend de Bouwer van het Segment aan. Meer over segmenten en de Bouwer van het Segment leren, verwijs naar het de dienstoverzicht [van de](../../segmentation/home.md)Segmentatie.