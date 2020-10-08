---
keywords: Experience Platform;home;popular topics;Segmentation Service;segmentation;Segmentation;create a dataset;export audience segment;export segment;
solution: Experience Platform
title: Een dataset maken voor het exporteren van een publiekssegment
topic: tutorial
type: Tutorial
description: Deze zelfstudie doorloopt de stappen die worden vereist om een dataset tot stand te brengen die voor het uitvoeren van een publiekssegment kan worden gebruikt gebruikend het Experience Platform UI.
translation-type: tm+mt
source-git-commit: fce215edb99cccc8be0109f8743c9e56cace2be0
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---


# Een dataset maken voor het exporteren van een publiekssegment

[!DNL Adobe Experience Platform] staat u toe om klantenprofielen in publiek gemakkelijk te segmenteren die op specifieke attributen worden gebaseerd. Zodra de segmenten zijn gecreeerd, kunt u dat publiek naar een dataset uitvoeren waar het kan worden betreden en worden gehandeld. Opdat de uitvoer succesvol is, moet de dataset behoorlijk worden gevormd.

Dit leerprogramma doorloopt de stappen worden vereist om een dataset tot stand te brengen die voor het uitvoeren van een publiekssegment kan worden gebruikt gebruikend [!DNL Experience Platform] UI.

Deze zelfstudie houdt rechtstreeks verband met de stappen die in de zelfstudie worden beschreven voor het [evalueren van en het openen van segmentresultaten](./evaluate-a-segment.md). Het evalueren van een segmentleerprogramma verstrekt stappen voor het creëren van een dataset gebruikend [!DNL Catalog Service] API, terwijl dit leerprogramma stappen beschrijft om een dataset tot stand te brengen gebruikend [!DNL Experience Platform] UI.

## Aan de slag

Om een segment uit te voeren, moet de dataset op het [!DNL XDM Individual Profile Union Schema]. worden gebaseerd. Een verenigingsschema is een systeem-geproduceerd, read-only schema dat de gebieden van alle schema&#39;s samenvoegt die de zelfde klasse delen, in dit geval dat de [!DNL XDM Individual Profile] klasse is. Voor meer informatie over de schema&#39;s van de verenigingsmening, te zien gelieve de sectie van het Profiel van de Klant in [real time van de Ontwikkelaar van het Registratie van het Schema gids](../../xdm/schema/composition.md#union).

Om verenigingsschema&#39;s in UI te bekijken, klik **[!UICONTROL Profielen]** in de linkernavigatie, dan klik op het **[!UICONTROL Unieschema]** tabel zoals hieronder getoond.

![Verenigingsschema-tabblad in gebruikersinterface van Experience Platform](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Werkruimte Gegevensbestanden

De datasetwerkruimte binnen [!DNL Experience Platform] UI staat u toe om alle datasets te bekijken en te beheren die uw organisatie IMS heeft gemaakt, evenals nieuwe degenen te creëren.

Om de datasetwerkruimte te bekijken, klik **[!UICONTROL Datasets]** in de linkernavigatie, dan klik op het **[!UICONTROL Browse]** lusje. De werkruimte van datasets bevat een lijst van datasets, met inbegrip van kolommen die naam tonen, (datum en tijd), bron, schema, en laatste partijstatus, evenals de datum en de tijd de dataset het laatst werd bijgewerkt. Afhankelijk van de breedte van elke kolom moet u mogelijk naar links of rechts schuiven om alle kolommen weer te geven.

>[!NOTE]
>
>Klik op het filterpictogram naast de zoekbalk om filtermogelijkheden te gebruiken om alleen die datasets weer te geven waarvoor [!DNL Real-time Customer Profile].

![Alle gegevenssets weergeven](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Een gegevensset maken

Als u een gegevensset wilt maken, klikt u op Gegevensset **** maken rechtsboven in de werkruimte **[!UICONTROL Gegevenssets]** .

![Klik op Gegevensset maken](../images/tutorials/segment-export-dataset/dataset-click-create.png)

Op het **[!UICONTROL Create scherm van de Dataset]** , klik **[!UICONTROL Create Dataset van Schema]** om verder te gaan.

![Gegevensbron selecteren](../images/tutorials/segment-export-dataset/create-dataset.png)

## XDM Individueel profiel verenigingsschema selecteren

Om [!DNL XDM Individual Profile Union Schema] voor gebruik in uw dataset te selecteren, vind het &quot;[!UICONTROL Individuele Profiel]XDM&quot;schema met een type van &quot;[!UICONTROL Unie]&quot;op het **[!UICONTROL Uitgezochte Schema]** scherm.

Selecteer het keuzerondje naast **[!UICONTROL XDM Individueel Profiel]** en klik vervolgens op **[!UICONTROL Volgende]** in de rechterbovenhoek.

![Schema selecteren](../images/tutorials/segment-export-dataset/select-schema.png)

## Gegevensset configureren

Op het **[!UICONTROL Configure scherm van de Dataset]** , zult u uw dataset een naam moeten geven en kan een beschrijving van de dataset ook verstrekken.

**Opmerkingen over gegevenssetnamen:**
- De namen van gegevenssets moeten kort en beschrijvend zijn, zodat de gegevensset later gemakkelijk in de bibliotheek kan worden gevonden.
- Dataset-namen moeten uniek zijn, wat betekent dat ze ook specifiek genoeg moeten zijn om in de toekomst niet opnieuw te worden gebruikt.
- Het is beste praktijken om extra informatie over de dataset te verstrekken gebruikend het beschrijvingsgebied, aangezien het andere gebruikers kan helpen tussen datasets in de toekomst differentiëren.

Als de gegevensset een naam en een beschrijving heeft, klikt u op **[!UICONTROL Voltooien]**.

![Gegevensset configureren](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Gegevensactiviteit

Een lege dataset is nu gecreeerd en u bent teruggekeerd aan het lusje van de Activiteit **[!UICONTROL van de]** Dataset in de werkruimte van **[!UICONTROL Datasets]** . U zou de naam van de dataset in de upper-left hoek van de werkruimte, samen met een bericht moeten zien dat &quot;Geen partijen zijn toegevoegd.&quot; Dit moet worden verwacht aangezien u nog geen partijen aan deze dataset hebt toegevoegd.

Aan de rechterkant van de werkruimte van Datasets zult u het lusje zien van **[!UICONTROL Info]** dat informatie met betrekking tot uw nieuwe dataset zoals dataset identiteitskaart, naam, beschrijving, lijstnaam, schema, het stromen, en bron omvat. Het tabblad **[!UICONTROL Info]** bevat ook informatie over het tijdstip waarop de gegevensset is gemaakt en de datum waarop deze voor het laatst is gewijzigd.

Noteer de **[!UICONTROL gegevensset-id]**, omdat deze waarde vereist is om de exportworkflow voor het publiekssegment te voltooien.

![Gegevensactiviteit](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Volgende stappen

Nu u een dataset hebt gecreeerd die op wordt gebaseerd [!DNL XDM Individual Profile Union Schema], kunt u datasetidentiteitskaart gebruiken om tot de [evaluatie en de toegang tot van segmentresultaten](./evaluate-a-segment.md) leerprogramma voort te gaan.

Op dit ogenblik, gelieve terug te keren naar de evaluerende zelfstudie van segmentresultaten en van het [produceren profielen voor publieksleden](./evaluate-a-segment.md#generate-profiles) stap van het uitvoeren van een segmentwerkschema te plukken.
