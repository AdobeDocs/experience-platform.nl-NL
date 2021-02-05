---
keywords: Experience Platform;huis;populaire onderwerpen;de Dienst van de segmentatie;segmentatie;creeer een dataset;het segment van het uitvoerpubliek;het uitvoersegment;
solution: Experience Platform
title: Creeer een Dataset voor het Uitvoeren van een Segment van de Publiek
topic: tutorial
type: Tutorial
description: Deze zelfstudie doorloopt de stappen die worden vereist om een dataset tot stand te brengen die voor het uitvoeren van een publiekssegment kan worden gebruikt gebruikend het Experience Platform UI.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---


# Een dataset maken voor het exporteren van een publiekssegment

[!DNL Adobe Experience Platform] staat u toe om klantenprofielen in publiek gemakkelijk te segmenteren die op specifieke attributen worden gebaseerd. Zodra de segmenten zijn gecreeerd, kunt u dat publiek naar een dataset uitvoeren waar het kan worden betreden en worden gehandeld. Opdat de uitvoer succesvol is, moet de dataset behoorlijk worden gevormd.

Deze zelfstudie doorloopt de stappen die worden vereist om een dataset tot stand te brengen die voor het uitvoeren van een publiekssegment kan worden gebruikt gebruikend [!DNL Experience Platform] UI.

Deze zelfstudie houdt rechtstreeks verband met de stappen die worden beschreven in de zelfstudie voor [het evalueren en benaderen van segmentresultaten](./evaluate-a-segment.md). De evaluatie van een segmentzelfstudie verstrekt stappen voor het creëren van een dataset gebruikend [!DNL Catalog Service] API, terwijl dit leerprogramma stappen beschrijft om een dataset tot stand te brengen gebruikend [!DNL Experience Platform] UI.

## Aan de slag

Als u een segment wilt exporteren, moet de gegevensset zijn gebaseerd op [!DNL XDM Individual Profile Union Schema]. Een verenigingsschema is een systeem-geproduceerd, read-only schema dat de gebieden van alle schema&#39;s samenvoegt die de zelfde klasse delen, in dit geval dat de [!DNL XDM Individual Profile] klasse is. Voor meer informatie over de schema&#39;s van de verenigingsmening, te zien gelieve [sectie van het Profiel van de Klant in real time van de Ontwikkelaar van het Registratie van het Schema gids](../../xdm/schema/composition.md#union).

Om verenigingsschema&#39;s in UI te bekijken, klik **[!UICONTROL Profielen]** in de linkernavigatie, dan klik op **[!UICONTROL Unieschema]** tabel zoals hieronder getoond.

![Verenigingsschema-tabblad in gebruikersinterface van Experience Platform](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Werkruimte Gegevensbestanden

De datasetwerkruimte binnen [!DNL Experience Platform] UI staat u toe om alle datasets te bekijken en te beheren die uw organisatie IMS heeft gemaakt, evenals nieuwe te creëren.

Om de datasetwerkruimte te bekijken, klik **[!UICONTROL Datasets]** in de linkernavigatie, dan klik op **[!UICONTROL Browse]** tabel. De datasetwerkruimte bevat een lijst van datasets, met inbegrip van kolommen die naam tonen, (datum en tijd), bron, schema, en laatste partijstatus, evenals de datum en de tijd de dataset het laatst werd bijgewerkt. Afhankelijk van de breedte van elke kolom moet u mogelijk naar links of rechts schuiven om alle kolommen weer te geven.

>[!NOTE]
>
>Klik op het filterpictogram naast de zoekbalk om filtermogelijkheden te gebruiken om alleen die datasets weer te geven die zijn ingeschakeld voor [!DNL Real-time Customer Profile].

![Alle gegevenssets weergeven](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Een gegevensset maken

Als u een gegevensset wilt maken, klikt u op **[!UICONTROL Dataset maken]** rechtsboven in de werkruimte **[!UICONTROL Datasets]**.

![Klik op Gegevensset maken](../images/tutorials/segment-export-dataset/dataset-click-create.png)

Klik op **[!UICONTROL Dataset maken]** in het scherm **[!UICONTROL Gegevensset maken van schema]** om door te gaan.

![Gegevensbron selecteren](../images/tutorials/segment-export-dataset/create-dataset.png)

## XDM Individueel profiel verenigingsschema selecteren

Als u het schema [!DNL XDM Individual Profile Union Schema] wilt selecteren voor gebruik in uw gegevensset, zoekt u het schema &quot;[!UICONTROL XDM Individual Profile]&quot; met het type &quot;[!UICONTROL Union]&quot; op het scherm **[!UICONTROL Select Schema]**.

Selecteer het keuzerondje naast **[!UICONTROL XDM Individual Profile]**, dan klik **[!UICONTROL Next]** in de hoger-juiste hoek.

![Schema selecteren](../images/tutorials/segment-export-dataset/select-schema.png)

## Gegevensset configureren

Op **[!UICONTROL vorm het scherm Dataset]**, zult u uw dataset een naam moeten geven en kan een beschrijving van de dataset ook verstrekken.

**Opmerkingen over gegevenssetnamen:**
- De namen van gegevenssets moeten kort en beschrijvend zijn, zodat de gegevensset later gemakkelijk in de bibliotheek kan worden gevonden.
- Dataset-namen moeten uniek zijn, wat betekent dat ze ook specifiek genoeg moeten zijn om in de toekomst niet opnieuw te worden gebruikt.
- Het is beste praktijken om extra informatie over de dataset te verstrekken gebruikend het beschrijvingsgebied, aangezien het andere gebruikers kan helpen tussen datasets in de toekomst differentiëren.

Als de gegevensset een naam en een beschrijving heeft, klikt u op **[!UICONTROL Voltooien]**.

![Gegevensset configureren](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Gegevensactiviteit

Er is nu een lege dataset gemaakt en u bent teruggestuurd naar het tabblad **[!UICONTROL Datasetactiviteit]** in de werkruimte **[!UICONTROL Datasets]**. U zou de naam van de dataset in de upper-left hoek van de werkruimte, samen met een bericht moeten zien dat &quot;Geen partijen zijn toegevoegd.&quot; Dit moet worden verwacht aangezien u nog geen partijen aan deze dataset hebt toegevoegd.

Rechts in de werkruimte Datasets ziet u het tabblad **[!UICONTROL Info]** met informatie over uw nieuwe gegevensset, zoals id, naam, beschrijving, tabelnaam, schema, streaming en bron. Het tabblad **[!UICONTROL Info]** bevat ook informatie over het tijdstip waarop de gegevensset is gemaakt en de datum waarop deze voor het laatst is gewijzigd.

Noteer **[!UICONTROL Dataset ID]**, aangezien deze waarde vereist is om de workflow voor het exporteren van het publiekssegment te voltooien.

![Gegevensactiviteit](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Volgende stappen

Nu u een dataset hebt gecreeerd die op [!DNL XDM Individual Profile Union Schema] wordt gebaseerd, kunt u datasetidentiteitskaart gebruiken om [het evalueren en tot segmentresultaten](./evaluate-a-segment.md) leerprogramma voort te zetten.

Op dit ogenblik, gelieve terug te keren naar de evaluerende zelfstudie van segmentresultaten en van [het produceren van profielen voor publieksleden ](./evaluate-a-segment.md#generate-profiles) stap van het uitvoeren van een segmentwerkschema op te halen.
